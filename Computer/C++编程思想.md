# C++编程思想

## 第二章 对象的创建和使用

### 语言的翻译过程

- 解释器：将源代码转化成一些动作并立即执行之

  - 优点：较好的交互性、适于快速程序开发
  - 缺点：内存空间的限制、调试困难

- 编译器：直接把源代码转化成汇编语言或机器指令

  - 预处理器：节省输入、增加代码的可读性

  - 语法分析：把源代码分解成小的单元并把他们按树形结构组织起来

    - 静态类型检查：检查函数参数是否正确使用

  - 全局优化器（可能）：生成更短、更快的代码

  - 代码生成器：将树的每个节点转化为汇编代码或机器代码

    生成的如果是汇编代码，还需要使用汇编器对其进行汇编

  - 窥孔优化器（可能）：查找冗余汇编模块

  - 连接器：将一组目标模块连接成可执行程序

    - 库管理器：创建和维护库

### 分段编译工具

- 函数：传入参数，得出返回值

- 声明（declaration）和定义（definition）

  - 声明：向编译器介绍标识符（函数或变量长什么样）

    - 函数声明：给函数取名，可以给函数参数命名，编译器会忽略它

      注：`int func()`在c语言中表示可带任意参数的函数，在c++中表示不带任何参数的函数

    - 变量声明：`extern`关键字（也可用于函数的声明）

  - 定义：在这里建立变量或函数，为他们分配存储空间

    - 函数定义：带花括号的函数体

      如果要在其中使用参数，函数定义中的参数必须有名字

    - 变量定义：不加`extern`时，声明即定义

- 头文件：两种类型

  - `#include <iostream>`以特定的方式寻找文件

  - `#include "local.h"`以实现定义的方式寻找文件

  - `#include <iostream.h>`等价于

    ```c++
    #include <iostream>
    using namespace std;
    ```

- 连接过程

  - 连接器会将库中包含所需定义的目标模块加入连接
  - 同时秘密连接启动模块（初始化例程）等模块

### `iostream`类和`std`名称空间

- 标准输出：发送输出的通用场所

  ```c++
  cout << "Helloworld!";
  ```

  `cout`是一个对象，它接受所有与标准输出绑定的数据；和`iostream`对象连用，`<<`的含义是发送到

- 名字空间（名称空间）

  `namespace`关键字表示名称空间，要使用某名称空间，使用`using`关键字，所有c++标准库函数在`std`名称空间中，不含`.h`的头文件往往包含名称空间，需要显式附加`using`指令

- `endl`函数表示一行结束并在行末加上一个换行符，例：

  ```c++
  cout << "Helloworld" << endl;
  ```

- 显式类型转换(cast)

  ```c++
  char(27)
  ```

- 多种进制的输出

  ```c++
  cout << "In decimal:" << dec << 15 << endl;
  cout << "In octal:" << oct << 15 << endl;
  cout << "In hex:" << hex << 15 << endl;
  ```

- 字符数组的拼接：预处理过程

  ```c++
  cout << "This is far too long to put "
      "in a single line but it can be broken "
      "up with no ill effects as long as "
      "there is no punctuation separating "
      "adjacent character arrays." << endl;
  ```

- 标准输入：控制台输入`cin`

  与`cout`类似，用于与`cin`一起使用的输入输出流操作符为`>>`，例如：

  ```c++
  cin >> number;
  ```

- `system`函数：兼容命令行

  在`cstdlib`文件中声明，例如：`system("cls");`

### `string`类

需要`#include <string>`才能使用`string`类，其使用相当直观，且具有动态特性，无需考虑其内存分配：

```c++
string s1, s2; //空字符串
string s3 = "Helloworld!"; //初始化方法1
string s4("I am"); //初始化方法2
cin >> s1; //输入
s2 = "today"; //赋值
s1 = s3 + " " + s4; //连接
s1 += " 8 "; //后接
cout << s1 + s2 + "!" << endl; //输出
```

### 文件的读写与`fstream`

- `fstream`会自动包含`iostream`，但是如果使用了`cin`和`cout`，最好还是显式包含`iostream`
- 为了读取而打开文件，需要创建一个`ifstream`对象，其用法和`cin`相同
- 为了写而打开文件，需要创建一个`ofstream`对象，其用法和`cout`相同
- `getline`是`iostream`库中的函数，其第一个参数是`ifstream`对象，第二个参数是`string`对象，读取文件中的一行内容并把它放进`string`对象中，同时丢弃换行符

```c++
ifstream in("input.txt");
ofstream out("output.txt");
string temp;
while (getline(in, temp)){
    out << temp << "\n";
}
```

### `vector`标准容器类

- 要使用`vector`，需要`#include <vector>`
- 表示一个装`type`类型的`vector`，创建为`vector<string>`
- 为了在`vector`中追加新元素，需要使用成员函数`push_back()`将其加至`vector`末尾
- 可以使用下标访问`vector`的一个单元，使用`size()`给出`vector`中的元素个数

```c++
vector<string> v;
ifstream in("input.txt");
string temp;
while (getline(in, temp)){
    v.push_back(temp);
}
for (int i = 0; i < v.size(); i++){
    cout << i << ": " << v[i] << endl;
}
```

- 使用`>>`操作符时，得到的不再是一行而是一个单词，使用`while (in >> temp)`构成循环
- 也可以使用下标对`vector`中的一个单元赋值

## 第三章 C++中的C

