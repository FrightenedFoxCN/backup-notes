# C Primer Plus 笔记

## C控制语句：循环

- C风格读取循环

  ```c
  status = scanf("%ld",&num);
  while (status == 1){
      /*循环行为*/
      status = scanf("%ld",&num);
  }
  //上述代码等价于
  while (scanf("%ld",&num) == 1){
      /*循环行为*/
  }
  ```

  scanf()函数具有两个特性：

  1. 若函数调用成功，将输入值存入num；
  2. 返回值为成功读入的输入值个数。

- while循环的通用形式：

  ```c
  while (expression)
      statement
  ```

  若expression为真，一直执行statement；当expression为假，跳过statement继续进行。被称为**入口条件循环**。

- 关系运算符用以比较浮点数时，尽量用严格不等式，舍入误差会引发问题。

- 一般而言，所有的非零值都被视为真。

- _Bool类型

  C99中的stdbool.h头文件使bool成为_Bool的别名，并定义true和false为0和1的符号常量，与C++兼容。

  可以进行如下赋值：

  ```c
  _Bool input_is_good;
  input_is_good = (scanf("%ld",&num) == 1);//这里从优先级上考虑，括号可以去掉
  ```

- 关系运算符的优先级分两组

  - 高优先级组：<，<=，>，>=
  - 低优先级组：==，!=

  结合方式均为从左到右。

- 不确定循环：预先不确定要执行多少次循环；

  计数循环：预先知道要执行多少次循环。

- 计数循环的行为：

  1. 必须初始化计数器；
  2. 计数器与有限的值作比较；
  3. 每次循环时递增计数器。

- for循环的通用形式：

  ```c
  for (initialization;test;update)
      statement
  ```

  先做判断，再做更新，例如

  ```c
  int i;
  for (i = 0;i <= 6; i++)
      printf("%5d %5d\n",i,i*i*i);
  printf("%d",i);
  /*输出为
      0     0
      1     1
      2     8
      3    27
      4    64
      5   125
      6   216
  7
  */
  ```

- 逗号运算符

  1. 多个语句占一个语句的位置；
  2. 多个语句从左往右执行；
  3. 逗号表达式的值是右侧项的值。

  例如：

  ```c
  houseprice = 249,500;//结果houseprice为249
  houseprice = (249,500);//结果houseprice为500
  ```

- 出口条件循环do while

  ```c
  do 
      statement
  while (expression);
  ```

- 数组

  ```c
  float debts[20];
  ```

  声明了debts这个含有20个元素的数组。

  **其中数组元素的编号从0开始，直到19。**

  注意：C编译器不会检查数组的下标是否正确！

  下例用for循环和数组计算了10个分数的总分、平均分和差点：

  ```c
  #include <stdio.h>
  #define SIZE 10
  
  int main(void){
      int index,score[SIZE];
      int sum = 0;
      float average;
      
      printf("Enter %d scores:\n",SIZE);
      for (index = 0; index < SIZE; index++)
          scanf("%d",&score[index]);
      printf("The score read in are as follows:\n");
      for (index = 0; index < SIZE; index++)
          printf("%5d",score[index]);
      printf("\n");
      
      for (index = 0; index < SIZE; index++)
          sum += score[index];
      average = (float) sum / SIZE;
      printf("Sum of scores = %d, average = %.2f\n",sum,average);
      
      return 0;
  }
  ```


## C控制语句：分支和跳转

- if语句和if else语句的结构

  ```c
  if (expression)
      statement
  else
      statement'
  ```

  注意，if else之间不能插入其他代码。

- getchar()和putchar()函数

  ```c
  ch = getchar();
  //该语句等价于
  scanf("%c",&ch);
  
  putchar(ch);
  //该语句等价于
  printf("%c",ch);
  ```

  由于这两个函数仅处理字符，他们比scanf()和printf()都要快，是定义于stdio.h中类似函数的预处理宏。

  同上一节讲到的读取循环，可以使用

  ```c
  ch = getchar(ch);
  while (ch != '\n'){
      /*处理字符*/
      ch = getchar(ch);
  }
  //与之功能相同地可以写成
  while ((ch = getchar) != '\n'){
      /*处理字符*/
  }
  ```

- ctype.h中的字符函数

  | 函数名     | 如果是下列参数时，返回值为真                                 |
  | ---------- | ------------------------------------------------------------ |
  | isalnum()  | 字母或数字                                                   |
  | isalpha()  | 字母                                                         |
  | isblank()  | 标准的空白字符（空格、水平制表符或换行符）或其他本地化指定为空白的字符 |
  | iscntrl()  | 控制字符（按住Ctrl键输入的）                                 |
  | isdight()  | 数字                                                         |
  | isgraph()  | 除空格之外的任意可打印字符                                   |
  | islower()  | 小写字母                                                     |
  | isupper()  | 大写字母                                                     |
  | isprint()  | 可打印字符                                                   |
  | ispunct()  | 标点符号（除空格或字母数字字符以外的任何可打印字符）         |
  | isxdigit() | 十六进制数字符                                               |
  | isspace()  | 空白字符（空格、换行符、换页符、回车符、垂直制表符、水平制表符或其他本地化定义的字符） |

  | 函数名    | 行为                                                   |
  | --------- | ------------------------------------------------------ |
  | tolower() | 如果参数是大写字符，返回小写字符；否则，返回原始参数。 |
  | toupper() | 如果参数是小写字符，返回大写字符；否则，返回原始参数。 |

- else if语句

  ```c
  if (expression1)
      statement1
  else if (expression2)
      statement2
  ...
  else (expressionn)
      statementn
  ```

  一串if else语句按一条语句处理，外层可以不加花括号。

- 逻辑运算符 &&与 ||或 !非

  在 iso646.h 中添加了备选拼写and/or/not。

  逻辑运算符保证从左往右运算，例如

  ```c
  ((c = getchar()) != ' ' && c != '\n')
  ```

  是合法且有效的。

  而且，一旦确定表达式值为真/假，停止往后运算，例如

  ```c
  (number != 0 && 12 / number == 2)
  ```

  不会出现浮点错误，因为若number\==0则不再计算12/number==2的值了。

- 示例：一个统计单词数的程序

  ```c
  #include <stdio.h>
  #include <ctype.h>
  #include <stdbool.h>
  #define STOP '|'
  int main(void){
      char c;
      char prev;
      long n_chars = 0L;
      int n_lines = 0;
      int n_words = 0;
      int p_lines = 0;
      bool inword = false;
      
      printf("Enter text to be analyzed (| to terminate):\n");
      prev = '\n';
      while ((c = getchar()) != STOP){
          n_chars++;
          if (c == '\n')
              n_lines++;
          if (!isspace(c) && !inword){
              inword = true;
              n_words++;
          }
          if (isspace(c) && inword)
              inword = false;
          prev = c;
      }
      
      if (prev != '\n')
          p_lines = 1;
      printf("characters = %ld,words = %d,lines = %d,",n_chars,n_words,n_lines);
      printf("partial lines = %d\n",p_lines);
      
      return 0;
  }
  ```

- 条件运算符 ? :

  ```c
  x = (y < 0) ? -y : y;
  //该语句等价于
  if (y < 0)
      x = -y;
  else x = y
  ```

  通用形式为：

  ```c
  expression1 ? expression2 : expression3
  ```

  若expression1为真，则整个表达式的值与expression2相同；否则，表达式的值与expression3相同。

- continue语句

  三种循环语句均可以使用continue。执行到该语句时，会跳过本次迭代的剩余部分，并开始下一轮的迭代。如果其在嵌套循环内，则只会影响包含之的内层循环。

- break语句

  终止包含它的循环，并进入下一阶段。

- switch语句

  ```c
  switch (ch){
      case 'a':
          statements;
          break;
      case 'b':
          ...
      default: defaultstatement;
  }
  ```

  对switch括号里的表达式求值，然后扫描标签，寻找匹配的值。若没有匹配，在有default标签的情况下转至该行，否则跳出switch语句。注意，如果没有break语句，则将持续向下运行每个标签里的语句。

  也可使用多重标签
  
  ```c
  case 'a':
  case 'A':statement
  ```
  
  是由于上述继续向下运行一特性带来的结果。
  
- goto语句（尽量避免！）

  ```c
  goto a;
  /*中间可以插入许多行语句*/
  a:statement
  ```

## 字符输入/输出和输入验证

- 缓冲区

  当运行如下程序时：

  ```c
  #include <stdio.h>
  int main(void){
      char ch;
      while((ch = getchar()) != '#')
          putchar(ch);
      return 0;
  }
  ```

  所形成的输出：

  ```c
  Hello, there.//用户输入
  Hello, there.//输出
      //以上为缓冲输入
  HHeelllloo,,  tthheerree..//输入和输出混杂在一起
      //以上为无缓冲输入
  ```

  缓冲输入过程中，输入的字符先被储存在缓冲区中，程序无法立刻使用这些字符。

  缓冲分为两类：完全缓冲I/O和行缓冲I/O。

  完全缓冲：当缓冲区被填满时才刷新；

  行缓冲：出现换行符是刷新缓冲区。

  ANSI C和后续的C标准都规定输入是缓冲的。

  若支持无缓冲输入，IBM PC兼容机在conio.h中提供了一系列特殊的函数，如getche()回显无缓冲输入和getch()无回显无缓冲输入。UNIX库中，ioctl()函数指定待输入的类型，然后用getchar()执行相应的操作。在ANSI C中，用setbuf()和setvbuf()函数控制缓冲。

- 文件的结尾

  CP/M，IBM-DOS和MS-DOS的文本文件曾经用Ctrl+Z字符来标记文件结尾；

  另一种方法是储存文件大小的信息。

  在C语言中，用getchar()检测到文件结尾是会返回一个特殊的值EOF，这个值被定义在stdio.h文件中，在一般的操作系统下被定义为-1；无论如何定义，EOF的值一定不会是输入字符产生的返回值。

  注意，使用EOF是，字符的定义应从char改为int，因为char类型不能储存负数值。

  键盘输入-1时，不能实现EOF的效果，因为它会被识别为两个字符。正确的方式是找到系统的要求。

- 命令行中输入和输出的重定向

  < 重定向输入 > 重定向输出 >>输出到文件末尾

- 更友好的用户界面：一个实例

  ```c
  //这是原始文件
  
  #include <stdio.h>
  
  int main(void){
      int guess = 1;
      printf("Pick a integer from 1 to 100. I'll try to guess ");
      printf("it.\nRespond with a y if my guess is right and with");
      printf("\nan n if it is wrong.\n");
      printf("Uh...is your number %d?\n",guess);
      while (getchar() != 'y')
        printf("Well, then, is it %d?\n",++guess);
      printf("I knew I could do it!");
      return 0;
  }//getchar()会读取换行符，故使用while丢弃输入行剩余内容
  
  #include <stdio.h>
  
  int main(void){
      int guess = 1;
      printf("Pick a integer from 1 to 100. I'll try to guess ");
      printf("it.\nRespond with a y if my guess is right and with");
      printf("\nan n if it is wrong.\n");
      printf("Uh...is your number %d?\n",guess);
      while (getchar() != 'y'){
          printf("Well, then, is it %d?\n",++guess);
          while (getchar() != \n)
              continue;
      }
      printf("I knew I could do it!");
      return 0;
  }//但是，这个程序会将y和n以外的所有输入默认为n
  
  #include <stdio.h>
  
  int main(void){
      int guess = 1;
      char response;
      printf("Pick a integer from 1 to 100. I'll try to guess ");
      printf("it.\nRespond with a y if my guess is right and with");
      printf("\nan n if it is wrong.\n");
      printf("Uh...is your number %d?\n",guess);
      while ((response = getchar()) != 'y'){
          if (response == 'n')
              printf("Well, then, is it %d?\n",++guess);
          else printf("Sorry, I understand only y or n.\n");
          while (getchar() != \n)
              continue;
      }
      printf("I knew I could do it!");
      return 0;
  }
  ```
  
- 混合字符和数值的输入，注意，scanf会跳过换行符，且将其留在输出队列中，而getchar()不会

- stdbool.h将_Bool替换为bool，可用true和false

## 函数

- 函数原型(prototype)，函数调用(call)，函数定义(definition)

- 函数原型指明函数的返回值类型和函数接受的参数类型，这些信息称为函数的签名(signature)

- 原型可以放在main函数前，也可以放在main函数顶端

- 函数可以放在分开的文件中，#include和#define也要跟上

- 形式参数(formal argument/parameter)是函数中的局部变量，为该函数私有，ANSI C要求在每个变量前加上类型

- 函数原型中也可直接用变量类型代表形参，此时变量事实上未被定义

- 实际参数(actual argument)是在函数调用过程中提供的形参的值

- 函数中的return语句将值返回给主调函数(calling function)

- 当返回值类型与声明的类型不同时，返回值发生强制类型转换

- 同时，return语句终止整个函数，使得其不再往下进行而回到主调函数

- 也可使用return;，此时不返回任何值而终止函数，在void函数中uiys

- 若函数定义放在首次调用之前，可以不加以声明

- 如果调用时的实参与形参类型不匹配，实参发生强制类型转换

- 递归

  ```c
  #include <stdio.h>
  void up_and_down(int);
  
  int main(void){
      up_and_down(1);
      return 0;
  }
  
  void up_and_down(int n){
      printf("Level %d: n location %p\n",n,&n);
      if (n < 4) up_and_down(n+1);
      printf("Level %d: n location %p\n",n,&n);
  }/*输出如下
  Level 1: n location 000000000065FE00
  Level 2: n location 000000000065FDD0
  Level 3: n location 000000000065FDA0
  Level 4: n location 000000000065FD70
  Level 4: n location 000000000065FD70
  Level 3: n location 000000000065FDA0
  Level 2: n location 000000000065FDD0
  Level 1: n location 000000000065FE00
  */
  ```

  每级递归的变量n都为此级递归私有

- 尾递归(tail recursion)指将递归调用置于函数末尾

- 递归用以倒序计算

  ```c
  #include <stdio.h>
  void to_binary(unsigned long n);
  
  int main(void){
      unsigned long number;
      printf("Enter an integer(q to quit):\n");
      while (scanf("%lu",&number) == 1){
          printf("Binary equivalent: ");
          to_binary(number);
          putchar('\n');
          printf("Enter an integer(q to quit):\n");
      }
      printf("Done.\n");
      return 0;
  }
  
  void to_binary(unsigned long n){
      int r;
      r = n % 2;
      if (n >= 2)
          to_binary(n / 2);
      putchar(r == 0 ? '0' : '1');
      return;
  }
  ```

- 递归会快速占用大量内存，可能导致程序崩溃

- &运算符返回变量的地址，使用%p打印地址

- 为了在一个函数中改变另一个函数中变量的值，必须使用指针

- *运算符(indirection operator / dereferencing operator)给出存储在某个地址下的值

- 指针的声明

  ```c
  int * pi //pi是指向一个int类型变量的指针
  ```

- 利用指针在函数之间通信

  ```c
  #include <stdio.h>
  void interchange(int * u, int * v);
  
  int main(void){
      int x = 5, y = 10;
      printf("Originally x = %d and y = %d.\n", x, y);
      interchange(&x, &y);
      printf("Now x = %d and y = %d\n", x, y);
      return 0;
  }
  
  void interchange(int * u, int * v){
      int temp;
      temp = *u;
      *u = *v;
      *v = temp;
      return;
  }
  ```

## 数组和指针

- 数组由数据类型相同的一系列元素组成

- 初始化：

  ```c
  int powers[8] = {1, 2, 3, 4, 5, 6, 7, 8};
  //ANSI C开始支持这种语法，不支持时可在声明前加static,即
  static int powers[8] = {1, 2, 3, 4, 5, 6, 7, 8};
  //也可使用const声明和初始化数组
  const int powers[8] = {1, 2, 3, 4, 5, 6, 7, 8};
  //在列表中元素个数少于数组元素个数时，剩余元素初始化为0，如
  int powers[8] = {1, 2, 3, 4, 5, 6} //则powers[6] = powers[7] = 0
  //如果多了，会被视为错误
  //C99增加了指定初始化器(designated initializer)
  int arr[6] = {[5] = 212}; //除末项外其余均为0
  int arr[6] = {[4] = 30, 31}; //第五项为30，第六项为31
  int arr[6] = {[4] = 30, 31, [1] = 12, 13}; //第五项为50，第六项为31；同时第二项为12，第三项为13
  //从左往右依序初始化，最后的将取代前面的赋值
  ```

- 不允许将一个数组作为单元赋给另一个数组

- 编译器不检查下标越界的问题，结果是UB

- 数组的数组：多维数组

  ```c
  int rain[5][12]; //初始化如下
  int rain[5][12] =
  {
      {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12},
      {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12},
      {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12},
      {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12},
      {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}
  };
  //在保证内部数据个数正确的前提下，可省略内层花括号
  ```

- 数组名是数组首元素的地址

- 指针 + 1指的是下一个元素的地址

- 指针表示法和数组表示法是等价的两种方法

- 函数中使用指针形参

  ```c
  int sum(int * ar, int n){ //或 int sum(int ar[], int n){
      int i;
      int total = 0;
      for (i = 0; i < n; i++)
          total += ar[i];
      return total;
  }
  ```

  上述函数给出数组中所有元素的和

- 使用指针算法完成上述任务：

  ```c
  int sump(int * start, int * end){ //其中start和end分别指向数组的始末元素
      int total = 0;
      while (start < end){
          total += *start;
          start++; //*和++优先级相同，为右结合
      }
      return total;
  }
  ```

- 给指针赋值时，地址应该和指针类型兼容

- 指针求差给出中间元素个数

- 注意，在用指针传递数据时，函数可以改变数据，ANSI C中可通过const防范这一点：

  ```c
  int sum(const int ar[], int n);
  ```

- const限定的指针不能改变其指向的值，但可以指向别处

- 多维数组和指针

  ```c
  zippo[2][1] == *(*(zippo + 2) + 1)
  ```

- 声明指向多维向量的指针时，只能省略最左边方括号的值，这一对方括号仅表明这是一个指针

- 变长数组(VLA)一经创建，其长度即不再可变，声明中，若省略形参名，用*表示维度，例

  ```c
  int sum2d(int rows, int cols, int ar[rows][cols]);
  //等价于
  int sum2d(int, int, int ar[*][*]);
  ```

- 复合字面量，即数组对应的常量为匿名，不可先声明再使用，必须即创建即使用

## 字符串和字符串函数

- 字符串字面量(string literal)为双引号括起来的内容，储存时编译器自动在最后加入\0

- 在字符串中，若要使用双引号，应使用\\"

- 字符串常量属于静态存储类别(static storage class)，只会被储存一次且在整个程序的生命期内存在

- 字符串表示该字符串所指向的地址，例

  ```c
  printf("%c",*"space");//输出为s
  ```

- 初始化字符数组时，所有未被使用的字符都被初始化为\0，无空字符不是字符串

- 数组和指针的字符串定义方法

  ```c
  const char * pt1 = "Hello world!";
  const char ar1[] = "Hello world!"
  ```

  其区别在于，ar1为地址常量，ar1不能更改，但其值可用于操作；数组的元素在未声明的情况下为变量。

  pt1为指针变量，可以指向其他地方；不能用其改变数组中元素的值，结果是未定义的。

  创建字符串数组时，指针数组效率更高，但是二维字符数组可修改。

  字符串的绝大多数操作都是利用指针来完成的。

- 字符串的输入

  必须首先为字符串分配足够的空间！

  gets()函数读取整行输入，丢弃换行符，储存其他字符，末尾加上\0。但是由于不安全性，会导致段错误

  fgets()函数有三个参数：

  - 第一个，指明读入字符的存储位置
  - 第二个，指明读入字符的最大数量（若碰到换行符终止，且将换行符存储在字符串中）
  - 第三个，指明要读入的文件，键盘输入使用stdin作为参数

  fgets()函数返回指向读入的字符串的指针，若读到末尾，返回空指针，记为0或者NULL，若遇到错误返回NULL

  gets_s()函数与fgets()函数类似但没有第三个参数

  scanf()函数以空白字符作为结束，而非以换行符作为结束

- 字符串的输出

  puts()在显示字符串的时候会自动在末尾添加一个换行符，到空字符停止输出

  fputs()函数类似，stdin改为stdout，不在输出中添加换行符

  printf()函数过程较慢，但能格式化更多的数据类型

- 字符串函数

  |   函数    |                             作用                             |
  | :-------: | :----------------------------------------------------------: |
  | strlen()  |                     用以统计字符串的长度                     |
  | strcat()  | 用以拼接字符串，以两个字符串作为参数，把第二个字符串的备份附加在第一个末尾，返回值为第一个参数 |
  | strncat() | 比strcat()多一个参数，最后一个参数表示复制字符的最大个数，遇到空字符若达到限制停止 |
  | strcmp()  | 用于比较两个字符串，若两者相等返回0，不相等返回非零值（具体值取决于实现） |
  | strncmp() |     比strcmp()多一个参数，只比较最后一个参数指定的字符数     |
  | strcpy()  | 第一个参数是目标字符串，第二个参数是源字符串，返回值为第一个参数的值，同时第一个参数未必是第一项 |
  | strncpy() |              多一个参数以指明可拷贝的最大字符数              |
  | sprintf() |     声明在stdio.h中，将数据写入字符串而非打印在显示器上      |
  | strchr()  | 第一个参数字符串，第二个参数字符；若字符串中包含此字符，则返回指向字符串首字母的指针，否则返回空指针 |
  | strpbrk() | 若第一个字符串中包含第二个字符串中的任意字符，返回指向第一个字符串首字符的指针，否则返回空指针 |
  | strrchr() | 第一个字符串，第二个字符；若字符串中包含此字符，则返回指向字符最后一次出现位置的指针，否则返回空指针 |
  | strstr()  | 返回指向第一个字符串中第二个字符串出现的首位置，若未找到，返回空指针 |
  | strlen()  |           返回字符串中中的字符数，不含结尾的空字符           |

- 一个字符串排序函数

  ```c
  #include <stdio.h>
  #include <string.h>
  #define SIZE 81
  #define LIM 20
  #define HALT ""
  void stsrt(char *strings[], int num);
  char * s_gets(char *st, int n);
  
  int main(void){
      char input[LIM][SIZE];
      char *ptstr[LIM];
      int ct = 0;
      
      printf("Input up to %d lines, and I will sort them.\n", LIM);
      printf("To stop, press the enter key at a line's stat.\n");
      while(ct < LIM && s_gets(input[ct], SIZE) != NULL && input[ct][0] != '\0'){
          ptstr[ct] = input[ct];
          ct++;
      }
      stsrt(ptstr, ct);
      puts("\nHere's the sorted list:\n");
      for (int k = 0; k < ct; k++)
          puts(ptstr[k]);
      
      return 0;
  }
  
  void stsrt(char *strings[], int num){
      char *temp;
      
      for (int top = 0; top < num - 1; top++)
          for (int seek = top + 1; seek < num; seek++)
              if (strcmp(strings[top], strings[seek]) > 0){
                  temp = strings[top];
                  strings[top] = strings[seek];
                  strings[seek] = temp;
              }
  }//选择排序算法(selection sort algorithm)
  
  char *s_gets(char *st, int n){
      char *ret_val;
      int i = 0;
      
      ret_val = fgets(st, n, stdin);
      if (ret_val){
          while (st[i] != '\n' && st[i] != '\0')
              i++;
          if (st[i] == '\n')
              st[i] = '\0';
          else
              while (getchar() != '\n')
                  continue;
      }
      return ret_val;
  }
  ```

## 存储类别、链接、内存管理

## 文件输入/输出

## 结构和其他数据形式

- 结构的声明(stucture declaration)

  ```c
  struct book{
      char title[MAXTITL];
      char author[MAXAUTL];
      float value;
  }
  ```

  其中的每一个部分被称为成员(member)或字段(field)

- 声明放在函数外部，则全局可用，函数内部则为此函数私有

- 结构变量的定义

  ```c
  struct book library;
  ```

  也可以定义相应的指针

  ```c
  struct book *ptbook;
  ```

  可以将结构的声明与定义合成一个步骤

  ```c
  struct book{
      char title[MAXTITL];
      char author[MAXAUTL];
      float value;
  } library;
  //甚至可以这样：
  struct{
      char title[MAXTITL];
      char author[MAXAUTL];
      float value;
  } library;
  ```

- 结构变量的初始化与数组的初始化类似

  ```c
  struct book library = {
      "The Pious Pirate and the Devious Dansel",
      "Renee Vivotte",
      1.95
  };
  //也可使用指定初始化器
  struct book library = {
      .author = "Renee Vivotte",
      1.95
  };
  //性质与数组类似
  ```

- 访问结构成员：结构成员运算符.

  library.value访问library的value部分，title，author和value相当于数组的下标

- .的优先级比&高

- 指向结构的指针后面的->与结构变量名后面的.的工作方式相同

- 可以使用嵌套结构

- 指向结构的指针：以一例说明：

  ```c
  #include <stdio.h>
  #define LEN 20
  
  struct names{
      char first[LEN];
      char last[LEN];
  };
  
  struct guy{
      struct names handle;
      char favfood[LEN];
      char job[LEN];
      float income;
  };
  
  int main(void){
      struct guy fellow[2] = {
          {
              {"Ewen", "Villard"},
              "grilled salmon",
              "personality coach",
              68112.00
          },
          {
              {"Rodney","Swillbelly"},
              "tripe",
              "tabloid editor",
              432400.00
          }
      };
      struct guy *him;
      printf("address #1: %p #2: %p\n", &fellow[0], &fellow[1]);
      him = &fellow[0];
      printf("pointer #1: %p #2: %p\n", him, him + 1);
      printf("him -> income is $%.2f: (*him).income is $%.2f\n", him -> income, (*him).income);
      him++;
      printf("him -> favfood is %s: him->handle.last is %s\n", him -> favfood, him->handle.last);
      return 0;
  }//下面是输出
  address #1: 000000000065FD70 #2: 000000000065FDC4
  pointer #1: 000000000065FD70 #2: 000000000065FDC4
  him -> income is $68112.00: (*him).income is $68112.00
  him -> favfood is tripe: him->handle.last is Swillbelly
  ```

- 函数调用结构用指针更加便捷，直接传递结构时，函数调用的是原始结构的一个副本

- C允许将一个结构赋值给另一个结构

- 函数的返回值也可以是一个结构

- 复合字面量，类似于强制类型转换

- 

## 位操作

## C预处理器和C库

## 高级数据表示