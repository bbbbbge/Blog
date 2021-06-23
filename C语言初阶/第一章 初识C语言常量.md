## 初识C语言常量

C语言中的常量分为以下几种：

- 字面常量

- const修饰的常变量

- #define定义的标识符常量

- 枚举常量

  

### 字面常量

即字面意思不能改变的量。如1就是1，你不能说让1等于2；如人的血型有固定的几种（A，B，O，AB）；如人的性别也只分为男性，女性，以及更深奥的一种形态。

在C语言中：1，3.14，‘a’，“hello”...这些都叫做常量。



### const修饰的常变量

可以通过一段代码来理解const修饰的常变量：

```c
int num = 10;
printf("%d\n", num);		//num=10
num = 5;
printf("%d\n", num);		//num=5
```

上面这段代码中 num是一个变量，通过你给num赋新的值，num就不停的在改变。

但是当你在数据类型前面加上const，num就发生微妙的改变。（自己可以在编译器上使用看看）

```c
const int num = 10;
printf("%d\n", num);		//编译产生报错
num = 5;
printf("%d\n", num);
```

当你编译后，结果会产生报错：

![image-20210403114222195](C:\Users\lenovo\Pictures\test_\image-20210403114222195.png)

因为此时num在const修饰下已经变成了常变量，而变量是不可以被修改的。

但是num此时不能完全叫做常量，它归根结底还是变量。如它不能在数组定义的时候使用。

```c
//通过定义一个数组看出问题
//int arr[10] = { 0 };------正常的定义数组

//int num = 10;
//int arr[num] = { 0 };-----结果产生报错

//const int num = 10;
//int arr[num] = { 0 };----结果产生报错
```



### #define定义的标识符常量（也叫宏定义）

这是C语言定义数组大小经常用到的方法，大家可以自行使用感觉一下。

使用格式：#define <标识符> <常量值/表达式>

```c
#include <stdio.h>
#define MAX 10
int main()
{
	int arr[MAX] = { 0 };	//通过改变MAX的大小就可以改变数组大小
    printf("%d",MAX);		//MAX=10
	return 0;
}
```

下面有个思考题，大家可以思考一下结果是什么：

```c
#include <stdio.h>
#define MAX 5+5
int main()
{
	printf("%d", 3 * MAX);
	return 0;
}
```

此时输出的结果是20，而并不是30。所以要明白#define MAX 5+5，MAX并不等于10。

既然可以把一个表达式赋给一个标识符，那我可以不可以把一些参数赋值给这个标识符呢？

大家可以思考一下这段代码：

```c
#include <stdio.h>
#define Add(a,b) a+b
int main()
{
	int sum = Add(3,2);
	printf("%d\n",sum);
	return 0;
}
```

此时，先发生sum=a+b，再发生sum=3+2，故输出5

我们这里只是讲解最基础的常量问题，故不多衍生宏定义，后面会专门讲解宏定义相关的内容。



### 枚举常量

如果大家学过结构体，枚举的定义与其比较相似。

enum的使用方法：

1.在定义enum的同时，声明变量:

```c
enum Day {
	Mon,Tue,Wed,Thus,Fri,Sat,Sun
}Workday;			
```



2.定义完enum之后再声明变量：

```c
enum Day {
	Mon,Tue,Wed,Thus,Fri,Sat,Sun
};
enum Day Workday;
```



3.定义匿名的枚举变量：（如果整个程序只用一个枚举，则enum后面不必加标识符，但是不能再定义枚举结构）

```c
enum {
	Mon,Tue,Wed,Thus,Fri,Sat,Sun
}Workday;	
```



通过一段码来为大家剖析枚举结构的一些细节：

```c
#include <stdio.h>
enum Day {			//enum--枚举类型关键字  Day--枚举类型标签  enum Day--枚举的类型
	Mon=1,
	Tue,			//{ }里面的为枚举值
	Wed,
	Thus,
	Fri,
	Sat,
	Sun
}Workday;			//Workday--枚举变量
```

这里做一些说明：

1.如果Mon不做赋值，则默认为0，后面依次增加，如Tue=1，Wed=2...

2.如果Mon赋值为3，则后面也依次增加，如Tue=4，Wed=5...

3.如果是从中间赋值，如Thus=7，则Thus后面的依次增加，之前的从Mon开始则从0

开始增加

4.枚举值是常量，不是变量。不能在程序中用赋值语句再对它赋值。

   如：Tue=7，Sun=Wed。这些都是错误的。

5.只能把枚举值赋给枚举变量，而不能将该枚举值的数值赋给枚举变量

   如：Workday=Tue----正确

​           Workday=2----错误

关于枚举的更多东西，后面再做分享。希望大家可以多动实践，这样自己会发现更多的东西。

