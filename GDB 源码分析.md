# 文件结构

# 几个部件的分析

## 函数前导代码分析（Prologue analysis）

代码：`gdb/prologue-value.h`，`gdb/prologue-value.c`

函数前导代码其实很简单也很固定，它主要就是进入一个函数时进行的代码操作，用来建立栈帧，并为临时变量开好空间。这里展示一个 x86 汇编的最简单情形：

```assembly
push ebp
mov ebp, esp
sub esp, N
```

很简单，很友好，不是吗？

那么为什么要对这块代码进行重点分析呢？一方面，这是一个函数开头的部分，可以用来分析这个函数调用栈的情况，并分析这个函数所使用的临时变量地址；另一方面，虽然看起来这段代码很可爱，但是随着编译器的复杂化和在调度指令时日益激进的策略，它往往会变得面目全非。但无论如何，这段代码总归是相对简单的部分。

事实上，在现代的 gcc 编译器中往往会给出调用栈信息（call frame information, CFI），其中描述了如何寻找栈的基地址和存储的寄存器等信息，但是这些信息并不总是存在。如果它们不存在，我们就必须采用一些策略来试图解读这些信息。为了解读这些信息，我们就采用一种对指令“抽象解读”的策略，也就是下面将介绍的模糊计算策略。

### 值的模糊计算

在 `prologue-value.h` 中，定义了如下结构：

```c++
enum prologue_value_kind {
	pvk_unknown,
	pvk_constant,
	pvk_register
};
```

这里所描述的是一个 prologue 值的类型，分别表示未知、常数和寄存器，它决定了在下面的结构体中，后面两个参数应该如何解读。

```c++
struct prologue_value {
    enum prologue_value_kind kind;
    int reg;
    CORE_ADDR k;
};
typedef struct prologue_value pv_t;
```

- 如果类型是 `pvk_unknown`，那么后面两个参数都没有意义，毕竟我们对它一无所知；
- 如果类型是 `pvk_constant`，这表明这个值就是常数，记录在 `k` 中。注意，所谓的 `CORE_ADDR` 实际上就是一个 `uint64_t`；
- 如果类型是 `pvk_register`，这表明寄存器 `reg` 所对应的原始值为 `初始值 + k` ，其中 `reg` 为 GDB 标定的寄存器编号，是为了防止不同架构带来的跨平台问题。在开始分析之前，所有寄存器都会被标为 `{pvk_register, reg, 0}`

每个类型都有相关的初始化函数，它们实现起来并不困难：

```c++
pv_t pv_unknown(void) {
    pv_t v = {pvk_unknown, 0, 0};
    return v;
}

pv_t pv_constant(CORE_ADDR k) {
    pv_t v;
    v.kind = pvk_constant;
    v.reg = -1;
    v.k = k;
    return v;
}

pv_t pv_register(int reg, CORE_ADDR k) {
    pv_t v;
    v.kind = pvk_register;
    v.reg = reg;
    v.k = k;
    return v;
}
```

随后我们要对这些值进行“保守估计”，保守估计的意思是说，我们会把一个值正确估计或者设为未知，但不能出现错误的估计。对应于这种估计方式的逻辑变量是这样的：

```cpp
enum pv_boolean {
    pv_maybe,
    pv_definite_yes,
    pv_definite_no
};
```

然后通过看相关的函数来理解其原理：

```c++
static void constant_last(pv_t *a, pv_t *b) {
    if (a->kind == pvk_constant && b->kind != pvk_constant) {
        pv_t temp = *a;
        *a = *b;
        *b = temp;
    }
}
```

这个函数就是个辅助函数。如果前者是常数而后者不是常数，对两者做个交换。这个函数在后面只是用来减少需要处理的情况总数的。接下来是对一大批寄存器运算的模拟。

```c++
pv_t pv_add(pv_t a, pv_t b) {
    constant_last(&a, &b);
    if (a.kind == pvk_register && b.kind == pvk_constant) {
        return pv_register(a.reg, a.k + b.k);
    } else if (a.kind == pvk_constant && b.kind == pvk_constant) {
        return pv_constant(a.k + b.k);
    } else {
        return pv_unknown();
    }
}

pv_t pv_add_constant(pv_t v, CORE_ADDR k) {
    return pv_add(v, pv_constant(k));
}
```

首先实现加法的计算。这里的过程看起来很简单：两个常数可以加，寄存器可以加上常数，但其他的加法都返回未知。如果要处理常数加法，那就将常数转换成对应的类型再相加。这里不妨停一下思考两个问题：

- 为什么寄存器和寄存器不能相加？
- 为什么常数加法的情况在两个函数中都进行了处理？

这里我们需要注意，我们并不会实际执行程序，只是取其中的一个片段进行分析。在分析这个片段的时候，寄存器的初始值是未知的。因此，我们总共知道的就是，某个寄存器相比其进入这个片段之前多了或者少了多少。如果将寄存器与寄存器相加，那么势必要用到初始值，也就是说，它的结果对我们来说是未知的。

对于第二个问题，需要注意，加常数的情况并不仅仅存在于显式的指令编码中。例如，在下面将读到的 `logical_and` 函数中，如果出现与常数 `0` 做 `and` 操作，这个寄存器的值就会变成常数 `0` ，于是，当它与另一个寄存器相加时，就会进入寄存器与常数相加的情形。

接下来按照这个思路，可以很简单的实现减法和逻辑与运算，代码如下：

```cpp
pv_t pv_subtract(pv_t a, pv_t b) {
	constant_last(&a, &b);
    if (a.kind == pvk_constant && b.kind == pvk_constant) {
        return pv_constant(a.k - b.k);
    } else if (a.kind == pvk_register && b.kind == pvk_constant) {
        return pv_register(a.reg, a.k - b.k);
    } else if (a.kind == pvk_register && b.kind == pvk_register 
               && a.reg == b.reg) {
        return pv_constant (a.k - b.k);
    } else {
        return pv_unknown();
    }
}

pv_t pv_logical_and(pv_t a, pv_t b) {
    constant_last(&a, &b);
    if (a.kind == pvk_constant && b.kind == pvk_constant) {
        return pv_constant(a.k & b.k);
    } else if (b.kind == pvk_constant && b.k == 0) {
        return pv_constant(0);
    } else if (b.kind == pvk_constant && b.k == ~(CORE_ADDR) 0) {
        return a;
    } else if (a.kind == pvk_register && b.kind == pvk_register 
               && a.reg == b.reg && a.k == b.k) {
        return a;
    } else {
        return pv_unknown();
    }
}
```

这两段的代码逻辑也相当清晰，如果理解了什么叫做保守估计，那么应该也能很轻松地读懂。主要的难点在于理解什么情况下可以对这个操作做出准确的估计，什么时候不能。基于这些计算方式，我们就可以基本上知道某段代码结束之后，能得到怎样的结果了。

这里需要注意，如果出现了除算术指令之外的其他指令，其结果就基本上全是 `pvk_unknown` 了。所以，这里所做的只是一个前导代码分析，因为函数的前导代码往往不会包含太复杂的东西。

### 对模糊值做出判断

当我们知道一段代码运行之后的结果之后，我们就可以尝试确定一些东西了，比如某个对象是否落在一个数组里。但在进行这些判断之前，先要有三个最普通的判断函数：判断某个值是否是常数、是否是某个寄存器、是否是某寄存器 `初始值 + k` 的结果，这三个函数将成为后面应用的基石。

```cpp
int pv_is_constant(pv_t a) {
    return (a.kind == pvk_constant);
}

int pv_is_register(pv_t a, int r) {
    return (a.kind == pvk_register && a.reg == r);
}

int pv_is_register_k(pv_t a, int r, CORE_ADDR k) {
    return (a.kind == pvk_register && a.reg == r && a.k == k);
}
```

接下来我们要开始考虑，如何判断一个对象是否落在某个数组里。很显然，我们需要考虑如何描述一个对象和如何描述一个数组。我们需要的参数有：

- 描述一个对象在内存中的位置和长度，`pv_t addr` 和 `CORE_ADDR size`；
- 描述一个数组在内存里的位置和长度，`pv_t array_addr` 和 `array_len` （数组长度），以及 `CORE_ADDR elt_size` （数组内每个元素的大小）；
- 返回值，是不是指向某个完整元素，以及如果指向某个完成元素，其对应的指标 `int *i`。

在开始考虑如何写这个函数之前，我们需要明确地指出这个函数的功能以及它的返回类型。它的返回类型是 `enum pv_boolean` 型：

- 如果这个对象一定落在数组中，那么返回 `pv_definite_yes` ，并把 `I`；
- 如果这个对象一定不落在数组中，那么返回 `pv_definite_no`；
- 如果不能判断、或者不指向完整的数组元素，那么返回 `pv_maybe` 。

好，接下来可以开始写这个函数了：

```cpp
enum pv_boolean pv_is_array_ref(pv_t addr, CORE_ADDR size, 
                                pv_t array_addr, CORE_ADDR array_len, 
                                CORE_ADDR elt_size, int *i) {
	pv_t offset = pv_subtract(addr, array_addr);
    if (offset.kind == pvk_constant) {
        if (offset.k <= -size && offset.k >= array_len * elt_size) {
            return pv_definite_no;
        } else if (offset.k % elt_size != 0 || size != elt_size) {
            return pv_maybe;
        } else {
            *i = offset.k / elt_size;
            return pv_definite_yes;
        }
    } else {
        return pv_maybe;
    }
}
```

这里的逻辑其实很简单：如果对象的起始地址和数组起始地址不能相减或相减不为常数，我们都不能严格做出判断。然后我们考虑这样的情形：

![case1.drawio](F:\notes\case1.drawio.png)

这里就是第一个比较的来源：只有当 `offset <= -size` 时，才能明确判断说这个元素不在数组内，同样的，第二个比较发生在右边。然后检查是否对齐。如果不对齐，那只能是 `pv_maybe`。只有当对齐且元素大小等于数组元素大小，且偏移量落在数组之内时，才会返回 `pv_definite_yes` 。

### 利用这种分析方式追踪某篇内存中的区域里的值

首先考虑一个问题：如何记录一个内存中的数据？不要忘记，我们需要分析一个函数的前导代码，而前导代码往往做的是栈操作。那么，既然我们不能预先知道栈地址的值，我们自然就得以一个寄存器作为基地址，那么我们需要存储的就是某个地址距离基地址寄存器的偏移量；同时，内存中的对象并不自带类型，所以需要长度作为其标识；最后，我们还要记下它的值。这就是下面这个结构体想要做的事情：

```cpp
struct pv_area::area_entry {
    struct area_entry *prev, *next;
    CORE_ADDR offset;
    CORE_ADDR size;
    pv_t value;
}
```

注意到它有两个指向前后的指针。事实上，它构成了一个环形双向链表，在后面的分析中，我们还会看到，它是以偏移量的大小进行排序的。然后就是把这个双向链表包装成一个类：

```c++
class pv_area {
private:
    int m_base_reg;
    CORE_ADDR m_addr_mask;
    struct area_entry *m_entry;
}
```

其中除了指向这样一个链表的指针之外，还有基地址寄存器的寄存器号，以及一个地址的掩码。看到后面之后会更容易理解这个掩码的目的，在这里我们只需要简单地认为，我们的地址空间是一个环形，前后相连即可。

接下来看类里面的三个私有成员函数：

```cpp
void pv_area::clear_entries() {
    struct area_entry *e = m_entry;
    if (e) {
        do {
            struct area_entry *next = e.next;
            xfree(e);
            e = next;
        } while (e != m_entry);
        m_entry = 0;
    }
}
```

这个函数用来清空双向链表。其中比较需要注意的就是 `xfree` 这个函数，事实上这个函数和内存保护有关，在读到这里的时候，我们不妨将其当成一个简单的 `free` 函数理解。

```cpp
struct pv_area::area_entry *pv_area::find_entry(CORE_ADDR offset) {
	struct area_entry *e = m_entry;
    if (!e) {
        return 0;
    }
    while (((e->next->offset - offset) & m_addr_mask) < 
           ((e->offset - offset) & m_addr_mask)) {
        e = e->next;
    }
    while (((e->prev->offset - offset) & m_addr_mask) < 
           ((e->offset - offset) & m_addr_mask)) {
        e = e->prev;
    }
    m_entry = e;
    return e;
}
```

这个函数用来找到在 `offset` 之后的第一项。如果本身这片区域一项也没有，那么就自然地返回一个空指针。而如果 `offset` 中一项也没有，那当然就会返回较为靠前的一项。这里需要澄清的是，因为 `m_entry` 指向的是环形链表中的**任意**一项，往后扫描和往前扫描都是必须的。最后一步将 `m_entry` 设为 `e` 就是出于局部性的假定，假定最近被访问的这项很可能再次被访问，从而提高整个数据结构的搜索效率。

在此不妨停下来思考一个问题：哪怕没有掩码的问题，是否有可能直接写成 `e->next->offset < e->offset` ？答案是否定的，原作者在注释中特别表明了这一点：

```cpp
   /*Note that, even setting aside the addr_mask stuff, we must not
     simplify this, in high school algebra fashion, to
     (e->next->offset < e->offset), because of the way < interacts
     with wrap-around.  We have to subtract offset from both sides to
     make sure both things we're comparing are on the same side of the
     discontinuity.  */
```

解释很清楚，在这也就不翻译了。

第三个函数就是一个判断 `offset` 处 `size` 大小的一项是否与某个 `entry` 重合，非常简单，直接贴代码不解释：

```cpp
int pv_area::overlaps(struct area_entry *entry, CORE_ADDR offset, CORE_ADDR size) {
    return (((entry->offset - offset) & m_addr_mask) < size || 
            ((offset - entry->offset) & m_addr_mask) < entry->size);
}
```

接下来观察一下公有的成员函数，首先来看构建过程：

```cpp
pv_area::pv_area(int base_reg, int addr_bit): m_base_reg(base_reg),
	m_addr_mask(((((CORE_ADDR) 1) << (addr_bit - 1)) - 1) << 1) | 1),
	m_entry(nullptr){}
```

非常简单的构造函数，但是这里我们就可以重新解释一下地址掩码的含义了。当我们有一个 32 bit 的地址时，自然而然地我们只希望其比较 32 bit，但是寄存器又是可以有 64 bit 的：也就是说，有一部分是需要被抛弃的。

一个很细节的问题是，为什么不把这个表达式写成 `((CORE_ADDR) 1 << addr_bit) - 1` ？注意，移位的位数与类型的宽度相同时，得到的结果是未定义的。如果采取上面代码的形式，就一定能够保证得到正确的结果。

析构函数非常简单：

```cpp
pv_area::~pv_area() {
    clear_entries();
}
```

然后用了一个有趣的小技巧取消了默认析构函数和 `operator=`：

```cpp
DISABLE_COPY_AND_ASSIGN(pv_area);
```

宏定义如下，这是为了与不同版本的 c++ 标准兼容：

```cpp
#if defined(__cplusplus) && __cplusplus >= 201103
#define DISABLE_COPY_AND_ASSIGN(TYPE)		\
  TYPE (const TYPE&) = delete;			\
  void operator= (const TYPE &) = delete
  #else
#define DISABLE_COPY_AND_ASSIGN(TYPE)		\
  TYPE (const TYPE&);				\
  void operator= (const TYPE &)
#endif
```

接下来我们就要正式进行模拟存取了。下面这个成员函数用来将一个 `size` 大小的值 `value` 写入到 `addr` 处：

```cpp
void pv_area::store(pv_t addr, CORE_ADDR size, pv_t value) {
    if (store_would_trash(addr)) {
        clear_entries();
    } else {
        CORE_ADDR offset = addr.k;
        struct area_entry *e = find_entry(offset);
        while (e && overlaps(e, offset, size)) {
            struct area_entry *next = (e->next == e) ? 0 : e->next;
            e->prev->next = e->next;
            e->next->prev = e->prev;
            xfree(e);
            e = next;
        }
        m_entry = e;
    }
    if (value.kind == pvk_unknown) {
        return;
    } else {
        CORE_ADDR offset = addr.k;
        struct area_entry *e = XNEW(struct area_entry);
        e->offset = offset;
        e->size = size;
        e->value = value;
        if (m_entry) {
            e->prev = m_entry->prev;
            e->next = m_entry;
            e->prev->next = e->next->prev = e;
        } else {
            e->prev = e->next = e;
            m_entry = e;
        }
    }
}
```

这个函数稍微有点长，但是思路其实挺简单的：

- 如果存储操作会使得我现在所有的表项都被无效化，那么直接先把表清掉；
- 否则的话，清掉所有与这个值重合的项，因为这些项都会被覆写掉；
- 然后，如果我需要存的值未知，那就直接返回；
- 如果我需要存的值已知，那就创建出这一项并把它插进去。

`XNEW(T)` 事实上拓展到了泛型 `xnew<T>()` ，这个函数和前面的 `xfree` 一样，只需要当成一个 `new` 就行，暂时不需要深究；接下来需要考虑的是，什么时候我可能无效化整个表：

```cpp
bool pv_area::store_would_trash(pv_t addr) {
    return (addr.kind == pvk_unknown ||
           addr.kind == pvk_constant ||
           (addr.kind == pvk_register && addr.reg != m_base_reg));
}
```

事实上说这种情况可能无效化整个表是不准确的。准确地说，是我们不能确定这次存储和我们现在的表有什么关系，为了方便起见，我们就直接认为这整个表的分析是不可能的，因而就将其抛弃了。这个函数还会被在其他地方调用，比如，考虑取一个值的问题：

```cpp
pv_t pv_area::fetch(pv_t addr, CORE_ADDR size) {
    if (!m_entry || store_would_trash(addr)) {
        return pv_unknown();
    } else {
        CORE_ADDR offset = addr.k;
        struct area_entry *e = find_entry(offset);
        if (e->offset == offset && e->size == size) {
            return e->value;
        } else {
            return pv_unknown();
        }
    }
}
```

很显然，这个函数的核心还是保守估计。需要注意的是第一行判断，如果表里没有内容，或者这个地址和表无关，那就返回未知。这里，“和表无关”才是上面那个函数真正的语义。

当然，我们可以找找我们的表中有没有关于某个寄存器值的信息：

```cpp
bool pv_area::find_reg(struct gdbarch *gdbarch, int reg, CORE_ADDR *offset_p) {
    struct area_entry *e = m_entry;
    if (e) {
        do {
            if (e->value.kind == pvk_register 
                && e->value.reg == reg
                && e->value.k == 0 
                && e->size == register_size(gdbarch, reg)) {
                if (offset_p) {
                    *offset_p = e->offset;
                }
                return true;
            }
            e = e->next;
        } while (e != m_entry);
    }
    return false;
}
```

关于 `gdbarch` 结构体，现在只要知道它记录了架构信息即可，`register_size` 则返回某种架构中某个寄存器的大小。这个函数也没什么特别的，就是一个遍历操作。

接下来有一个稍微看起来复杂点但功能很简单的函数，也是这个类的最后一个函数：

```cpp
void pv_area::scan(void (*func)(void *closure, 
                                pv_t addr, 
                                CORE_ADDR size, 
                                pv_t value), void *closure) {
    struct area_entry *e = m_entry;
    pv_t addr;
    addr.kind = pvk_register;
    addr.reg = m_base_reg;
    if (e) {
        do {
            addr.k = e->offset;
            func(closure, addr, e->size, e->value);
            e = e->next;
        } while (e != m_entry);
    }
}
```

循环遍历整个表，对表中的每一项做一个自定义操作。函数指针使得整个函数看起来有些抽象，但也不难明白它的意思。

现在，我们已经获得了对一块内存区域的数据进行分析的工具，接下来，我们可以利用这些工具进行分析了。下面将针对两种架构的整个前导代码分析过程做出解释，在那里，我们可以看见这些工具都是怎样被应用的，又能给出怎样的结果。



# 一些类型的定义

代码：`gdbsupport/common-types.h`

```c++
typedef unsigned char gdb_byte;
typedef uint64_t CORE_ADDR;
typedef int64_t LONGEST;
typedef uint64_t ULONGEST;

#define CORE_ADDR_MAX (~(CORE_ADDR) 0)
#define ULONGEST_MAX (~(ULONGEST) 0)
```

这一部分定义的类型中，需要注意的是 `gdb_byte` 和 `CORE_ADDR` ，前者指来自于被调试程序的一个 byte ，后者指来自于被调试程序的一个地址。随后还定义了一个三态的逻辑变量：

```c++
enum tribool {
    TRIBOOL_UNKNOWN = -1,
    TRIBOOL_FALSE = 0,
    TRIBOOL_TRUE = 1
};
```

