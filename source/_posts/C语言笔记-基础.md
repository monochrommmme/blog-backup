---
title: C语言笔记-基础
date: 2024-04-27 19:37:54
categories: 
 - 学习笔记
tags:
 - C语言
 - 笔记
 - 应试
---

c语言学习笔记，内容很基础，因为完全是应对考试用所以既斤斤计较，又一点也不深入。

<!-- more -->

*部分图片来自网课，水印存在本人信息，所以进行了一定程度的打码，用于学习，侵删。*

### 前置

[c语言vscode环境配置](https://zhuanlan.zhihu.com/p/354400717)
[修改cmd控制台默认代码页编码的几种方法【GBK、UTF-8】](https://blog.csdn.net/qq_39621009/article/details/122817826)`utf-8:chcp 65001;gbk:chcp 936`

资料：
[C 语言教程 - 网道](https://wangdoc.com/clang/)

### 构成

标识符命名规范
![](../images/C语言笔记-基础/17118702744255.jpg)

常量和变量
![](../images/C语言笔记-基础/17118723671242.jpg)

![](../images/C语言笔记-基础/17118727532367.jpg)

输入输出

```c
#include <stdio.h>/*引用头文件stdio.h；std即standard；
io指输入输出；
.h代表这是头文件；
所有#开头的行表示预编译指令，结尾没有分号*/
void main()
{
    printf("今天是2024年2月17日!\n");
}/*大括号内部叫代码块，可执行语句必须在代码块里面；
void是变量名，不需要返回数据；main(){}指唯一的主函数；
这里使用了头文件中的print()函数*/
```

```c
#include <stdio.h>
int main()
{
int a,b,sum;//声明语句，和下方执行语句两者形成一个函数体
scanf("%d%d",&a,&b);/*输入两个值赋予a和b；
输入时可以用空格隔开后enter，也可以分别输入再enter；
&是取地址符，每个变量都存在指向其内存的地址*/
printf("a = %d,b= %d\n",a,b);//%d套用“,”后的int数据值
sum=a+b;
printf("sum = %d\n",sum);//%d套用“,”后的数据值
return 0;//返回数据“0”
}
```
返回数据和自定义函数

```c
#include <stdio.h>
int max(int x,int y)
{
    int z;
    if(x > y){
        z = x;
    }else{
        z = y;
    }
    return z;
}//自定义的max函数，处理对象是x,y，结果值为z

int main()
{
    int a,b,c;
    scanf("%d%d",&a,&b);
    printf("第一个数为%d\n",a);
    printf("第二个数为%d\n",b);
    c=max(a,b);//输入两个数据，将a和b交给max函数处理，给c赋予max结果返回值
    printf("更大的数是%d\n",c);
    return 0;
}
```
也可以将自定义的max函数作为头文件单独保存和调用。
```c
//举例max.h和main.c在相同目录下时，max.h的内容：
int max(int x,int y)
{
    int z;
    if(x > y){
        z = x;
    }else{
        z = y;
    }
    return z;
}
```
```c
//main.c内容是：
#include <stdio.h>
#include "./max.h"//"./"省略也没关系；如果max.h放在头文件夹中也能用尖括号
int main()
{
    int a,b,c;
    scanf("%d%d",&a,&b);
    printf("第一个数为%d\n",a);
    printf("第二个数为%d\n",b);
    c=max(a,b);
    printf("更大的数是%d\n",c);
    return 0;
}
//这样结果是一样的
```

### 数据类型和计算

![](../images/C语言笔记-基础/17118731678856.jpg)

![](../images/C语言笔记-基础/2A14B73E7A86EDD76385BA6F2197542B.png)
*这里的字符串是个类，c语言没有这种数据。数据在双引号内*
补充：
%p：指针；%%：输出一个百分号；%u：无符号整数（unsigned int）；%hd：十进制 short int 类型；%g：6个有效数字的浮点数。整数部分一旦超过6位，就会自动转为科学计数法，指数部分的e为小写；%G：等同于%g，唯一的区别是指数部分的E为大写。

![](../images/C语言笔记-基础/17118754488079.jpg)

![](../images/C语言笔记-基础/17118766210475.jpg)
*（以上适用于windows）*

signed和unsigned
![](../images/C语言笔记-基础/0AF722CC3186BB7EBCD7733CD0197E72.png)

![](../images/C语言笔记-基础/17118770565485.jpg)
*char类型本质上就是个整型。存放的其实是个对应字符的ASCII码，所以前面就算有unsigned也不会报错*
[什么是ASCII码，ASCII码值的大小顺序是怎么样 - 知乎](https://zhuanlan.zhihu.com/p/579787917)
常见ASCII码的大小规则：0-9<A-Z<a-z。
几个常见字母的ASCII码大小： “A”为65；“a”为97；“0”为 48。
```c
char c = 'a';
printf("%d",a-32);//A
char c1 ='abc';
    printf("%c",c1);//c 取最后的一个字符
```

```c
char a = 'B'; // 等同于 char a = 66;
char b = 'C'; // 等同于 char b = 67;

printf("%d\n", a + b); // 输出 133
```
![](../images/C语言笔记-基础/A9559D695785D2E6950D0B553F76ABBA.png)
*这四种赋值都是等价的*

![](../images/C语言笔记-基础/CEA017C2609971B96FBB8E6F2AE5B049.png)
```c
printf("%d",1/3);//结果为0
printf("%lf",1/3);//结果为0.000...
/*原因是c语言中整型除以整型还是整型，
1/3结果为0，然后转型成double类型*/
printf("%f",1.0/3)//结果为0.333333...
```

自动类型转换：大的变成小的

强制类型转换：
![](../images/C语言笔记-基础/31D4413C47686EA1A3909A69A91B5D53.png)
```c
int temp = 3.99f;
printf("%d\n",temp);//3
printf("%f\n",temp);//0.000000
printf("%lf\n",(double)6/3);//2.000000
printf("%f\n",(float)temp);//3.000000
```

![](../images/C语言笔记-基础/1E1E030CB2D22BB04692EFF0D9C086CA.png)
![](../images/C语言笔记-基础/6E496766FB83D612DB0C34977DAF3583.png)
![](../images/C语言笔记-基础/4165D512A8486301EAD368EF0028EC54.png)

sizeof函数
sizeof是 C 语言提供的一个运算符，返回某种数据类型或某个值占用的字节数量。它的参数可以是数据类型的关键字，也可以是变量名或某个具体的值。
```c
printf("%u",sizeof(float));//4
printf("%zd",sizeof(double));//8

int x = sizeof(int);// 参数为数据类型

int i;// 参数为变量
sizeof(i);

sizeof(3.14);// 参数为数值
```
![](../images/C语言笔记-基础/0C708102E2D6DB29A57BD32F1D9EB190.png)

算数运算符
![](../images/C语言笔记-基础/FC5DC4F496DC6661C71A0600F0B0CA08.png)
```c
int a = 1;
int b = 2;
++a+b;//a=2,b=2
a+++b;//a=3,b=2
//不存在共用
```

赋值运算符
![](../images/C语言笔记-基础/2F14D68CBFA03D6DC36749309B98242F.png)

比较运算符/关系运算符
1为真0为假。没有java的布尔类型。
![](../images/C语言笔记-基础/AE2370D76DB7568E9A954CF5B713EFDD.png)

逻辑运算符
![](../images/C语言笔记-基础/C543BCD3BE601DDC39FE44263243B1D6.png)

### 基本语句
if-else语句
```c
#include <stdio.h>

int main()
{
    printf("输入你的成绩\n");
    double score;
    scanf("%lf", &score);

    if (score >= 0 && score < 60)//括号中是条件语句
    {
        printf("成绩不合格\n");
    }
    else if (score >= 60 && score <= 100)
    {
        printf("成绩合格\n");
    }
    else
    {
        printf("输入数据有误\n");
    }
    //()内判断真假，真执行{}语句，假执行else后语句
    return 0;
}
```

switch语句
![](../images/C语言笔记-基础/F99BF1698ED7327F29F618A5A526307B.png)
```c
#include <stdio.h>

void main()
{
    char grade;
    scanf("%c",&grade);
    switch(grade)//得是整型（char类型也算）
    {
        case 'A':
        printf("优秀");
        break;//break表示中断，不继续这个代码块的运行
        case 'B':
        printf("良好");
        break;
        case 'C':
        printf("及格");
        break;
        case 'D':
        printf("不及格");
        break;

        default://输入表达式和任意case表达式不符时运行默认内容
        printf("输入数据有误");
        break;
    }
}
```

for循环
![](../images/C语言笔记-基础/84CA10022989C6D5F63CFFB3A68C04AF.png)
```c
/*计算1到100之和*/
#include <stdio.h>

void main()
{
    int num = 0;
    for(int i = 1;i <= 100;i++)
    {
        num = num + i;
        printf("i=%d\n",i);
        /*可以看出循环执行了100次
        但i的最终值是101，因为最后循环执行之后还会自增；
        循环中赋值的i只在循环中有效*/
    }
    printf("结果是%d",num);
}

```

while循环

```c
#include <stdio.h>
//同样可以计算1~100的和
void main()
{
    int sum = 0;
    int i = 100;
    while(i >= 0)
    {
        sum += i;
        i--;
    }
    printf("sum等于%d",sum);
}
//sum等于5050
```

do-while循环
```c
//和while循环的区别是无论如何先运行一次执行语句
#include <stdio.h>
void main()
{
    int i = 10;
    do {
        i--;
    } while(i > 10);

    printf("i等于%d",i);
}
//i等于9
```

练习：控制台输出乘法口诀表
```c
#include <stdio.h>

int main()
{   
    for(int y = 1;y <= 9;y++)
    {
        for(int x = 1;x <= y;x++)
        {
            printf("%d*%d=%d ",x,y,x*y);
        }

        if(y < 9)
        {
            printf("\n");
        }//为防止最后输出多余的一行，单拎出来输出
    }
    return 0;
}
/*
1*1=1 
1*2=2 2*2=4 
1*3=3 2*3=6 3*3=9 
1*4=4 2*4=8 3*4=12 4*4=16 
1*5=5 2*5=10 3*5=15 4*5=20 5*5=25 
1*6=6 2*6=12 3*6=18 4*6=24 5*6=30 6*6=36 
1*7=7 2*7=14 3*7=21 4*7=28 5*7=35 6*7=42 7*7=49 
1*8=8 2*8=16 3*8=24 4*8=32 5*8=40 6*8=48 7*8=56 8*8=64 
1*9=9 2*9=18 3*9=27 4*9=36 5*9=45 6*9=54 7*9=63 8*9=72 9*9=81 
*/
```

continue语句
用于在循环体内部终止本轮循环，进入下一轮循环

```c
#include <stdio.h>

void main()
{
    for(int i = 1;i <= 10;i++)
    {
        if(i % 3 == 0)
        {
            continue;
        }
        printf("%d不是1~10之间的3的倍数\n",i);
    }
}
```

break语句
在switch语句中时,作用是跳出switch结构，执行之后的代码；
在循环语句中，作用是跳出当前内循环语句，执行之后的代码

```c
//计算2到100之间的质数之和
#include <stdio.h>

int main()
{
    int num = 0; // 初始化质数之和
    for (int i = 2; i <= 100;i++) // 遍历2到100之间的数字
    {
        int is_prime = 1; // 假设当前数字是质数
        for (int j = 2; j < i; j++) // 检查当前数字是否能被较小的数字整除
        {
            if (i % j == 0)
            {
                is_prime = 0; // 如果能整除，标记为非质数
                break; // 不需要继续检查，提高效率
            }
        }
        if (is_prime)
        {
            printf("%d是质数\n",i);// 打印每个质数
            num = num + i; // 将质数添加到总和中
        }
    }
    printf("2到100之间的质数之和为：%d\n", num); // 打印质数的总和
    return 0;
}
```

*goto语句
用于跳到指定的标签名。会破坏结构化编程，建议不要轻易使用。也可以用于跳出某个循环*
```c
#include <stdio.h>

void main()
{
    infinite_loop://标签名
  printf("Hello, world!\n");
  goto infinite_loop;
}
//结果为Hello,world\n的无限循环
```
### 指针

指针是一个值，这个值代表有一个内存地址，因此指针相当于指向某内存地址的路标。通过指针，可以简化一些 C 编程任务的执行，还有一些任务，如动态内存分配

字符`*`表示指针，通常跟在类型关键字的后面，表示指针指向的是什么类型的值。比如`char*`表示一个指向字符的指针。

```c
int* intPtr;
int * intPtr;
int  *intPtr;
//等效
```
```c
//同时声明两个指针时
// 正确
int * foo, * bar;
// 错误，结果成了foo是整型指针变量，bar是整型变量
int* foo, bar;
```

每一个变量都有一个内存位置，每一个内存位置都定义了可使用`&`运算符访问的地址，它表示了在内存中的一个地址
```c
#include <stdio.h>
 
int main ()
{
    int var_runoob = 10;
    int *p;
    p = &var_runoob;
 
   printf("var_runoob 变量的地址： %p\n", p);
   printf("var_runoob 变量的地址： %p\n",&var_runoob);//等效
   return 0;
}
/*
var_runoob 变量的地址： 000000000061FE14
var_runoob 变量的地址： 000000000061FE14
*/
```
![](../images/C语言笔记-基础/7E9766D228CA4785CC79D3A531230940.png)

使用指针时会频繁进行以下几个操作：定义一个指针变量、把变量地址赋值给指针、访问指针变量中可用地址的值。这些是通过使用一元运算符 * 来返回位于操作数所指定地址的变量的值
```c
#include <stdio.h>
 
int main ()
{
   int  var = 20;   /* 实际变量的声明 */
   int* ip;        /* 指针变量的声明 */
 
   ip = &var;  /* 在指针变量中存储 var 的地址 */
 
   printf("var 变量的地址: %p\n", &var  );
 
   /* 在指针变量中存储的地址 */
   printf("ip 变量存储的地址: %p\n", ip );
 
   /* 使用指针访问值 */
   printf("*ip 变量的值: %d\n", *ip );
 
   return 0;
}
/*
var 变量的地址: 000000000061FE14
ip 变量存储的地址: 000000000061FE14
*ip 变量的值: 20
*/
```

![](../images/C语言笔记-基础/956ED3608F9B808DA80778B425D3E987.png)

空指针/NULL指针在C语言中是一个常量，表示地址为0的内存空间，这个地址是无法使用的，读写该地址会报错
```c
#include <stdio.h>
 
int main ()
{
   int  *ptr = NULL;
 
   printf("ptr 的地址是 %p\n", ptr  );
 
   return 0;
}
//ptr 的地址是 0000000000000000
```

![](../images/C语言笔记-基础/DCA01E1CBE790AEB81279ACB34F07361.png)
![](../images/C语言笔记-基础/1FA44ED7B476D0FC45A5B56A97A3A5E5.png)
![](../images/C语言笔记-基础/AB1F434B11FB843D0A2928A80D7B5E87.png)

### 函数


### 数组

![](../images/C语言笔记-基础/40DA60536120D13643EADB167ADA85FE.png)
![](../images/C语言笔记-基础/BA886C8023AF2276A4B62FBDE92553F1.png)
![](../images/C语言笔记-基础/05089E0CBB1EA7C3FEBA6FCC6708ADD6.png)
```c
//定义数组
int a[10];//数据类型
char arr[10][9][8];//三维数组
struct Stu boy[10];//构造类型（不在转本考纲范围内）
```

一维数组的初始化
在定义数组的同时进行赋值被称为初始化。全局数组若不进行初始化，编译器将其初始化为0
![](../images/C语言笔记-基础/23A37AA462099A742E2E4E4B26265F58.png)
![](../images/C语言笔记-基础/26DDF9CFD44A73E29B3F8D8C1967036B.png)

数组元素的引用
数组名是一个地址的**常量**，代表数组中首个元素的地址
```c
#include <stdio.h>
void main()
{
  int arr[5] = {1,2,3,4,5};
  printf("arr = %p\n",arr);//arr = 000000000061FE00
  printf("&arr[0] = %p\n",&arr[0]);//&arr[0] = 000000000061FE00
  printf("&arr = %p\n",&arr);//&arr = 000000000061FE00
}//这些十六进制数都是内存地址
```

![](../images/C语言笔记-基础/17132621478849.jpg)

二维数组和多维数组
![](../images/C语言笔记-基础/B56B473FEAEC60D00AB085DBEDB09C53.png)
![](../images/C语言笔记-基础/99BCB14A950CF5A3F15512DE0FFEFD94.png)

char数组
![](../images/C语言笔记-基础/194652735B8E074DB4C9CAF9557D6B74.png)
![](../images/C语言笔记-基础/57ADB8BD34225C3EA28EA76C9B74A225.png)
![](../images/C语言笔记-基础/FC4AD7FFFE05C2651F01D37B3C986DA3.png)

### *排序二分法及递归算法*




