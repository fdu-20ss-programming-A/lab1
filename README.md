# Lab 1

> 本次lab目标：
>
> 1. 熟悉开发环境和调试环境
> 2. 学习C语言中的加减乘除运算
> 3. 学习定义宏常量
> 4. 使用编程解决实际问题



## 获取及提交lab

**获取**：通过 `https://github.com/fdu-20ss-programming-A/lab1`或者`超星平台`获取。

**提交**：将提交物放到lab1的文件夹中，将文件夹压缩，压缩文件名应为你的 `学号_姓名` （如`20302010000_小明`），提交压缩文件至超星学习通对应的作业中。

**提交物**：本次lab需要提交源代码文件（.c文件即可），以及一份lab文档。文档需要包含每题执行的测试数据以及结果（截图即可）。

**截止时间**：2020年9月27日 23:59:59



## 1. lab0回顾

> LAB0我们进行了环境配置以及学习在命令行中运行C程序。这里我们总结几个lab中出现的问题，希望同学之后的作业和LAB注意。

+ **文档的重要性**

  课程LAB通常以文档的形式发布，我们会将LAB的学习内容、LAB学习目标以及LAB作业的提交方式直接在文档表述，所以我们希望同学们完成LAB前先将LAB文档阅读一遍。LAB文档通常会发布在超星平台以及[Github的LAB仓库](https://github.com/fdu-20ss-programming-A)。我们推荐同学们使用Github仓库的文档，因为文档可能会有局部的调整和更新，Github仓库能够保证文档是最新的版本。

+ **学会如何自己解决问题**

  同学们在编程过程中难免会碰上一些问题，学会自己寻找问题的解决方法也是编程的必经之路。一旦遇到问题我们**强烈建议**同学们先利用网络资源寻找解决方案。一般错误都会出现错误提示信息，同学们只需要将出现的问题在搜索引擎中搜索便能寻找到各种解决方案。

+ **如何向助教求助**

  TA的工作就是帮助同学解决课程方面的问题，所以我们欢迎同学们向TA询问关于课程内容的问题。但是我们也希望能够比较高效地帮助同学，所以我们建议同学们提问时能够将问题描述地**尽可能的详细**，最好能够提供出现问题的截图，方便助教定位问题。我们也建议同学尽可能在课程大群提问，方便其他遇到类似问题的同学进行参考。

+ **开发环境问题**

  很多同学提问关于开发环境的问题，这里我们再明确一下。Code::Blocks是课程推荐的开发环境，原因是课程视频中会使用Code::Blocks进行编程学习以及代码调试。我们非常建议同学们跟着课程视频一步一步操作，所以我们认为没有软件或者硬件的问题最好都能安装Code::Blocks。

  课后作业以及LAB作业的编码环境，我们并不作要求，同学们可以直接使用自己熟悉的dev-c++或者助教推荐的Clion或者Code::Blocks。编程环境只是其次的，我们更希望同学们关注课程知识的学习！



## 2. C语言的输入与输出

> 在之前的作业中，我们已经碰到 printf 函数和 scanf 函数，它们是我们进行输入输出最重要的调用函数。在LAB1 的作业中我们会频繁使用这两个函数，所以在这里我们介绍一下这两个函数的用法，顺便推荐几个C语言库函数的查询网站方便同学以后查询其他库函数。

### printf函数

printf函数的调用格式为：

```
printf("<格式化字符串>", <参量表>);
```

`<格式化字符串>`为将被输出的字符串模板，字符串内部可以插入类似`%d`,`%f`的变量占位符。占位符在输出时将被替换为`<参量表>`内对应的变量。需要注意，有几个占位符就需要几个传入参数。例如：

```c
int main(){
    int a = 0, b = 1;
    float c = 1.5;
    printf("a=%d,b=%d,c=%f\n",a,b,c);
    return 0;
}
```

上面的程序将输出`a=0,b=1,c=1.500000`。

占位符支持的格式为`%[标记][字符串总长度][.浮点数精度][格式字符长度]格式字符`，下面介绍基本用法。

`格式字符`需要与传入的参数类型保持一致，下面是常见类型参数：

| 格式字符 | 意义                                       |
| :------- | :----------------------------------------- |
| d        | 以十进制形式输出带符号整数(正数不输出符号) |
| u        | 以十进制形式输出无符号整数                 |
| f        | 以小数形式输出单、双精度实数               |
| c        | 输出单个字符                               |
| s        | 输出字符串                                 |
| p        | 输出指针地址                               |

`标记`支持为字符串的输出时改变输出格式。例如，使用`-`将字符串左对齐（默认右对齐），使用`+`输出变量的符号。

`字符串总长度`指定变量的最小长度，如果变量小于这个值，将用空格填充。

`浮点数精度`指定输出浮点数的精度，如果输入小于精度，将以0填充，默认小数输出时的精度为6。

下面的程序指定浮点数a输出精度为3：

```c
int main(){
    float a = 1.23456f;
    printf("a=%.3f\n",a);/* 这里将打印a=1.235 */
    return 0;
}
```

同学们如果想更加深入了解`printf`函数，请查阅[这里](https://www.runoob.com/cprogramming/c-function-printf.html)。



### scanf函数

C语言中我们经常使用 `scanf` 接收控制台的输入。

 `scanf`  的调用格式为：

```c
scanf("<格式化字符串>", <参量表>);
```

与 `printf` 的区别为  `scanf` 传入的参数为变量的指针。现在我们不需要大家了解指针的概念，这里解释一下使用指针的原因。`scanf` 需要修改变量的值为输入的值，所以需要传入指针而不是变量的值。所以请大家明确：`&varible != varible` 。

接下来举一个例子：

```c
int main(){
    int a;
    float b;
    scanf("%d %f",&a,&b);/* 中间的分隔符可以自由使用，一般用空格 */
    printf("a=%d, b=%.2f\n",a,b);
    return 0;
}
```

同学们如果想深入了解`scanf`的用法，请参考[这里](https://www.runoob.com/cprogramming/c-function-scanf.html)。



### 参考链接

+ [菜鸟教程--C标准库](https://www.runoob.com/cprogramming/c-standard-library-stdio-h.html)
+ [Linux库函数手册](https://linux.die.net/man/)



## 3.  宏常量

在C语言中我们经常需要定义一些常量方便代码中多处调用。

`#define` 是预处理指令，语法为：

```C
#define 标识符 字符串
```

"`#`" 表示这是一条预处理命令。凡是以“`#`”开头的均为预处理命令。“define”为宏定义命令。“标识符”为所定义的宏名。“字符串”可以是常数、表达式、格式串等。注意预处理语句结尾**没有分号**!

例如，可以在程序定义一些常量方便使用：

```c
/* include也是预处理指令 */
#include <stdio.h> 
/* 定义一个浮点常数 */
#define PI 3.14 
/* 定义一个整型常量 */
#define ARRAY_LENGTH 10
/* 定义一个字符串常量 */
#define STRING "hello"

int main(){
    int a = ARRAY_LENGTH;
    float b = PI;
    char *str = STRING;
    printf("a=%d, b=%.2f, str=%s\n", a, b, str);
    return 0;
}
```



## 4. 寻找程序bug

> 接下来我们用一个例子帮助大家学习如何调试程序。

```c
#include <stdio.h>

int main(){
    char input[6];
    int i;
    for(i = 0; i < 5; i++){
        input[i] = getchar();/* getchar()从命令行获取一个输入的字符 */
    }
    for(i = 0; i < 5; i++){
        printf("%c",input[i]);
    }
    return 0;
}
```

上面的程序从控制台获取5个字符，并按照顺序打印。

接下来我们尝试设计一个测试数据：

```
测试数据：
a
b
c
d
e
预期的结果：
abcde
```

但是当我们使用测试数据的时候，问题出现了：

```
运行结果：
a
b
c
a
b
c

...Program finished with exit code 0         
Press ENTER to exit console.
```

我们还没输入结束程序就结束了，那么问题在哪呢？



## 5. LAB1上机作业

> 上机作业要求每题单独写在XXX.c文件中。

### Question 1

题目

>输入三角形的底和高，输出三角形的面积。

限制

>底和高均为整数，面积保留两位小数。

示例

> 请输入三角形的底和高：10,5
>
> 三角形的面积为：25.00

### Question 2

题目

> 输入等差数列的首项、等差和总项数，输出等差数列的和

限制

> 首项，等差和总项数均为整数

示例

> 请输入等差数列的首项：1
>
> 请输入等差数列的等差：2
>
> 请输入等差数列的总项数：3
>
> 等差数列的和为：9

### Question 3

题目

> 输入圆的半径，求圆的周长和面积。要求定义以下宏常量：
>
> #define PI 3.14159

限制

> 输出保留2位小数

示例

> 请输入圆的半径：1
>
> 圆的周长为6.28，圆的面积为3.14

### Question 4

题目

> 输入三个整数，输出三个整数的和，乘积与平均数。

限制

> 平均数保留两位小数

示例

> 请输入三个整数：1,2,3
>
> 三个整数的和为6，乘积为6，平均数为2.00

### Question 5

题目

> 温度转换：键盘读入华氏温度，输出摄氏温度。

限制

> 输入华氏温度为浮点数，输出摄氏温度保留两位小数

提示

> 华氏温度 = (9/5) * 摄氏温度 + 32

示例

> 请输入华氏温度：32.0
>
> 摄氏温度为0.00