## 欲穷千里目之路

> 在今天的内容介绍之前我们要知道：C语言中，由一个分号（ ; ）隔开的就是一条语句。
>
> 很好理解，如：

```c
int a=3;//语句1

printf("请大家多多指教！");//语句2

;//语句3----空语句
```

> 今天讲解的内容，则是自己对于这三种语句一些细节的介绍。（**并不是具体讲解这些语句**）
>
> 分支语句：if，switch
>
> 循环语句：while，for，do while
>
> goto语句



## 补充小知识（后面如果遇见，可在此了解）

> 1. C语言中：0  表示假--------非0  表示真，如：1，2，-1
>
> 2. EOF： EOF是一个计算机术语，为End Of File的缩写（文件结束标志），其值为-1。通常在文本的最后存在此字符表示资料结束。
>
> 3. getchar()：(来源于MSDN，大家可以自己翻译一下哦  \\(^  ^)/ )
>
>    - Read a character from a stream (**getc**, **getwc**), or get a  character from **stdin** (**getchar**, **getwchar**).
>
>    - **Return Value**
>
>      Each of these functions returns the character read. To indicate an read error  or end-of-file condition, **getc** and **getchar** return **EOF**. For **getc** and  **getchar**, use **ferror** or **feof** to check for an error or for  end of file.（个人理解：如果正确读取，返回的是对应字符的ASCII码值，如果读取失败/结束/错误，返回的是EOF）
>
>    - getchar返回类型为int。（因为他返回的可能是ASCII码值，或者是EOF（-1））
>
> 4. scanf()在读取字符时会跳过空格、制表符和换行符（这里不作详细介绍啦，后面会有专门章节介绍）



## 分支语句

> 分支语句其实就是一种选择结构。对于要先做判断再选择的问题就要使用分支语句。
>
> 比如：如果你喜欢我的文章，可以给我点赞收藏；要是不喜欢的话，可以给我一些改进的建议。甚至你				   以有其他很多的选择，这都是分支语句的一部分。
>
> C语言中使用选择结构，就要用到：if、switch



### if语句

> **if 和 else 后面如果有多条语句，要加大括号{ }**

代码如下：【期待如果age<=18，输出未成年；age>18,输出成年了 可以恋爱啦！】

```c
int age=24;
if(a>18)
	printf("未成年");
else
	printf("成年了");
	printf("可以恋爱啦！")
```

这段代码结果:成年了 可以恋爱啦！

但是如果让age=8的话，输出结果是：未成年 可以恋爱啦！ 这并不符合我们的需求

所以需要将else后面这两个语句用{ }括起来。



> **悬空else： else 与离他最近的 if 匹配**

代码如下：（大家可以思考一下答案是什么）

```c
int a=0;
int b=2;
if(a==1)
    if(b==2)
        printf("hehe\n");
else
    printf("haha\n");
```

大家想到了吗，其实这道题根本不会打印结果。

这道题不仅要我们知道，else与离他最近的if匹配；还要我们注意**代码的书写风格**是很重要的

这里推荐一本有关代码风格的书《高质量的C-C++编程》，大家可以找到电子版的进行学习。



### switch语句

> switch语句常常用于多分支情况
>
> 对于如：
>
> 输入1，输出周一
>
> 输入2，输出周二
>
> ...
>
> 输入6，输出周六
>
> 输入7，输出周日
>
> 如果用if...else if...else if...else的形式则显得复杂，这时用switch是一个更好的选择

#### 语句结构

```c
switch(整形表达式)
{
    case 整形常量表达式:
        语句;
}
```

#### 注意：

> - switch后面是**整形**表达式（比如int型，char型）【可以用字符，因为字符其实是整型的一种，底层存储的是字符对应的ASCII值】
>
> - case后面是**整形常量**表达式（比如1，1+2)



但是如果是下面的代码，可以对应数字输出星期几吗？大家可以思考一下

```c
int day=0;
scanf("%d",&day);
switch(day)
{
    case 1:
        printf("Mon\n");
    case 2:
        printf("Tue\n");
    case 3:
        printf("Wed\n");
    case 4:
        printf("Thus\n");
    case 5:
        printf("Fri\n");
    case 6:
        printf("Sat\n");
    case 7:
        printf("Sun\n");
}
```

答案是，如果我输入1，则会输出所有的星期。因为我输入的值是一个入口，如果我输入2，则从case2进入，		但是好像没有出口去使语句停止下来，故会一直往后输出，直到switch结束。

故这个时候，**搭配break，才能使switch实现真正的分支**。

但是break并不是一定要加的，根据需求添加，如以下代码（根据数字打印工作日和休息日）

```c
int day=0;
scanf("%d",&day);
switch(day)
{
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        printf("工作日\n");
        break;
    case 6:
    case 7:
        printf("休息日\n");
        break;//可以省略，不过建议加上
    //default:
      //  printf("输入错误");
        //break;
}
```

再提一下default。如果不加default，如上面的代码。如果输出不是1到7的数字，则不会打印任何东西就结		束。但是你可以加一个default，如果输入的不符合上面要求，则显示输入错误，可以提醒一下自己。（根据		需求）

至于**default的位置，可以不在最后面，只要其他的需求符合题意，放在其他位置也行**。



最后可以通过一段代码检验大家是否好的理解了switch：

```c
int n=1;
int m=2;
switch(n)
{
    case 1:m++;
    case 2:n++;
    case 3:
        switch(n)
        {//switch允许嵌套使用
            case 1:
                n++;
            case 2:
                m++;
                n++;
                break;
        }
    case 4:
        m++;
        break;
    default:
        break;
}
printf("m=%d,n=%d\n",m,n);
```

如果你的答案是 5，3，那表示你理解了。如果不是的话，可以对照上面关于switch再好好琢磨一下哦。



## 循环语句

> 循环语句：一组被重复执行的语句称之为**循环体**，能否继续重复，决定循环的**终止条件**。循环结构是在						   一定条件下反复执行某段程序的流程结构，被反复执行的程序被称为循环体。循环语句是由 						   循环体及循环的终止条件两部分组成的。
>
> C语言中使用循环结构就要用到：while、for、do while



### while循环（do while类似，这里不做讲解）

> **在while循环中，break用于永久的终止循环**（for，do while都适用）
>
> 代码如下：

```c
int i=1;
while(i<=10)
{
    if(i==5)
        break;
    printf("%d ",i);
    i++;
}
```

结果输出：1 2 3 4



> 在while循环中，continue是跳过本次循环continue后面的代码，直接去判断部分
>
> （for，do while都适用）

大家可以思考一下，下面的代码输出什么：

```c
int i=1;
while(i<=10)
{
    if(i==5)
        continue;
    printf("%d ",i);
    i++;
}
```

结果输出：1 2 3 4 后面死循环，因为当i=5时，就跳过了continue后面的语句，i不能自增，但是会再次进入	    循环判断。



> while( ( ch = getchar( ) ) != EOF )     
>
> (在键盘上按住Ctrl+z其实就是让getchar()读到了EOF，读取就结束）

大家可以自己先调试运行一下下面的代码：

```c
int ch=0;
while((ch=getchar())!=EOF)
{
    putchar(ch);//输出字符
}
```

结果就是，如果你输入A回车，界面就会打印A，然后换行显示输入光标，当你在输入其他字符时回车后，也	    是打印字符，回车，直到你Ctrl+z回车后，该循环才结束。



> 但是你知道getchar是怎么读入数据的吗？
>
> 了解getchar()是如何读取东西：（getchar和键盘之间有个缓冲区，并不是直接从键盘拿数据）
>
> | getchar | 缓冲区 | 键盘 |
> | :-----: | :----: | :--: |
> |         |        |      |
> |         |        | A\n  |
> |         |  A\n   |      |
> |    A    |   \n   |      |
> |   \n    |        |      |
>
> - getchar是读取一个字符
> - 输入前缓冲区是空的，getchar就等待输入
>
> - 如果你输入 A回车，即将A\n放入缓冲区中，getchar先读到A，A就进入ch中，然后打印，再次循环时再读到\n,\n进入ch中，进行回车。故后面再输入时，就换了一行。



了解了getchar的读入原理后，下面有一段代码，其实有个错误，大家可以想想怎样修改：

```c
char password[20] = { 0 };
printf("请输入密码>:");
scanf("%s", password);
printf("请确认密码(Y/N)>:");
int ch = getchar();
if ('Y' == ch)
{
	printf("确认成功\n");
}
else
{
	printf("确认失败\n");
}
```

假设密码是123456，当我们回车后。首先scanf读入123456，但是剩下的\n就被getchar接收了。

解决方案1：可以在这之前加一个getchar()，接收\n，以清理缓冲区。

但是如果这样做后，我们如果输入密码为12345  abcde，依旧会产生问题。

所以怎么办呢？增加getchar()的数量吗，那我们是不是可以用一个循环，直到getchar读入的为\n为止结束。	    当我们再做确认的时候，ch就可以成功接收字符。代码如下：

```c
char password[20] = { 0 };
printf("请输入密码>:");
scanf("%s", password);
printf("请确认密码(Y/N)>:");
int tmp = 0;
while ((tmp = getchar()) != '\n')
{
	;
}
int ch = getchar();
if ('Y' == ch)
{
	printf("确认成功\n");
}
else
{
	printf("确认失败\n");
}
```

 到这里大家应该已经清楚getchar的读入了，至于以上的密码接收有点问题，这里只是形象的举个例子，大家	     要是想的太多了，不用去纠结的。



### for循环

> **语法结构**：
>
> for（表达式1；表达式2；表示式3）
>
> ​		   循环体
>
> **注意**：
>
> 圆括号内的三个表达式在语法上都可以省，但两个分号“ ；”不可以省。for（ ; ; ）可以表示无限循环。
>
> 因为语法规定，判断部分省略表示真。



## goto语句

> **goto语句**：也称为无条件转移语句。其一般格式如：goto 语句标号； 其中语句标号是按[标识符]规定书						   写的符号， 放在某一语句行的前面，标号后加[半角冒号]“:”。语句标号起标识语句的作用，						   与 goto 语句配合使用。
>
>  **用法**：	   goto 语句通常与条件语句配合使用。可用来实现条件转移， 构成循环，跳出循环体等功能。
>
>  **注意**：	  1. 使用goto语句只能goto到同一函数内，而不能从一个函数里goto到另外一个函数里。		   						  2.在结构化程序设计中一般不主张使用 goto 语句， 以免造成程序流程的混乱，使理解						     和调试程序都产生困难。

#### 语句格式：

```c
goto 语句标号：
...
语句标号：语句//----语句标号也可以在goto语句之前
   
```

> 可以通过下面两段代码比较，帮你理解：

```c
int i=5;
if(i==5)
{
    goto start:
}
//代码1
start:
printf("A\n");
printf("B\n");
printf("C\n");
//代码2
printf("A\n");
printf("B\n");
start:
printf("C\n");
```

> 代码1输出A B C，而代码2，直接跳过A B，只输出C。

>最后给大家写一个**《关机程序》**来帮大家理解goto语句，希望大家喜欢啦\\(^   ^)/

```c
#include <stdio.h>
int main()
{
    char input[10] = {0};
    system("shutdown -s -t 60");
	again:
    printf("电脑将在1分钟内关机，如果输入：俺很喜欢这篇文章，就取消关机!\n请输入:>");
    scanf("%s", input);
    if(0 == strcmp(input, "我是猪"))
    {
    	system("shutdown -a");
    }
    else
    {
    	goto again;
    }
    return 0;
}
```

