---
title: Java 学习之路
declare: true
date: 2020-05-12 20:14:06
tags: [Java]
categories: [计算机基础,Java]
toc: true
copyright: true
---

<meta name="referrer" content="no-referrer" />  
<!--more-->

# Java 学习之路

[TOC]



## Part 1 为什么要学 Java

### 1.1 应用市场

&emsp;Java作为主流语言，已有30亿的设备正在运行Java程序，应用市场很大，包括，电脑，打印机，路由器，智能手机，地铁交通卡...

### 1.2 前景

&emsp;职业生涯方面，工作岗位多，薪资不错。语言本身也很有活力。

### 1.3 语言特性

1.Java是一种纯面向对象的语言。

2.简洁性

> Java语法和C++相似
>
> Java省略了C++中的一些语言包袱(多继承，操作符重载等)
>
> Java舍弃了C++中的**指针**
>
> Java提供内存回收机制，程序员不用再去进行**内存管理**

3.可移植性(平台无关性)

> 平台是**操作系统(OS) + 处理器CPU**，平台无关指的是，不管你是Mac，Windows还是    Linux操作系统，无论你用的谁家的CPU，Java的字节码通过JVM总能成功运行。
>
> Java可以将源代码编译成字节码，通过Java虚拟机(JVM)来执行字节码。

4.解释型(半解释半编译)

> Java源代码被编译成字节码后，Java平台中的**Java解释器**会对字节码做解释执行，这个效率随着CPU性能的提高而提高

5.适合分布式计算

> 有很多网络编程的类库，可供使用

6.性能好

> 相比于同为解释型语言的Python，JavaScript，MATLAB等等相比，Java是高性能的
> Java用伪编译器将源代码转化为字节码，然后解释执行
> 还可以通过**JIT(Just-In-Time)编译器**直接把字节码转化成机器码，然后缓冲下来，需要时直接执行

7.安全性

> 在网络环境中，为确保应用安全，Java提供**安全管理机制**

8.健壮性

> Java采用**强类型转换**，**异常处理**，**垃圾回收机制**，**丢弃指针**和**安全检查机制**等方式保障Java程序健壮性

9.多线程处理能力

10.动态语言 



### 1.4  运行机制

#### JVM (Java Virtual  Machine)

Source.java -> Source.class ->执行

![](https://images.gitee.com/uploads/images/2020/0124/122946_f138d931_5550632.png)

1. 写源代码(.java文件)
2. 执行javac.exe生成字节码文件(.class)

3. 执行java.exe运行程序

```python
def load(Source_file_java):
 "加载.class到内存"
 return Source_file_class

def execute(Source_file_class):
 "基于平台转换成机器指令"
 return binary_file

def check(Source_file_class):
 if "合法且安全"：
 	"告诉平台"
     return True
 else:
     "回去重写代码"
     return False
 
while True:
 Source_file_class = load(Source_file_java)
 if(check(Source_file_class)):
     binary_file = execute(Source_file_class)
 else:
     break;
 
```



### 1.5 搭建运行环境

#### 相关术语

JDK(Java Development Kit) Java开发工具包

JRE(Java Runtime Environment) Java运行环境

JVM(Java Virtual Machine) Java虚拟机

SDK(Software Development Kit) 开发工具包

它们的关系是这样的

![](https://images.gitee.com/uploads/images/2020/0225/140553_a8dd8739_5550632.png)



1.浏览器搜索 java archive，进入官网选择对应版本。

2.找到适合的此电脑操作系统的版本下载，选择路径安装。

3.配置环境变量，Windows10下，右键此电脑属性->高级系统设置->环境变量->在系统环境变量中新建JAVA_HOME，变量值D:\\...\Java\jdk-11.0.4(你的jdk安装路径)->进入Path，添加%JAVA_HOME%\bin

4.下载IDE，Eclips(开源，免费)

   

## Part 2 基础语法

&emsp;类(class)是Java中最基本的逻辑单位,所以Java程序可以看成由一个个class构成的程序。类里包含两项内容，**成员变量和方法**，一个class中只能有这样命名的main 函数**public static void main(String[] args)** 或 **static public void main(String[] args)**还有**public static void main(String args[])**



文件名是 Test.java  ，在Java中**主类名应该和文件名完全相同!!!**

```java
public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		System.out.println("Hello world!");
		int i;
		
		for(i = 2;i<10;i++) {
			if(Test.is_prime(i)) {
				System.out.printf("%d is primary number\n",i);
			}
			System.out.printf("%d 的阶乘是 %d\n",i,Test.factorial(i) );
		}
	}
	
	public static boolean is_prime(int num) {
		int i;
		for(i = 2;i<num;i++){
			if(num%i == 0){
				return false;
			}
		}
		return true;	
	}
	
	public static int factorial(int num) {
		if(num == 1) {
			return 1;
		}
		else {
			return factorial(num-1)*num;
		}
	}

}
```



### 2.2 Java数据类型

**基本数据类型**

**非数值型**

1. char  一个16bit的Unicode字符
2. byte 能存放8个bit
3. boolean 只有true和false

**数值型**

&emsp;整型

&emsp;short,int,long 

```java
/*定义时注意 l (L) long num = 1344312312 l*/
long num = 1344312312l;
long num_2 = 134431231L;
```

&emsp;浮点型

&emsp;float,double

编译器默认使用双精度浮点数(double)，所以定义float型变量时最好加上f

```java
float num = 12.34f;
```

**引用数据类型**

类 ( class )

接口 ( interface，Annotation )

数组 ( [] )

枚举 ( enum )

它们在内存中的大小(bit)，最大最小容纳界限，都可以以下图的方式查看:

![](https://images.gitee.com/uploads/images/2020/0301/104038_b2644218_5550632.png)



**Java标识符声明规则**

由于Java语言采用的是**Unicode字符集**，这就意味着，声明变量时可以出现中文。

标识符(变量名，方法名..)中可包含的合法字符：

> Unicode 的字符(包括中文)【长度不限】
>
> $
>
> 数字
>
> _
>
> > 可以有数字，**但不能以数字开头**

![](https://images.gitee.com/uploads/images/2020/0301/104913_c908c36d_5550632.png)

这些都可以...但是要记住，**一个好的名字，一定要能“知名解意”**。



#### 常量与变量

##### 常量

1.整型常量

> 十进制整数：110，112，120，999，...
>
> 八进制整数: **0**112，**0**114，**0**777，...【在数字前面加0】
>
> 十六进制整数:**0x**456ab，**0x**ffff，**0x**123cf，...【在数字前面加0x】
>
> 二进制整数【Java7以上版本支持】:**0B**1111,**0B**1101,...

Java 7 的新特性,可以在整数中放下划线，来区分位数

```java
long number = 1_000_000_456L;
```



2.浮点型常量

> 小数点形式：3.14169,0.61803,2.71828...
>
> 指数形式:

0.54123e10就代表了

$$
0.54123*10^{10}
$$

12345e-2同理可知
$$
12345*10^{-2}
$$




3.字符型常量

> **单引号**括起来的单字符： ’a'，'b'，'学'，...【每个字符都是两个字节】
>
> **单引号**扩起的转义字符：'\n'，'\b'，'\t'，'\\'''，...
>
> **单引号**扩起的八进制转义字符：'\ddd'【d是数字】，'\101'八进制101 = 十进制 65，ACSII字符'A'
>
> '\012' = '\n'
>
> **单引号**扩起的Unicode转义字符:'\uxxxx',【x是十六进制数(0-F)】



4.字符串常量

> **双引号**扩起的**0**或**多个字符序列**："Hello World!\n",""...
>
> Java一行只能写一个字符串，想拼接用”+“



5.布尔型常量

> true
>
> false



##### 变量

变量：程序运行过程中其值可以发生改变的量

变量的构成：**变量名** 和 **变量值**【酒店房间号和住进去的人】

```java
int x,y,z;//声明语法： 数据类型 变量名1,[变量名2,...];
x = 7386;//赋值语法:和C语言一样
```



##### 数据类型转换

**自动转换**

> 1.转换前后的**数值类型**要兼容
>
> 2.转换后的**表示范围**要比之前的类型大
>
> 例如：
>
> byte->short->int->long
>
> PS：在这组转换关系中没有数据丢失



**强制转换**

有的时候我们需要强制将double当成int使用，这当然会导致**信息丢失**

```java
double num = 31.415926;
int num2 = (int)num; // 语法和C语言一样
```



### 2.3 选择结构

#### 2.3.1 if-else 语句

![](https://images.gitee.com/uploads/images/2020/0323/194729_3e0af442_5550632.jpeg)

```java
boolean con = true;
if (con) {
    System.out.println("True");
} else {
    System.out.println("False");
}
```

注意：if-else语句有一种缩略写法如下

```java
int a,b,c;
c = a>b?a:b;
```

这条语句等价于

```java
if(a>b){
	c = a;
}
else{
	c = b;
}
```



#### 2.3.2 if-else if-else语句

![](https://images.gitee.com/uploads/images/2020/0323/195714_885f8092_5550632.jpeg)

```java

int con = 1;
if (con == 1) {
System.out.println("1");
} else if (con == 0) {
System.out.println("0");
} else {
System.out.println("False");
}

```



#### 2.3.3 switch 语句

switch语句又称开关语句和C语言很像，语法格式如下：

```java
int choice = 1;
switch (choice) {
    case 1:
        System.out.println("1");
        break;
    case 2:
        System.out.println("2");
        break;
    case 3:
        System.out.println("3");
        break;
    case 4:
        System.out.println("4");
        break;
    default:
        System.out.println("default");

}
```

注意：

> 1. Java的switch的条件中只能是int,short,byte,char[常用的就这些，多了我也记不住了]
>
> 2. 关键字**break**起到了“兜底”的作用，即执行完一条case语句后会停止整个switch代码块
> 3. 当所有条件都不满足时，执行default



### 2.4 循环结构

#### 2.4.1 for循环

```
for(计算表达式1;循环条件;计算表达式3)
```

![](https://images.gitee.com/uploads/images/2020/0323/201058_e4cc2768_5550632.jpeg)

和C语言一样，虽然不想赘述了，但是还是写个Demo意思一下吧。

```java
public class Test {
	//这是一个计算从1加到100的程序
	public static void main(String[] args) {
		
		int sum = 0;
		for(int i = 0;i<=100;i++) {
			sum+=i;
		}
		System.out.println(sum);
	}
}
```



#### 2.4.2 while循环

语法格式：

```java
boolean con = true;
while(con){
	/*我是循环体代码，且这是个死循环*/
}
```

既然在语法格式中我写了一个死循环，那么就接着研究研究怎么跳出循环吧，毕竟这两个关键字不讲也不行。

**continue**

作用：跳出本次循环

**break**

作用：跳出本层循环

是不是特别简洁[糊弄]，写两个例子就明白了。

Demo1

```java
public class Test {

	public static void main(String[] args) {
		
		int i = 0;
		while(i++<100) {
			if(i%2 == 0) {
				continue;
			}
			System.out.println(i);
		}
	}
}
```

打印出1-100的所有奇数，因为遇到偶数就会跳出本次循环，即continue以下的语句都不执行。

Demo2

```java
public class Test {
	public static void main(String[] args) {
		int i = 0;
		int sum = 0;
		while(i<=100) {
			if(i == 50) {
				break;
			}
			sum+=i;
			i++;
		}
		System.out.println(sum);
	}
}

```

此时当i = 50时就跳出循环了，答案是从1加到49 = 1225

#### 2.4.3 do-while循环

和C语言一样，依旧不想赘述

   do-while循环形式：

```java
do{
	"循环体语句"
}while("条件判断");
```



![](https://images.gitee.com/uploads/images/2020/0323/203620_41281115_5550632.jpeg)

再次强调一点，do-while中的**循环体代码无论如何都会至少执行一次。**



### 2.6 数组

喂(#`O′)，从现在开始，打起精神了，前面看累了的话，去洗把脸休息10分钟再来，后面的内容和C，C++，Python差别较大，仔细看好了哈！！！


#### 2.6.1 一维数组

##### 一维数组的声明

首先啊，咱们先学会声明一维数组，注意，是**声明**。

语法格式：

数组元素类型 [] 数组名;

数组元素类型 数组名 [] ;

以上两种声明方式哪个都对。

```java
int array[];
int [] array;
```

其中数组元素类型既可以是基本类型也可以是引用类型

```java
String strArr[];
double douArr[];
```

声明，就是给这个数组起了个名字，但是并没有真正的在内存中给它开辟空间，想要真正的拿到这个对象，需要实例化...啊，不对，是需要创建它。



##### 一维数组的创建

语法格式：

数组名 = **new**  数组元素类型名[数组元素个数]

```java
int arr[];//声明数组
arr = new int [3];//创建数组

arr2 = new int[3]{1,2,3};//创建数组时就给它初始化，静态数组
```

```java
arr = new int [100];//创建数组的简便写法
```

Java数组的创建过程

![](https://images.gitee.com/uploads/images/2020/0323/211555_e86a8f9b_5550632.png)



##### 一维数组的访问

可以通过下标对数组进行访问和修改。

```java
public class Demo {
	public static void main(String args[]) {
		int arr[] = new int [10];
		for(int i = 0;i<arr.length;i++) {//通过length方法获得数组长度
			arr[i] = i;
		}
		
		for(int i = 0;i<arr.length;i++) {
			System.out.println(arr[i]);
		}
	}
}
```

注意：数组下标从0开始，使用下标注意不要越界。



#### 2.6.2 二维数组

在Java中，只存在一维数组，二维数组可以给它看成一维数组中套着若干个一维数组。所以，在Java中我们只需准确声明二维数组中有多少个一维数组即可，即行数。

```java
int matrix [][] = new int[4][];
```

上面这条语句就是声明了一个二维数组matrix，其中包含4个一维数组。

由于Java采用“数组之数组”的特性，我们就可以声明这种不定长的二维数组

```java
public class Demo010 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int matrix [][] = {{1,2,3},{4,5},{6,7,9,8},{1,2,3,4,5,6}};
		for(int i = 0;i<matrix.length;i++) {
			for(int j = 0;j<matrix[i].length;j++) {
				System.out.print(matrix[i][j] + " ");
			}
			System.out.print("\n");
		}	
	}
}
```

运行结果：

![](https://images.gitee.com/uploads/images/2020/0324/205915_9c8491b5_5550632.png)



#### 2.6.3 for-each语句

Java和C++一样，为了方便程序员遍历数组，都设计出了一种for-each语句来进行数组遍历。

语法格式：

for(数组元素类型名 变量名:数组名){

}

```java
//一维数组
int arr[] = new int[10];
for(int i = 1;i<=10;i++) {
    arr[i-1] = i;
}

for(int i:arr) {
    System.out.print(i + " ");
}
//运行结果：1 2 3 4 5 6 7 8 9 10 
//等价于
for(int i = 0;i<arr.length;i++){
    System.out.print(arr[i] + " ");
}
```

```java
//二维数组
int matrix [][] = {{1,2,3},{4,5},{6,7,9,8},{1,2,3,4,5,6}};

for(int []list:matrix) {
    for(int elem:list) {
        System.out.print(elem + " ");
    }
    System.out.print("\n");
}

/*运行结果：
1 2 3 
4 5 
6 7 9 8 
1 2 3 4 5 6 
*/
//等价于
for(int i = 0;i<matrix.length;i++){
    for(int j = 0;j<matrix[i].length;j++){
        System.out.print(matrix[i][j] + " ");
    }
     System.out.print("\n");
}
```



#### 2.6.4 有关数组操作的Arrays类

Arrays类可以通过

```java
import java.util.Arrays;
```

这条语句导入

常用方法

> boolean equals（array1，array2）：比较两个数组是否相等
>
> void sort（array）：对数组array元素进行升序排序
>
> String toString(array)：该方法将会一个数组array转换成一个字符串
>
> void fill（array，val）：把数组array所有元素都赋值为val
>
> copyof(array,length):把数组array复制成一个长度为length的新数组
>
> int binarySearch(array,val):查询元素值val在数组array中下标



### 2.7 方法(函数)

由于Java是纯面向对象的语言，所以，所有的函数都是写在类的内部的，我们将类内部的函数称为**方法**。

排除那些乱七八糟的关键字[public,private,protected...]【访问权限控制符】，其实Java中写方法的步骤和C语言中写函数的方式差不多，无外乎就是**确定形式参数列表**，**确定返回值**。

在Java中我们第一个看到的就是主方法

```java
public static void main(String[] args) {
		"代码块"
	}
```

咱会发现，比起传统的函数，它多了两个关键字**public** 和 **static**，现在讲这两个关键字还有点早，**存在既有意义**，可能在面向对象的时候讲更容易理解。总之，咱们先暂且先都这么写函数:

```
public static 返回值类型 函数名(形参列表){
	"代码块"
	return ...;//有返回值就写
}
```



**实参向形参传值的两种方式**

由于Java取消了指针，所以传参方式就变成了2种

1. 值传递
2. 引用传递



#### 2.7.1 Java特性

**形参长度可变**

在Java中，如果你不确定方法需要多少个参数，可以写一个可变长参数，这个参数Java默认把它当成一个数组，注意：**可变长参数前的类型名不能少**。

```
public static void foo(int a,int b,int...arr) {

}
```



**函数重载**

在Java中，如果在**同一个类中**起了**同名的函数**，但**形式参数列表不同(参数类型，个数)**它会依据不同实参选择不同函数。这与**返回值类型无关**。

比如：

```java
public class Test {
	public static void main(String[] args) {
		int [] arr = {1,2,3,4,5,6,7,8,9,10};
		double [] arr2 = {3.1,3.34,2.34,45.32,56.9};
		
		System.out.println(sumArray(arr));
		System.out.println(sumArray(arr2));
		
	}
	
	public static double sumArray(double []arr) {
		double res = 0.0;
		for(double elem:arr) {
			res+=elem;
		}
		return res;
	}
	
	public static int sumArray(int []arr) {
		int res = 0;
		for(int elem:arr) {
			res+=elem;
		}
		return res;
	}    
}
```

你会发现这里有一个求和方法**sumArrray**,一个形参列表是double数组，另一个形参列表是int数组。虽然它们都叫**sumArrray**，但是Java会依据不同实参进行函数重构。而不是像C语言那样报错。

附上运行结果:

![](https://images.gitee.com/uploads/images/2020/0325/184738_624b9416_5550632.png)

**函数重写(Rewrite)**

这一块的内容将在继承的时候详细讲解。



**命名规则**

驼峰式：sumArray();



## Part 3 面向对象(Oriented Procedure)

#### 对象

&emsp;面向对象的思想大致可以从三个维度来进行描述，第一个维度，**客观世界**，第二个维度，**概念世界**，第三个维度**计算机的世界**。基于面向对象思想，我们开发软件的角度不再是从某个功能出发，而是站在上帝视角对整个世界进行逻辑抽象到达概念世界，在概念世界中设计方法，应用于计算机的世界。

&emsp;比起面向过程，面向对象弱化了**流程**这个概念，我们接下来举个例子说明一下，体会一下二者的区别。



生活场景：糕点师傅在面包房中烘焙面包

**面向过程**

糕点师傅**首先**进入了面包房，**然后**准备了原材料，**接着**打开了烤箱，**最后**完成了烘焙。

**面向对象**

糕点师傅是个对象，面包房是个对象，面包是个对象。糕点师傅通过某种方法打开了面包房的门，然后门开了，糕点师傅通过某个方法，然后原材料有了，糕点师傅又通过某个方法，给不同面包标了个价，使用面包房中的烤箱(方法)，面包熟了。



即，面向对象的理念是**用软件系统模拟真实世界的系统**。

对象本身是从现实中抽象而来的，所以它拥有和现实对象一样的特性

> 1.  唯一性：任意两个学生是不同的，所以每个学生对象都是不同的
> 2. 属性：对象的静态特征。比如：学生的学号，姓名，性别，体重，身高...
> 3. 行为：对象的动态特征。比如：学生在学习，学生在吃饭，学生在摸鱼...
> 4. 状态：行为改变状态，状态即所有属性的集合。例如：学生打羽毛球前，体重为60kg，进行打羽毛球这个行为后体重变成了59.5kg



#### 类

把具有相同属性和行为的对象进行抽象就得到了类。

所有动物都有这些属性：如，性别，门类... 而且都有这些行为：如吃，喝，拉，撒，睡...

所以可以把所有动物对象抽象成动物类



#### 对象与类

&emsp;现实世界中是由对象和对象之间相互作用组成的，那什么是对象呢？就如同面包房做面包，通过模子生产出的一个个面包就是不同的对象，它们有名称，价格，配料表(对象属性),它们有用途,比如被吃掉(方法)。所以，**对象 = 属性 + 方法 || 对象的规范(类) = 属性定义 + 方法定义**，模子，就是我们所说的规范，即 “类”。

##### 从内部组成上看

基本类型(单一变量) => C语言结构体(多个变量没有方法) => Java类(多个变量加方法)【甚至还有匿名代码块】

##### 从宏观概念上看

类就是类型，它抽象出了对象的共性，是虚的。

对象是一种变量，是具体的东西。

##### 从生活角度上看

类规定了对象应具有的属性和方法，从类->对象，叫做**实例化**，

比如:西红柿炒鸡蛋菜谱就是类，一盘西红柿炒鸡蛋这道菜就是对象，通过向锅里放不同比例的调料，就是在实例化不同的对象。

所以，**对象的抽象是类，而对象是类的实例**，类的成员变量就是对对象状态的抽象，类的方法则是对对象行为的抽象。



**面向对象三大特征**：

**继承**，**多态**  和 **封装**

咱们先看最好理解的封装，剩下的以后慢慢讲

封装：简单来说就是将客观世界中对象的属性和方法放到类的内部，详细的后面会细讲。



#### 3.1 定义类和实例化对象

&emsp;既然我们对类与对象有了一个简单的认识，那么就让我们用Java语言来对这个世界进行抽象吧。

&emsp;使用关键字public class声明一个类(public 是一个关键字【访问权限控制符】，这样声明使得该类在任意情况下都可以使用)

我们认为一个.java文件就是一个独立的类，所以一个java源程序中**只能有一个public类(公共类)**，其他种类的类个数不限【但是不建议把类都写到一起，一个java文件就是一个类是最好的】

类里面有两样东西：**成员变量**的声明和**方法**



```java
public class Test/*类名*/
{
    int x,y;//声明成员变量
    public Test(int num1,int num2)/*构造函数-特殊的方法*/
    {
        x = num1;
        y = num2;
    }
    public int gcd(int a,int b)//方法
    {
        if(b == 0)
        {
            return a;
		}
        return gcd(a,a%b);
    }
}
```



##### 3.1.1 实例化对象

***Java语法 : 类名 对象名 = new 类名(属性值...)***

咱们再来写几个Demo来熟练类和对象的这种表达方式

以下是一个学生类，属性包括 ：*studentId，name，gender，age，tel* ，方法有：  *learn，exam*

```java
public class Student {

	String studentId,name,gender;
	int age,tel;
	
	public static void learn() {
		System.out.println("我是学生，我正在学习!");
	}
	
	public static void exam() {
		System.out.println("我是学生，我正在考试!");
	}
		
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Student xiaoming  = new Student();
		Student lihua = new Student();
	}

}
```

这个类实例化出了两个对象，一个xiaoming(小明),另一个叫做lihua(李华),他们在内存中是这样的存储方式。

![](https://images.gitee.com/uploads/images/2020/0330/202614_3eb6b43e_5550632.png)

**栈内存中存放对象的引用(类似于指针，作用相同)**，堆内存中存放对象真正的信息



```java
package secondpackage;

public class Rectangle {

	double length,width;//声明成员变量
	
	public double calculateArea() {//方法：计算面积
		return length*width;
	}
	
	public double calculatePerimeter() {//方法：计算周长
		return 2*(length+width);
	}
	
	public String getInfo() {//方法：获取信息
		return "Rectangle's length is " + length + " width is " + width; 
	}
	
}

public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Rectangle r1 = new Rectangle();
		r1.length = 20;
		r1.width = 15.3;
		
		System.out.println("r1's area is "+r1.calculateArea());
		System.out.println("r1's primeter is "+r1.calculatePerimeter());
		System.out.println(r1.getInfo());
	}

}

/*
运行结果
r1's area is 306.0
r1's primeter is 70.6
Rectangle's length is 20.0 width is 15.3
*/
```



定义类时我们要遵循**开放封闭原则(Open Closed Pricinple)**，即对拓展开放，对修改封闭。

核心就是一个词**解耦合**，类越独立，越抽象耦合度就越低，对于程序的可拓展性，健壮性就越好。



##### 3.1.2 构造方法(函数)

语法规则: 

public 类名(初始化参数列表...)

{

​		...

}

所谓构造方法就是**与类名相同的方法**

```java
public class Test{
	public Test("初始化参数列表"){
		
	}

}
```

注意：构造方法**不能有返回值,同时还不能用void声明**，若不写构造方法，编译器会自动生成一个空的构造方法。构造方法也是方法同样**可以进行重载**。

Q:构造方法干什么用的？

A:有时我们希望在实例化对象的同时给它的属性赋初始值。比如，下文中的Point类，我希望每个点初始时都能拥有x,y两维坐标，所以在实例化的时候就需要传两个值进去。

```java
public class HelloWorld
{

	public static void main(String[] args)
	{
		Point p1 = new Point(1,2);//实例化一个叫做p1的对象
		p1.get_location();	//调用方法
	}
}
/*Point 类 如下，在另外的一个.java文件中*/

public class Point
{
	double x = 0.0,y = 0.0;
	public Point(double num1,double num2)//构造函数1
	{
		x = num1;
		y = num2;
	}
    
	public Point(int num1,int num2)//构造函数2
	{
		x = (double)num1;
		y = (double)num2;
	}
    
	public void get_location()
	{
		System.out.println("X = " + this.x +" "+ "Y = " + this.y);
	}
	
	public static void main(String[] args)
	{
		

	}
}
```

再写一个关于圆的类，来品一品构造方法的意义

```java
import java.lang.Math;
public class Circle {
	static double pi = Math.PI;
	double radius;
	public Circle() {
		radius = 1.0;
	}
	
	public Circle(double radius) {
		this.radius = radius;
	}

	public double getRadius() {
		return radius;
	}

	public void setRadius(double radius) {
		this.radius = radius;
	}
	
	public double calcArea() {
		return radius*radius*pi;
	}
	
	public double calcPerimeter() {
		return 2*pi*radius;
	}
}



public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Circle c1 = new Circle();
		Circle c2 = new Circle(4.0);
		
		System.out.println("采用无参构造方法产生的圆 ");
		System.out.println("c1's area is "+c1.calcArea());
		System.out.println("c1's primeter is "+c1.calcPerimeter());

		System.out.println("采用有参构造方法产生的圆 ");
		System.out.println("c2's area is "+c2.calcArea());
		System.out.println("c2's primeter is "+c2.calcPerimeter());

		System.out.println("修改圆c1成员变量radius ");
		c1.setRadius(100.0);
		System.out.println("c1圆 ");
		System.out.println("c1's area is "+c1.calcArea());
		System.out.println("c1's primeter is "+c1.calcPerimeter());

		System.out.println("c2圆 ");
		System.out.println("c2's area is "+c2.calcArea());
		System.out.println("c2's primeter is "+c2.calcPerimeter());
		
		System.out.println("修改类变量pi ");
		Circle.pi = 3;
		System.out.println("c1圆 ");
		System.out.println("c1's area is "+c1.calcArea());
		System.out.println("c1's primeter is "+c1.calcPerimeter());

		System.out.println("c2圆 ");
		System.out.println("c2's area is "+c2.calcArea());
		System.out.println("c2's primeter is "+c2.calcPerimeter());
		
	}

}

```



```
运行结果：
采用无参构造方法产生的圆 
c1's area is 3.141592653589793
c1's primeter is 6.283185307179586
采用有参构造方法产生的圆 
c2's area is 50.26548245743669
c2's primeter is 25.132741228718345
修改圆c1成员变量radius 
c1圆 
c1's area is 31415.926535897932
c1's primeter is 628.3185307179587
c2圆 
c2's area is 50.26548245743669
c2's primeter is 25.132741228718345
修改类变量pi 
c1圆 
c1's area is 30000.0
c1's primeter is 600.0
c2圆 
c2's area is 48.0
c2's primeter is 24.0
```

通过观察会发现，更改对象的成员变量时，都是独立的，对象之间不会发生影响。而修改类变量时，比如本例中把pi的精度调低，就会导致所有对象发生变化。



#### 3.2 this关键字(和Python中的self很像)

this指针，负责指向本类中的成员变量或方法，目的是进行区分同名成员变量和参数。从上面圆的例子就可以看出来，参数名叫radius，类里的属性名也叫radius，为了区分我们引入了**this**关键字

```java
package test;

public class Point
{
	private double x = 0.0,y = 0.0;//这里是this所指向的x,y
	
	public Point(double x,double y)//传的参数叫x,y，而成员变量也叫x,名称冲突，采用this区分
	{
		this.x = x;
		this.y = y;
	}	
	
	public Point(int x,int y)
	{
		this.x = (double)x;
		this.y = (double)y;
	}
	

	public double getX()
	{
		return x;
	}

	public void setX(double x)
	{
		this.x = x;
	}

	public double getY()
	{
		return y;
	}

	public void setY(double y)
	{
		this.y = y;
	}

	public void get_location()
	{
		System.out.println("X = " + this.x +" "+ "Y = " + this.y);
	}

}

```

此外，**this**还能互相调用构造方法，不过需要注意的是，它必须写在**构造函数的第一行有效位置上。**

```java
public class Person {
	int age;
	String name;
	
	public Person() {//无参构造函数
		
	}
	
	public Person(int age) {
		this.age = age;
	}	
	
	public Person(String name,int age) {
		this(name);//this 调用第二个构造方法
		this.age = age;
	}
	
	public Person(String name) {
		this.name = name;
	}
	
	public void speak() {
		System.out.println("大家好,我叫"+name+",我今年" + age + "岁!");
	}
}

```

**this**还能引用成员方法

语法格式：***this.方法名()***

```java
public class Person {
	int age;
	String name;
	
	public Person() {//无参构造函数
		
	}
	
	public Person(String name,int age) {
		this(name);
		this.age = age;
	}
	
	private void talk() {
		System.out.println("Here is 'talk'");
	}
	
	public void speak() {
		System.out.println("大家好,我叫"+name+",我今年" + age + "岁!");
		this.talk();//this引用成员方法
	}
}

```

我们给Person类添加一个方法

```java
public void printThis() {
		System.out.println(this);
	}
```

用来比较**对象** 和 **this** 之间的关系

```java
Person p1 = new Person("晓英",27);
p1.printThis();
System.out.println(p1);

/* 运行结果 */
Person@36d64342
Person@36d64342
```

两个引用指向同一内存地址

**对象名**：给栈内存单元取了个名字，在栈内存中存放堆内存的首地址

**this**：存在堆内存，保存了当前对象的引用





#### 3.3 private 访问权限控制符

&emsp;在实际生活中，有些属性是不想被别人知道的，比如身高，体重，年龄等等。同理，在类里，也有一些方法或者属性，只希望在类中自己使用，不想被其他类所使用。此时，我们引入了一个新的关键字**private**。

```java
package test;

public class Point
{
	private double x = 0.0,y = 0.0;
	
	public Point(double num1,double num2)
	{
		x = num1;
		y = num2;
	}	
	
	public Point(int num1,int num2)
	{
		x = (double)num1;
		y = (double)num2;
	}
	
	public void change_x(double num)//更改横坐标
	{
		x = num;
	}
	
	public void change_y(double num)//更改纵坐标
	{
		y = num;
	}
	
	public void get_location()
	{
		System.out.println("X = " + this.x +" "+ "Y = " + this.y);
	}
	
	public static void main(String[] args)
	{
		// TODO Auto-generated method stub

	}

}

```

像这种通过类方法**间接修改访问**成员属性的方式，叫做 **消息隐藏** 。

规范版:

```java
package test;

public class Person
{
	private String name;
	private double height;
	private double weight;
	private int age;
	
	public String getName()
	{
		return name;
	}
	public void setName(String name)
	{
		this.name = name;
	}
	public double getHeight()
	{
		return height;
	}
	public void setHeight(double height)
	{
		this.height = height;
	}
	public double getWeight()
	{
		return weight;
	}
	public void setWeight(double weight)
	{
		this.weight = weight;
	}
	public int getAge()
	{
		return age;
	}
	public void setAge(int age)
	{
		this.age = age;
	}
	
}

```

偷懒小技巧：一键生成get和set的方法==>点击Sourse->Generate Getters And Setters->勾选相关private属性->生成



#### 3.4 封装

将对象的 **属性 **和 **行为** 封装起来，它的载体就是类。通过 **访问权限控制符** 对不可信的类进行信息隐藏。封装之后就如同一个黑盒子。就像我们玩电脑游戏，我们只需要敲击键盘就可以进行操作，而不用知道游戏背后代码的运行细节，这一特点最大的优势就是便于拓展。

封装时，程序员可以选择那些属性方法是对外公开的，哪些属性，方法是隐藏的，我们通过访问权限控制符，可以控制这些属性，方法是否对其他的类可见。

例如：public，default 关键字就是合理暴露，使外部程序能直接访问属性或方法



##### 小总结

![](https://images.gitee.com/uploads/images/2020/0413/194830_d2adc08e_5550632.png)

第一层的封装就是通过**private**进行封装，第二层的封装，就是通过**空缺**，**protected**，在包的级别上进行封装。



#### 3.5 继承、接口和抽象类

客观世界中，同类的事物既有**共性**又有**特性**，比如，学生和老师都是人，他们都有年龄，姓名，所属学校，但是学生的特性是学号，行为是考试，而老师的特性是工号，行为为批改试卷。

面向对象的一大优点就是继承特性，不仅可以减少代码冗余，同时也可以减少代码更新时所产生的成本。那什么是继承呢？自然语言描述的话就是:**子承父业，父亲的一切都会继承给儿子**。

> 1) 子类继承父类成员变量
>
> 2)  子类从父类继承方法，使子类具有父类相同的行为

继承需要符合“一般->特殊”的关系，**is-a**，父类更通用。比如说公交车是交通工具，但不能反过来说。

类 B (具体类/特殊类) 继承了类 A (一般类)，我们称 类A 为**父类(超类，基类)**，类 B 为**子类（派生类）**。

下面让我们看一个例子：

```java
public class Man
{
    double height,weight;
    public void eat()
    {
        
    }
    public void hunt()//打猎
    {
        
    }
}

public class Woman
{
    double height,weight;
    public void eat()
    {
        
    }
    public void cook()//做饭
    {
        
    }
}
```

上面的两个类，无论男性还是女性都有共同的特征和行为，即身高，体重和吃饭。我们将其抽象成人类。**从很多类别中提取共同点就形成了父类，而子类只要继承它，就会有父类的特点(非private成员)**，继承关系就像是族谱，可以通过画出继承树的方式理清关系。

![](https://images.gitee.com/uploads/images/2020/0425/175323_a5df323f_5550632.png)

```java
public class Human
{
   double height,weight;
    public void eat()
    {
        
    }  
}

public class Man extends Human//继承语法
{
    public void hunt()
    {
        
    }
}

public class Woman extends Human
{
    public void cook()
    {
        
    }  
}
```

继承语法：

> 【修饰符】class 子类名 **extends** 父类名

##### 继承的注意事项

1. 子类和父类要是有重复的属性和方法，优先使用子类的(本身的)。

2. **单根继承原则: 和c++，Python不同，Java中的类只能继承一个类**。**哪怕不写 extends Java类也会默认继承java.lang.Object类**。

3. 子类在继承父类时，私有成员属于**隐式继承（不能在子类中直接访问）**。

![](https://images.gitee.com/uploads/images/2020/0425/175244_f95beee8_5550632.png)

4. 调用子类构造方法一定调用父类的构造方法（默认无参构造方法），以确保父类对象先实例化，再实例化子类对象，**先有祖先，再有子孙**。

5. 子类继承了父类的所有方法，但子类可以重新定义一个**名称，参数相同**都和父类一样的方法，这种行为叫做**重写/覆盖(overwrite/overide)**。**子类方法的优先级大于父类**。而且方法重写时，**子类中方法的访问权限不能小于父类的访问权限**。

   

##### super 关键字

super关键字的作用：

> 1. 使用父类中被覆盖的成员变量
> 2. 调用fu类中被重写的成员方法
> 3. **调用父类的构造方法**

如果子类构造方法没有显示地调用父类的构造方法，那么编译器会自动为它加上一个**默认的无参的super()方法调用**。构造函数内只能有一句super()语句且必须在第一句的位置上。

```java
package test;

public class B
{
	public B()
	{
		System.out.println("我是B类的无参构造函数!");
	}
	public B(int num)
	{
		System.out.println("我是B类的有参构造函数!参数为 " + num);
	}
}

public class A extends B
{
	public A()
	{
		System.out.println("我是A类的无参构造函数!");
	}
	
	public A(int num)
	{
		System.out.println("我是A类的有参构造函数!参数为 " + num);
	}
	
	public static void main(String[] args)
	{
		// TODO Auto-generated method stub
		A a = new A();
		System.out.println("====================");
		A b = new A(10);
	}

}

```

![](https://images.gitee.com/uploads/images/2020/0115/200711_4def567d_5550632.png)

在分割线之上，我们new了一个A类的对象，由于A继承了B，所以先执行了父类B的无参构造函数super()【编译器默认生成的】，所以是这样的效果。然而，在对A进行有参实例化时，由于我们没写super()方法，编译器依旧默认使用无参构造函数，很有可能出错导致会出现分割线之下的情况。

![](https://images.gitee.com/uploads/images/2020/0115/203007_2a25c2c2_5550632.png)

![](https://images.gitee.com/uploads/images/2020/0425/180016_3fed0469_5550632.png)

PS:一定要想好子类使用父类的哪个构造方法。

规范写法如下:

```java
package test;

public class B
{
	public B()
	{
		System.out.println("我是B类的无参构造函数!");
	}
	public B(int num)
	{
		System.out.println("我是B类的有参构造函数!参数为 " + num);
	}
}

public class A extends B
{
	public A()
	{
		super();
		System.out.println("我是A类的无参构造函数!");
	}
	
	public A(int num)
	{
		super(num);//使用父类的有参构造函数
		System.out.println("我是A类的有参构造函数!参数为 " + num);
	}
	
	public static void main(String[] args)
	{
		// TODO Auto-generated method stub
		A a = new A();
		System.out.println("====================");
		A b = new A(10);
	}

}

```

我们再看一个例子：

```java
package secondpackage;
//父类
public class Person {
	private int age;
	private String name;
	public String address = "霍格沃兹";
	Person(){
		
	}

	Person(String name,int age){
		this.name = name;
		this.age = age;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	
	public String getInfo() {
		return "name: "+this.name +" "+",age: " + this.age;
	}
}


//子类
public class Student extends Person {
	
	private String className;
	public Student(String name,int age,String className) {
		super(name,age);//调用父类的构造方法
		this.className = className;
	}
	public String getClassName() {
		return className;
	}
	public void setClassName(String className) {
		this.className = className;
	}
	public String getStudent() {
		return this.getInfo() + ",班级： " + this.className;//由于继承父类中有getInfo方法
	}
	
}


//主类
class Test {

	public static void main(String argv[]) {
		Student stu = new Student("阿斯蒂芬",18,"国学");
		System.out.println(stu.getStudent());
		System.out.println(stu.address);//父类的公共成员变量可以被子类对象访问
	}

}

```

![](https://images.gitee.com/uploads/images/2020/0425/191427_57e9839e_5550632.png)

##### 抽象类和接口

类里面有属性和方法，一个正常的类中方法都是已经实现的，类可以没有方法，但是一旦拥有方法就应该实现，那些**有方法却没有具体实现的类就要定义成抽象类**。用**关键字abstract**声明

```java
public abstract class Shape
{
    /*这是一个图形类，然而图形未知*/
    double area;
    public abstract void calculateArea();
    /*这个方法想计算面积，显然，未知图形无法使用公式进行计算，无法写出具体实现*/
}
```

抽象类的构成:**成员变量，具体方法，抽象方法(abstract)**

**抽象类是无法new的。**

**抽象类也是类，也可以继承，一个类继承于抽象类，就不能继承其它的(抽象)类。**

**抽象类和抽象方法不能用final修饰**

**抽象类不能用private修饰**

只有将方法全都实现后，才能摆脱abstract这种状态。

```java
package test;

public abstract class Shape
{
	double area;
	public Shape()
	{
		
	}
	public abstract void calculateArea();
}


package test;

public class Matrix extends Shape
{
	double width,length;
	public Matrix(double width,double length)
	{
		super();
		this.width = width;
		this.length = length;
	}
	
	public void calculateArea()
	{
		System.out.println("Area is " + (this.width*this.length));
	}
	
	public static void main(String[] args)
	{
		Matrix m = new Matrix(4.5,3.5);
		m.calculateArea();
	}

}

```

如果一个类里的**所有方法都没有实现**，就变成了**接口（interface）**，它是一种“特殊”的类。


PS：接口里面可以定义变量，但一般是常量。

```java
public interface Animal
{
    public void eat();
    public void move();
    public void sleep();
}
```

类只能**继承(extends)一个类**但是却可以**实现(implements)多个接口**。

接口的意义在于：

> 1. 解决Java不能多继承的问题
> 2. 描述系统对外开放的服务，本身不负责任何实现，可以把接口理解成一种规范

Java 8 后，接口中可以声明静态变量，静态方法，抽象方法，内部类，枚举定义和内部类接口……

1. 接口中的成员变量默认是 **public static final** 型的
2. 接口中的方法默认是**public abstract** 型的，编译后也产生.class文件
3. 接口中不能有构造函数

声明方式：

```java
public intereface ...
{
	
}
```

![](https://images.gitee.com/uploads/images/2020/0518/173532_e42ad47c_5550632.png)

例1

```java
package test2;

public interface Animal//一个接口，里面的方法全都没有实现
{
	public void eat();
	public void move();
}


public class Cat implements Animal//Cat类实现了这个接口
{
	public void move()//把接口中没有实现的方法补全
	{
		System.out.println("Cat : I can move ");
	}
	public void eat()
	{
		System.out.println("Cat : I can eat");
	}
}

```

例2

```java
package test2;

public interface ClimbTree//爬树接口
{
	public void climb();
}

public abstract class LandAnimal implements Animal//陆生动物抽象类实现了动物接口
{
	public abstract void eat();//陆地生物吃什么的都有，无法实现，是抽象方法
	public void move()
	{
		System.out.println("I can walk by feet");
	}
}

public class Rabbit extends LandAnimal implements ClimbTree
{
    /*兔子类继承了陆生动物抽象类，实现了爬树接口*/
	public void climb()
	{
		System.out.println("I'm rabbit,I can climb tree");
	}
	
	public void eat()
	{
		System.out.println("Rabbit : I eat plants");
	}

	public static void main(String[] args)
	{
		// TODO Auto-generated method stub

	}
}

```

例3

```java
package test2;

public interface CatFamily extends ClimbTree,Animal
{
	/*接口可以继承多个接口*/
}


public class Tiger implements CatFamily
{
	public void climb()
	{
		System.out.println("Tiger:climb");
	}
	
	public void move()
	{
		System.out.println("Tiger:move");
	}
	
	public void eat()
	{
		System.out.println("Tiger:eat");
	}
	
	public static void main(String[] args)
	{
		// TODO Auto-generated method stub

	}

}

```

![](https://images.gitee.com/uploads/images/2020/0115/214958_8f3136c8_5550632.png)

抽象类实现接口时，可以只重写一部分接口方法。



#### 3.6 转型、多态和契约设计

##### 3.6.1 转型

普通变量转型

```java
int num = (int)3.14159;
```

在**有继承关系**的类中，可以进行转型。由于子类是具体的，父类是抽象的，所以我们可以将子类转型成父类即**从具体到抽象，向上转型**，反过来是不行的【有特例，**向下转型**】。

![](https://images.gitee.com/uploads/images/2020/0116/125349_fecdad70_5550632.png)

上图第7行，将Man类转化成了其父类Human(实例化了Man类，将其转型成了Human类)，这是合法的，反过来写，第8行是不合法的。

```java
package test3;

public class Man extends Human
{
	public static void main(String args[])
	{
		Human m1 = new Man();//当对象本身就是来源子类时
		Man m2 = (Man) m1;//可以将父类转成子类
	}
}

```

![](https://images.gitee.com/uploads/images/2020/0525/163454_a759a084_5550632.png)

##### 3.6.2 多态

多态：$\color{red}{字面理解就是,"多种状态"}$，这多种状态怎么体现出来的呢？第一个就是我们最熟悉地**函数重写了**，当不同子类继承父类的时候，父类方法会被重写，这就导致了，一个函数有两种状态。

类型转换，带来的结果也是多态。它意味着，一个抽象类或一个接口，会有多种实现。

```java
package test3;

public class Human
{
	public void eat()
	{
		System.out.println("I can eat");
	}
}

public class Man extends Human
{
    public void hunt()
    {
        System.out.println("I can hunt");
    }
    
	public void eat()//Man继承Human，Man类重写了Human中的eat()方法
	{
		System.out.println("I can eat more!");
	}
	
	public static void main(String args[])
	{
		Man obj1 = new Man();//实例化Man对象obj1
		obj1.eat();
		Human obj2 = (Human) obj1;//转型为Human
		obj2.eat();
		Man obj3 = (Man) obj2;
		obj3.eat();
	}
}

```

![](https://images.gitee.com/uploads/images/2020/0116/133118_8ecf59c2_5550632.png)

图中，第17行，实例化了一个Man类的对象obj1，18行的eat()毋庸置疑，使用的是Man.eat()。

19行开始转型，**由Man类型的obj1**强制转换成Human类型的obj2，obj1本身就是Man类型，由于**多态性**所以它的**方法被重写**，基于它而转型的obj2，自然使用了重写后的方法，即Man.eat()。

21行将Human类型的obj2转型成Man类型的obj3(为什么能将父类转化成子类?因为它本身就是从Man实例化出来的啊。)，毫无疑问，obj3是Man类，由于多态性使eat方法重写，调用的依旧是Man.eat()

![](https://images.gitee.com/uploads/images/2020/0116/135241_931b5538_5550632.png)

**调用的方法是基于对象的**，由上图可知obj1,obj2,obj3在内存中完全指向同一个东西，所以调用的都是Man.eat()

##### 多态的作用

1. 用统一的接口来操作某类中不同实例化对象的动态行为。

2. 对象之间解耦合。

   ```java
   package test3;
   
   public interface Animal
   {
   	public void eat();
   	public void move();
   }
   
   public class Cat implements Animal
   {
   	public void eat()
   	{
   		System.out.println("Cat : I can eat");
   	}
   	
   	public void move () 
   	{
   		System.out.println("Cat : I can move");
   	}
   }
   
   public class Dog implements Animal
   {
   	public void eat()
   	{
   		System.out.println("Dog : I can eat");
   	}
   	
   	public void move () 
   	{
   		System.out.println("Dog : I can move");
   	}
   }
   
   
   public class AnimalTest
   {
   	public static void main(String[] args)
   	{
   		// TODO Auto-generated method stub
   		Animal [] arr = new Animal[4];//声明数组
   		arr[0] = new Cat();//Animal arr[0] = new Cat();
   		arr[1] = new Dog();
   		arr[2] = new Cat();
   		arr[3] = new Dog();
   		for(int i = 0;i<arr.length;i++)
   		{
   			arr[i].eat();
               /*Animal自身的eat方法是空的，不可能调用，所以是对象自己的eat方法
               　即，通过统一的接口来操纵一个类中的不同对象的动态行为
               */
   		}
           for(int i = 0;i<arr.length;i++)
   		{
   			haveWalk(arr[i]);
   		}
           haveWalk(new Cat());//进行了转型 Animal an = new Cat();
   	}
       
       public static void haveWalk(Animal an)
   	{
   		an.move();
   	}
   }
   
   
   ```

   ##### 3.6.3 契约设计

   契约:规定规范了对象应该包含的行为方法(接口)。

   类不会直接使用另一个类，而是通过接口的形式，统一进行使用。将调用类和被调用类解耦。

   ![](https://images.gitee.com/uploads/images/2020/0116/150653_08613cfc_5550632.png)

PS:接口中的方法都是空的，但是实现(implements)接口的类必须实现接口中的所有方法，这就保证了在统一操作时，可以基于多态的特性，使用对象本身的方法。



### Part 4 Java 关键字

#### 关键字 static

英文原意:静态的，不变的，恒定的

**存在的意义：方便在没有创建对象的情况下来进行调用**

应用场景:

1. 修饰变量
2. 修饰方法(函数)
3. 修饰类
4. 修饰匿名代码块

最常见的就是

```java
public static void main(String args[])
{
    
}
```

它的作用是什么呢?

当一个类里很多个对象的属性需要修改，通过**static**就可以轻松改变，所有对象的属性。

##### static 变量

```java
package test4;

public class Recipe
{
	static int price = 5;
	String name = "";
	public Recipe(int price,String name)
	{
		this.price = price;
		this.name = name;
	}
	public static void main(String args[])
	{
		
		Recipe r1 = new Recipe(10,"西红柿炒鸡蛋");
		System.out.println("对象r1的price:" + r1.price);
		System.out.println("类Recipe的price:" + Recipe.price);
		System.out.println("=============================");
		Recipe r2 = new Recipe(20,"黄瓜炒鸡蛋");
		System.out.println("对象r2的price:" + r2.price);
		System.out.println("类Recipe的price:" + Recipe.price);
		System.out.println("r1和r2指向的price是相同的吗?" + (r2.price == r1.price));
		System.out.println("r1和Recipe指向的price是相同的吗?" + (r1.price == Recipe.price));
		System.out.println("r2和Recipe指向的price是相同的吗?" + (r2.price == Recipe.price));
		
	}
}

```

```java
/*
对象r1的price:10
类Recipe的price:10
=============================
对象r2的price:20
类Recipe的price:20
r1和r2指向的price是相同的吗?true
r1和Recipe指向的price是相同的吗?true
r2和Recipe指向的price是相同的吗?true
*/
```

结论：r1和r2，和类的price(静态变量)，实际上指向了一块相同的内存地址。

##### static 关键字修饰变量时的特点

static关键字只依赖于类存在。即，无论实例化多少个对象，他们具有static关键字的相同属性在内存中存储在同一块内存中。

![](https://images.gitee.com/uploads/images/2020/0415/155643_478e7542_5550632.png)

##### static 方法

**静态方法可以直接通过类名进行使用(非静态方法只能对象进行调用)**，**规定：静态方法中只能使用静态变量，静态方法只能调用静态方法**

```java
package test4;

public class Greet
{
	public static void hello()
	{
		System.out.println("hello");
	}
	
	public void hi()
	{
		System.out.println("hi");
	}
	
	public static void main(String[] args)
	{
		// TODO Auto-generated method stub
		Greet obj = new Greet();
		
		obj.hi();
		obj.hello();
		System.out.println("================");
		Greet.hello();
		Greet.hi();//报错:Cannot make a static reference to the non-static method hi() from the type Greet
	}
}

```

上述代码报错，报错原因是:从类Greet中,不能对非静态方法hi(),进行静态调用。前一句话，QED。

```java
package test4;

public class Greet
{
	static String str = "11111111";
	String str2 = "22222222222";
	public static void hello()
	{
		System.out.println("hello");
		System.out.println(str);
		System.out.println(str2);//报错：Cannot make a static reference to the non-static field str2

	}
	
	public static void main(String[] args)
	{
		Greet.hello();
	}

}

```

上述代码报错，报错原因是:对于非静态属性str2，不能进行静态引用。后一句话的前半句，QED。

**总结**

> 1. 静态方法（类方法）可以通过**类名**或**对象名**访问，但非静态方法（实例方法）只能通过对象访问
> 2. 静态方法可以调用静态方法，但不可以调用非静态方法
> 3. 非静态方法可以调用静态方法
> 4. 用**static**修饰的变量叫类变量或**静态变量**，没有static修饰的叫实例变量

![](https://images.gitee.com/uploads/images/2020/0415/160356_2c876618_5550632.png)



##### static 类

使用机会很少，暂时忽略不计。

##### 代码块

###### static 代码块

```java
package test4;

public class StaticBlock
{

	public StaticBlock()
	{
		/*构造函数*/
		System.out.println("我是构造函数1111111111");	
	}
	
	{
		System.out.println("我是匿名代码块2222222");
	}
	
	{
		System.out.println("我是匿名代码块3333333");
	}
	
	static {
		System.out.println("我是static匿名代码块444444");
	}
}

```

代码块就是没有名称的方法，而静态匿名代码块，就是加了static修饰符的代码块。

```java
static{


}
```



```java
package test4;

public class StaticBlockTest
{

	public static void main(String[] args)
	{
		System.out.println("开始测试1");
		StaticBlock obj= new StaticBlock();
		System.out.println("开始测试2");
		StaticBlock obj2= new StaticBlock();
	}
}

```

```java
/*
运行结果如下

开始测试1
我是static匿名代码块444444
我是匿名代码块2222222
我是匿名代码块3333333
我是构造函数1111111111
开始测试2
我是匿名代码块2222222
我是匿名代码块3333333
我是构造函数1111111111
*/
```

关于static 代码块的结论：

1. static代码块只会被执行一次
2. 优先级关系  static代码块  >  匿名代码块  >  构造函数
3. static代码块中只能访问静态成员变量，普通匿名代码块可以访问静态成员变量或非静态成员



###### 匿名代码块

它也是类体成员，其实你已经见过它了，就是上面哪个不带static关键字的代码块

```java
{


}
```



不建议使用代码块，容易让人混淆。至此，Java实例化对象的过程就彻底清晰了。

![](https://images.gitee.com/uploads/images/2020/0415/164503_f1c89158_5550632.png)



##### 单例设计模式(单态模式)

设计模式：用于解决在特定环境下，重复出现的，特定问题的解决方案。【起源于建筑行业】

作用：保证一个类只有一个对象。

如何保证:

1. 采用**static关键字**共享对象实例。【引用同一内存空间】
2. 采用**private**构造函数，防止外界new操作。【禁止外界实例化该类的对象】

```java
package test4;

public class Test
{
	private static Test obj = new Test();
	private static String content;
	private Test()
	{
		this.content = "abc";
	}
	
	public static Test getInstance()
	{
		return obj;
	}
	
	public String getContent()
	{
		return content;
	}

	public void setContent(String content)
	{
		this.content = content;
	}

	public static void main(String args[])
	{
		Test obj1 = Test.getInstance();
		System.out.println("obj1 content>>>: "+obj1.getContent());
		Test obj2 = Test.getInstance();
		System.out.println("obj2 content>>>: "+obj2.getContent());
		obj2.setContent("definition");
		System.out.println("obj1 content>>>: "+obj1.getContent());
		System.out.println("obj2 content>>>: "+obj2.getContent());
		System.out.println("obj2 == obj1? : "+(obj1 == obj2));
	}
}

```

```java
/*
运行结果:
obj1 content>>>: abc
obj2 content>>>: abc
obj1 content>>>: definition
obj2 content>>>: definition
obj2 == obj1? : true
*/
```

&emsp;暂且不看类内部的内容，直接看主函数。29行通过getInstance方法获得了对象【没有使用new进行实例化】，随后拿到内容abc，接着如法炮制，获得obj2，两个内容是一样的。随后**调用方法更改obj2的content**，发现obj1的值也改了。猜测，此二者同出而异名，最终的对象比较确实告诉了我们，这两个对象是在内存中是同一个东西。

单例模式和之前有什么区别？

1. 实例化的方式变了，外界无法调用该类的构造函数
2. 通过**static**共享内存，使得无论该类有多少个不同名的对象，最终都引用同一块内存空间

第5行，在类内部定义了一个静态变量，这个变量就是该类的对象，同时定义了一个静态方法getInstance，该方法返回这个类的对象【obj】，这个对象只有一个就是obj。又由于进行了private约束，导致这个对象只能在类内存在一个，在外界是无法new出来的。

当你企图new时，会报如下错误:【构造函数不可见】

![](https://images.gitee.com/uploads/images/2020/0120/184627_49b6a633_5550632.png)

外部不让new，内部只new了一次，就变成了**单例设计模式**。【在数据共享中有着重要的应用】



##### 对象数组

数组的元素类型是对象类型，由于对象是引用型数据类型，所以必须需要实例化，即**new**

使用对象数组分为两步：

> 1. 定义对象数组
> 2. 实例化对象数组元素

```java
//定义对象数组
类名[] 数组名 = new 类[数组长度] 
//实例化对象数组
数组名[下标] = 对象名/new 构造方法();
```





#### 关键字final

英文原意：不可更改的，决定性的，最终的

在 Java 中又称：**完结器**，感觉很像 C++ 的 **const**。

应用场景：

1. 修饰类
2. 修饰方法
3. 修饰字段

特性：

**1. final的类，不能被继承 **。

**2.父类中有final方法，子类不能重写【改写】此方法**。

**3.final的基本型变量【int,float】，不能再次赋值,若是对象实例，不能修改其引用（但是可以修改引用内部的值）**。

![](https://images.gitee.com/uploads/images/2020/0120/190316_3190e5f1_5550632.png)

特性1，QED。

```java
public class FinalFather
{

	final public void helloWorld()
	{
		System.out.println("hello world from FinalFather class");
	}
}

public class FinalTest extends FinalFather
{
	
	public void helloWorld()
	{
		System.out.println("hello world from FinalTest class");
	}
	
	public static void main(String args[])
	{
		
	}
}

```

![](https://images.gitee.com/uploads/images/2020/0120/192558_09df559b_5550632.png)

特性2，QED。

特性3，图示：

![](https://images.gitee.com/uploads/images/2020/0120/193954_2925aaf8_5550632.png)

引用固定了，但是引用里的值可以改变。

final 修饰的静态变量，必须赋值且不可更改

```java
final static int MAX_NUM = 100;
```



## Part 5 对象之间的关系

在 Java中，不同对象之间存在**横向**和**纵向**两种关系。

纵向关系包括：

>  1.继承 (extends)
>
>  2.实现 (implements)

横向关系包括：

> 1. 依赖关系
> 2. 关联关系
> 3. 聚合关系
> 4. 组合关系

### 5.1 对象间依赖关系

![](https://images.gitee.com/uploads/images/2020/0511/181226_1a2034bd_5550632.png )

例如，人用手机发短信，其中人是一个对象，手机是一个对象。

依赖关系在UML中采用**虚线箭头**表示。箭头终点表示依赖对象。

```java
public class Mobile {
	public String brand;
	public Mobile() {
		
	}
	public Mobile(String brand) {
		this.brand = brand;
	}
	
	public String editMsg(String msg) {
		return " “ "+msg+" ”的短信";
	}
}

```

```java
public class Person {
	public String name;
	public Person() {
		
	}
	public Person(String name) {
		this.name = name;
	}
	public void sendMsg(Mobile phone,String msg) {
		System.out.println(this.name + "使用了"+phone.brand+"发送了"+phone.editMsg(msg));
	}
}

```

```java
public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Person p = new Person("李华");
		Mobile phone = new Mobile("小米 10");
		p.sendMsg(phone, "今天放假。");
	}

}

```

其中 Person 中的 sendMsg 方法**依赖了** Phone 对象。

### 5.2 对象间关联关系

![](https://images.gitee.com/uploads/images/2020/0511/185743_b7d13927_5550632.png)

关联关系是一种**强依赖关系**，例如，学生老师，司机汽车……

在UML图中使用**实线箭头**来表示，箭头终点是关联对象。

这种关系是平等且长久的。还是**人和手机**，只要在代码层面进行修改，它们的关系就变了：

```java
public class Mobile {
	private String brand;
	public Mobile() {
		
	}
	public Mobile(String brand) {
		this.brand = brand;
	}
	
	public String getBrand() {
		return brand;
	}
	public void setBrand(String brand) {
		this.brand = brand;
	}
	public String editMsg(String msg) {
		return msg;
	}
}
```

```java
public class Person {
	private String name;
	private Mobile phone;
	public Person() {
		
	}
	public Person(String name,Mobile phone) {
		this.name = name;
		this.phone = phone;
	}
	public void sendMsg(Person other,String msg) {
		System.out.println(this.name + "使用了"+phone.getBrand()+" 给 "+other.name+"发送了-->"+phone.editMsg(msg));
	}
}
```

```java
public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Mobile phone = new Mobile("小米 10");
		Mobile phone2 = new Mobile("小米 8");
		Person p = new Person("李华",phone);
		Person p2 = new Person("张三",phone2);
		
		p2.sendMsg(p, "你好,我是法外狂徒张三!");
	}

}
```

我们让 Moblie 对象成为了 Person对象的一部分，使得它们**在代码层面上无法分割**。

### 5.3 对象间聚合关系（Aggregation）

所谓聚合，就是由多个对象聚集在一起进行组合。在生活中，例如：电脑与CPU，球员和球队之间的关系就是聚合关系，它和关联关系很像。在UML中用空心菱形表示。

![](https://images.gitee.com/uploads/images/2020/0513/140236_52b40dab_5550632.png)

![](https://images.gitee.com/uploads/images/2020/0513/140212_4784df88_5550632.png)



### 5.4 对象间组合关系

组合关系也是一种特殊的关联关系，它比聚合关系的关联性更强，整体的生命周期结束后，部分也随之结束。

比如，人有五官，人死了，五官也就无法执行功能了【生命周期结束】，但是缺少一个五官不会让人立刻暴毙。

组合关系在UML图中，采用**实心菱形表示**，箭头始点是部分，终点是整体。

![](https://images.gitee.com/uploads/images/2020/0513/140935_59ae8fed_5550632.png)

![](https://images.gitee.com/uploads/images/2020/0513/141050_f959291e_5550632.png)

![](https://images.gitee.com/uploads/images/2020/0513/141110_b6671cb3_5550632.png)



#### 关键字 instanceof

作用：判断一个对象是否是一个类的实例，有三种情况会返回**true**

> 1. 对象obj 是 类 Class 的对象
> 2. obj 是Class 的直接或间接子类对象
> 3. obj 是 Class接口的实现类的对象

语法如下：

```java
boolean result = obj instanceof Class
```

```java
class Person{};
class Student extends Person implements Fly{};
interface Fly{};

public class Test {

	public static void main(String args[]) {
		Person p = new Person();
		Student stu = new Student();
		System.out.println(stu instanceof Student);
		System.out.println(p instanceof Person);
		System.out.println(stu instanceof Person);	
		System.out.println(p instanceof Student);
		System.out.println(stu instanceof Fly);
		
	}
}

/*
true
true
true
false //父类对象 当然不是 子类的实例
true
*/
```





## Part 6 包

### 6.1 关键字package，import和classpath

&emsp;之前的Java类都是放在同一目录下的，类之间的相互调用关系无需**显式声明调用**。

当程序规模变大时，可能出现的情况：

1. 同一目录下，可能会有有同名文件
2. 文件过多，查找和修改不易**容易出错**

所以，我们要引入一种跨目录放置和调用Java类的方式。

引出关键字**package，import，classpath，jar**



##### package【声明包】

&emsp;和C++的namespace类似【**声明**一个命名空间】，在Java类文件的第一句话写出包的名称。

```java
/*
假设文件路径
	//io/github/daoqi
*/

package io.github.daoqi;
public class PackageExample
{

}
```

包名最好是唯一的，命名方法：

1. 域名是唯一的，因此常用域名作为报名
2. 逆序域名，范围从大到小



##### import【导入包】

&emsp;和C++中的include类似【导入】

```java
/*
	包中代码
*/
package io.github.daoqi;

public class PackageExample
{
	public PackageExample()
	{
		System.out.println("包导入成功，无参构造函数执行成功！");
	}
}

```

```java
/*
	导入时的代码
*/
package test6;
import io.github.daoqi.PackageExample;
public class PackageTest
{
	public static void main(String[] args)
	{
		PackageExample obj = new PackageExample();
		System.out.println("hello world");
		
	}
	
}

```

PS：import可以导入单个类，也可以导入该包下的所有文件，**将PackageExample改成 * 即可**。

使用须知：

1. import必须写在package之后
2. 多个import的顺序可以随意调换
3. 【*】不包括子目录中的文件
4. 不推荐使用【*】，尽量精准导入【同名导入问题】

```java
/*
	原因解释
*/
/*b目录开始*/
package b;

public class Man()
{

}
/*b目录结束*/

/*c目录开始*/
package c;

public class Man()
{
    
}
/*c目录结束*/

/*a目录开始*/
package a;
import c.*;
import b.*;

public class Test()
{
    public static void main(String[] args)
    {
        Man obj = new Man();//到底是b下的Man还是c下的Man啊？？？结果：报错
	}
}
/*a目录结束*/

```



##### 小结

package用来区分class，但是必须和目录层次一致。

import用来导入类，尽量精准地导入。

### 6.2  JFC（Java Foundation Classes）类库

JFC，又称 Java 基础开发类库，里面包含了一些Java基本类，比如：

> java.lang:包含System，String，异常处理Exception，线程控制
>
> java.io:Java的标准输入输出类库
>
> java.util:Java的实用工具类库，Date,Calender，Queue，Random等
>
> java.lang.reflect
>
> java.net：网络编程
>
> java.awt：构建GUI
>
> java.sql：提供访问处理数据库中数据的接口



##### classpath

###### jar机制

&emsp; jar文件，就是一种扩展名叫做jar的文件，是Java所特有的一种文件格式，**用于可执行程序文件的传播**。

本质上，jar文件就是一组class文件的压缩包【不知道.class 文件是什么的请翻倒文章开头】。和

C++的dll文件一样。

jar文件优势

1. jar文件可以包括多个class，比多层目录更加简洁实用
2. jar文件经过压缩，只有一个文件，在网络传输上更具优势
3. jar文件中只包含class文件，因为它是字节码，没法看到具体的类，在保护知识产权和源文件上能起到更好的作用
4. 更容易进行版本控制，一个版本，一个jar

**使用Eclipse的Export功能导出一个jar**

选中项目->顶部菜单File->Export->找到 Java下的 JAR file->勾选要导出的类，在下方写上路径->finish即可。



## Part 7 异常处理

程序运行过程中一定会产生异常，它们大致可以分为以下3类：

![](https://images.gitee.com/uploads/images/2020/0601/174711_c0a70308_5550632.png)



Java提供了一套异常处理机制可以捕获这些异常，按异常被发现的场所，我们分为：

> 1. 编译时异常：文件不存在……
> 2. 运行时异常：数组越界，除以0……

Java所有的异常类都是**java.lang.Throwable**的子类，由它派生出两大异常类：

> 1. 由于系统发生严重错误的Error类
> 2. 程序运行过程中的Exception类



![](https://images.gitee.com/uploads/images/2020/0601/175221_bfae2454_5550632.png)

### 7.1 try/catch/finally 语句捕捉异常

语法格式如下：

```java
try{
    //语句段
}catch(异常类A对象 a){
    //...
}catch(异常类B对象 b){
    //...
}catch(异常类C对象 c){
    //...
}finally{
    //永远会执行，无论有无异常，通常用来释放系统资源
}
```

![](https://images.gitee.com/uploads/images/2020/0601/180618_13ef1524_5550632.png)

利用多态性，我们可以只使用Exception，Error两个异常类，然后通过下列语句进行详细查看：

![](https://images.gitee.com/uploads/images/2020/0601/181206_ab425c2c_5550632.png)



### 7.2 异常处理使用原则

![输入图片说明](https://images.gitee.com/uploads/images/2020/0601/181407_9fb1ee27_5550632.png )

### 7.3 throws 关键字

我们如果不知道如何处理一个方法的异常时，我们可以throws(抛出) 异常。

语法格式：

```java
[修饰符] 返回类型 方法名(参数列表) throws 异常类A[B,C,...{
	方法体
}
```

注意：

1. throws只是抛出异常不处理，我们一定要让它的调用者try...catch来处理这个异常或者让它调用者接着throws,直到有人处理为止。
2. main 方法是整个程序的入口，它不可以抛出异常。

```java
public class Demo{
	void A() throws SQLException{
		
    }
    
    void B() throws SQLException{
		A();
    }
    void C() throws SQLException{
		B();
    }
    
    public static void main(String args[]){
        try{
			C();
        }catch(SQLException e){
		
        }finally{
            
        }
    }
}
```

#### 7.4 自定义异常

自定义异常类是Exception或RuntimeException的子类，它的固定写法是：

```java
class ... extends Exception{
	public ...(){}//空构造方法
	public ...(String msg){
		super(msg);
	}
}
```

然后通过关键字**throw**抛出。

注意：

> throw 只负责抛出异常，$\color{red}{它必须和try...catch...finally配套使用或者throws连着一起用}$

##### 7.4.1 关键字**throws**和**throw**的区别：

1. throws出现在方法**函数头**，而throw出现在**函数体**。
2. throws表示**出现异常的一种可能性**，并不一定会发生这些异常。throw则是抛出了异常，执行throw则**一定抛出了某种异常对象**。
3. 两者都是消极处理异常的方式（这里的消极并不是说这种方式不好），只是抛出或者可能抛出异常，但是不会由函数去处理异常，真正的处理异常由函数的上层调用处理。换句话说：它们都是那种只抛不管的，所以父调用者才要写try...catch语句来接收处理异常。
   



## Part 8 Object类

Object是所有类的父类。所以所有类都可以调用Object类中的方法：

![](https://images.gitee.com/uploads/images/2020/0610/154824_c4f8c6be_5550632.png )

其中，toString，equals，hashCode需要我们详细学习。

我们直接打印对象时，自动调用toString方法，而且当进行字符串拼接时，也会调用toString方法。但是通常情况下直接打印的结果是这样的：

![](https://images.gitee.com/uploads/images/2020/0610/155226_e6734534_5550632.png)

@后面是一个哈希码，然而并没有什么实际的意义，所以我们要重写toStirng方法。

```java
public class People {
	String name;
	String sex;
	int age;

	public People() {

	}

	public People(String name, String sex, int age) {
		super();
		this.name = name;
		this.sex = sex;
		this.age = age;
	}
	
	public String toString() {
		return "name :"+this.name+" gender: "+this.sex+" age : "+this.age;
	}
}


public class Test {

	public Test() {
		
	}

	public static void main(String[] args) {
		
		People p1 = new People("zzh","女",18);
		People p2 = new People("zzh","女",18);
		System.out.println(p1);
		System.out.println(p2);
	}

}

```

新的运行结果：

![](https://images.gitee.com/uploads/images/2020/0610/161427_3a200c74_5550632.png)

### 8.1 对象之间的关系

**对象相等**：当两个对象具有相同类型和属性时它们是相等的

**对象同一**：当两个引用对象指向同一个对象时，这两个对象同一

Object类下的equals方法是来判断两个对象$\color{red}{是否同一}$的，而不是相等。

![](https://images.gitee.com/uploads/images/2020/0610/160159_690758c0_5550632.png )

为了能判断两个对象是否相等，此时我们要重写equals方法

```java
public class People extends Object{
	String name;
	String sex;
	int age;

	public People() {
		
	}

	public People(String name, String sex, int age) {
		super();
		this.name = name;
		this.sex = sex;
		this.age = age;
	}

	public void eating(String food) {
		System.out.println(this.name + "is eating");
	}
	
	
	public String toString() {
		return "name :"+this.name+" gender: "+this.sex+" age : "+this.age;
	}
	
	public boolean equals(Object obj) {
        if(! (obj instanceof People)) {
        	return false;
        }
        People per = (People) obj;
        //哈希值相同，一定是同一个对象
        if(per == this) return true;
        if(per.name.equals(this.name) && per.sex.equals(this.sex) && per.age == this.age) {
        	return true;
        }
        return false;
        
    }
}


public class Test {

	public Test() {
		// TODO Auto-generated constructor stub
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		People p1 = new People("zzh","女",18);
		People p2 = new People("zzh","女",18);
		People p3 = new People("zzh","男",20);
		System.out.println("两个对象的地址是否相同："+(p1==p2));
		System.out.println("两个对象的name是否相同："+(p1.name.equals(p2.name)));
		System.out.println("两个对象的是否相同：" + p1.equals(p2));
		System.out.println("两个对象的是否相同：" + p1.equals(p3));
	}
}

```

运行结果：

![](https://images.gitee.com/uploads/images/2020/0610/162520_998fa545_5550632.png)

##### hashcode函数

每个对象都有一个hash值，它可以用来判断两个对象是否相等，例如：

![](https://images.gitee.com/uploads/images/2020/0610/160858_8830bba8_5550632.png)

hashCode函数返回的是10进制哈希值

![](https://images.gitee.com/uploads/images/2020/0610/160528_ce906379_5550632.png )

**hashCode和equals**

hashCode按照哈希表来理解，Java 会根据对象调用哈希函数得到哈希值，一般而言相同哈希值的对象应该是以链表形式组织的，就像下图这样：

![](https://bkimg.cdn.bcebos.com/pic/c9fcc3cec3fdfc035f8e2b9cd63f8794a4c22624?x-bce-process=image/watermark,g_7,image_d2F0ZXIvYmFpa2U4MA==,xp_5,yp_5)

equals 咱们先看没重写过的源代码：

![](https://images.gitee.com/uploads/images/2020/0619/114758_2e7b4543_5550632.png)

它在比较两个对象的引用是否相同。

重写之后的equals会根据你自定义的属性进行比较，直接比较内容而不是引用。

所以，**无论equals还是hashCode是否重写，equals和hashCode这两个函数本来就是两个不同的东西，没有依赖性。**

由于哈希表的特性，每一个引用不同的对象应该独自占用一个哈希值，**当equals没有改动时，a.equals(b)和a.hashCode() == b.hashCode()是等价的**，当你重写equals之后，本来两个引用不同的对象反而会返回true，此时你的哈希函数也应该返回的是同一个值。

总结：

重写equals之后要重写hashCode这是一种标准。源码里是这样写的：

![](https://images.gitee.com/uploads/images/2020/0619/113434_3cd0b038_5550632.png)

规范就是，hashCode和equals返回值要稳定，两个对象==equals应该返回true，两个equals的对象hashCode应当相等。要保证内容相等的对象，hash值也相同。

<br>

## Part 9 其它常用类-不定期更新

### 9.1 Java 可视化编程

#### 9.1.1 基本概念

&nbsp;&nbsp;在本节，我将明确JAVA GUI编程的一些基本概念与框架。

在Java的可视化编程中，我们常用如下两个包：

> java.awt
>
> java.swing

它们包含了基本的**窗体**和**组件**。

#### 窗体是什么？

窗体，可以简单理解为一个容器，用于盛放组件的容器。通常我们用 JFrame 类来表示。

#### 组件是什么？

组件就是一个窗体里所具有的，可以以显示或隐式和用户进行交互的对象。比如，按钮，下拉框，文本框等等。

![](https://images.gitee.com/uploads/images/2020/1007/134653_27a9c748_5550632.png)

下图为Java中常用的组件和窗体的继承关系，这也能体现出为什么我们需要引入这两个包

![](https://img.jbzj.com/file_images/article/201711/20171120110340122.png?2017102011351)

<br>

#### 9.1.2 新建窗口(窗体)

```java
package helloGUI;

import java.awt.*;
import javax.swing.*;

public class Test {

	public Test() {
		// TODO Auto-generated constructor stub
	}

	public static void main(String[] args) {
		//新建窗体
		JFrame window = new JFrame("Hello world");
		//设置 位置(int x, int y) 窗口大小(int width, int height)
		window.setBounds(200, 200, 300, 300);
		//固定写法 设置背景颜色
		Container container = window.getContentPane();
		container.setBackground(Color.GREEN);
		//设置可见为真
		window.setVisible(true);
		
	}

}
```

显示效果：

![输入图片说明](https://images.gitee.com/uploads/images/2020/1007/135359_80cb1943_5550632.png "屏幕截图.png")

在Java的可视化编程中，一般一个窗口一个类，上述代码中为了方便演示，直接写到了主类中。

JFrame 的构造方法如下：

![输入图片说明](https://images.gitee.com/uploads/images/2020/1007/135913_6b46afe5_5550632.png "屏幕截图.png")

<br>

#### 9.1.3 添加布局和组件

有了窗体之后，我们就可以来向窗体添加组件了。我们仿照Eclipse，来模拟一个简陋的页面(没有实际功能)

```java
package helloGUI;

import java.awt.*;
import javax.swing.*;

@SuppressWarnings("serial")
public class EclipseTest extends JFrame {
	JMenuBar jmenubar;
	JMenu fileMenu,editMenu,sourceMenu,refactorMenu;
	
	public EclipseTest() {
		
	}
	
	public EclipseTest(String title) {
		super(title);
		//this代表当前窗体
		this.menuInit();
		//设置布局为流式布局( 从左向右，从上到下布局)
		this.setLayout(new FlowLayout());
		this.setBounds(200, 200, 500, 500);
		Container container = this.getContentPane();
		container.setBackground(Color.BLUE);
		this.setVisible(true);
		
		
	}
	
	private void menuInit() {
		this.jmenubar = new JMenuBar();
		this.fileMenu = new JMenu("File");
		this.editMenu = new JMenu("Edit");
		this.sourceMenu = new JMenu("Source");
		this.refactorMenu = new JMenu("Refactor");
		
		this.jmenubar.add(this.fileMenu);
		this.jmenubar.add(this.editMenu);
		this.jmenubar.add(this.sourceMenu);
		this.jmenubar.add(this.refactorMenu);
		
		//窗体添加菜单栏
		this.add(jmenubar);
		
	}
	
	public static void main(String[] args) {
		EclipseTest eclipseTest = new EclipseTest("test");
		
	}
}

```

 同一个代码将流式布局注释前后的效果图：

![输入图片说明](https://images.gitee.com/uploads/images/2020/1007/141157_2e4264ab_5550632.png "屏幕截图.png")

<br>

#### 9.1.4 监听事件与响应

 我们刚才可以画出一个丑陋的页面，但是咱们会发现，我们根本无法和组件进行交互，以一个按钮为例，我们希望点击它之后，整个窗体会关闭，那么我们应该如何考虑这个流程呢？

文字描述如下：首先，组件会产生事件(Event) ，如ActionEvents,ChangeEvents,ItemEvents等，来响应用户的鼠标点击行为，列表框中值的改变，计时器的开始计时等行为。然后，我们需要实现对应类型的监听器(Listener)接口中的actionPerformed方法来对该事件进行处理。

图示：

![输入图片说明](https://images.gitee.com/uploads/images/2020/1007/142457_c799b5fe_5550632.png "屏幕截图.png")

看上去还是很抽象对吧，我们通过一个例子来深入理解一下这个过程。

需求如下：

> 设计一个页面，包括两个JButton组件(按钮)
>
> > 按下其中一个背景颜色变红，另一个变蓝

代码如下：

```java
package helloGUI;

import java.awt.*;
//注意要导入 java.awt.event包
import java.awt.event.*;
import javax.swing.*;


@SuppressWarnings("serial")
public class ChangeColorWindow extends JFrame implements ActionListener{
	//定义两个按钮
	JButton redButton;
	JButton blueButton;
	//按钮所产生的事件都是ActionEvents,所以它们两个可以共用一个ActionListener监听器
	
	
	
	public ChangeColorWindow() {
		
	}
	
	public ChangeColorWindow(String title) {
		super(title);
		
		//按钮初始化
		this.buttonInit();
		
		//给窗体添加按钮
		this.add(this.redButton);
		this.add(this.blueButton);
		
		//添加监听器(注意:只有实现了ActionListener接口的类才可以添加)
		this.redButton.addActionListener(this);
		this.blueButton.addActionListener(this);
		
		//添加流式布局
		this.setLayout(new FlowLayout());
		
		//设置窗口基本参数
		this.setBounds(200, 200, 350, 350);
		
		this.setVisible(true);
	}
	
	@Override
	public void actionPerformed(ActionEvent e) {
		
		//Container改变颜色
		Container container = this.getContentPane();
		
		//getSource 方法用来捕获事件产生的对象，进而可以分别控制两个按钮
		if(e.getSource() == this.redButton) {
			container.setBackground(Color.RED);
		}else if(e.getSource() == this.blueButton) {
			container.setBackground(Color.BLUE);
		}
	}
	
	private void buttonInit() {
		this.redButton = new JButton("turn red");
		this.blueButton = new JButton("turn blue");
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		ChangeColorWindow window = new ChangeColorWindow("Change color");
	}

}

```

效果图：

![输入图片说明](https://images.gitee.com/uploads/images/2020/1007/144210_04b0140e_5550632.png "屏幕截图.png")

总结：

> 1. 想进行事件处理必须清楚选用的组件产生的事件类型，如JButton产生的就是ActionEvents类型的事件
> 2. 明确事件类型后，需要选择实现对应事件的监听器，如ActionEvents对应的就是ActionListener接口
> 3. 重写 actionPerformed 方法，以便于给用户呈现出效果

再来一个例子:

> 请通过文本框，下拉框，设计一个具有简单功能的四则运算器（计算器）

```java
package calculator;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.*;
import javax.swing.event.*;


public class Calculator extends JFrame implements ActionListener{

	//定义文本框
	JTextField num1Field,num2Field,resulTextField;
	//定义运算符下拉框
	/*注意:JComboBox本身为泛型类,如果下拉列表中的元素为字符串则最好将其写成 JComboBox<String>
	 *       当然，不写<String>只是警告并“JComboBox is a raw type. 
	 *       References to generic type JComboBox<E> should be parameterized”，
	 *       并不会报错
	 * */
	JComboBox<String> operatorComboBox;
	//定义标签
	JLabel equalLabel;
	
	public Calculator() {
		
	}
	
	public Calculator(String title) {
		super(title);
		
		/*初始化组件*/
		this.JtextFeildInit();
		this.JLabelInit();
		this.JComboBoxInit();
		/*对resulTextField 添加监听器 (也可以对num2Field添加)
		 * 注意：回车，属于点击事件(ActionEvent)，需要实现ActionListener接口
		 * */
		this.num2Field.addActionListener(this);
		this.resulTextField.addActionListener(this);
		
		this.deploy();
		this.setLayout(new FlowLayout());
		this.setBounds(200,200,500,300);
		this.setVisible(true);
	}
	
	/*定义初始化函数-开始*/
	private void JtextFeildInit() {
		this.num1Field = new JTextField(10);
		this.num2Field = new JTextField(10);
		this.resulTextField = new JTextField(10);
	}
	
	private void JLabelInit() {
		this.equalLabel = new JLabel("=");
	}
	
	private void JComboBoxInit() {
		this.operatorComboBox = new JComboBox<String>();
		this.operatorComboBox.addItem("+");
		this.operatorComboBox.addItem("-");
		this.operatorComboBox.addItem("*");
		this.operatorComboBox.addItem("/");
		//与原定需求不符，添加取余和乘方运算
		this.operatorComboBox.addItem("%");
		this.operatorComboBox.addItem("^");
	}
	
	/*定义初始化函数-结束*/
	
	/*定义组件布局函数-开始*/
	private void deploy() {
		this.add(this.num1Field);
		this.add(this.operatorComboBox);
		this.add(this.num2Field);
		this.add(this.equalLabel);
		this.add(resulTextField);
	}
	
	/*定义组件布局函数-结束*/
	
	/*实现actionPerformed方法*/
	@Override
	public void actionPerformed(ActionEvent event) {
		// 该方法目的是获取下拉列表的值，返回值为Object，需要类型强转
		String opString = (String)this.operatorComboBox.getSelectedItem();
		try {
				if(opString.equals("+")) {
					//获取文本框内容并转成double型
					double num1 = Double.parseDouble(this.num1Field.getText());
					double num2 = Double.parseDouble(this.num2Field.getText());
					double res = num1 + num2;
					//呈现结果
					this.resulTextField.setText(Double.toString(res));
				}
				if(opString.equals("-")) {
					//获取文本框内容并转成double型
					double num1 = Double.parseDouble(this.num1Field.getText());
					double num2 = Double.parseDouble(this.num2Field.getText());
					double res = num1 - num2;
					//呈现结果
					this.resulTextField.setText(Double.toString(res));
				}
				if(opString.equals("*")) {
					//获取文本框内容并转成double型
					double num1 = Double.parseDouble(this.num1Field.getText());
					double num2 = Double.parseDouble(this.num2Field.getText());
					double res = num1 * num2;
					//呈现结果
					this.resulTextField.setText(Double.toString(res));
				}
				if(opString.equals("/")) {
					//获取文本框内容并转成double型
					double num1 = Double.parseDouble(this.num1Field.getText());
					double num2 = Double.parseDouble(this.num2Field.getText());
					//呈现结果
					this.resulTextField.setText(String.format("%.2f", num1 / num2));
				}
				if(opString.equals("^")) {
					//获取文本框内容并转成double型
					double num1 = Double.parseDouble(this.num1Field.getText());
					double num2 = Double.parseDouble(this.num2Field.getText());
					double res = Math.pow(num1, num2);
					//呈现结果
					this.resulTextField.setText(String.format("%.2f", res));
				}
				if(opString.equals("%")) {
					//获取文本框内容并转成double型
					double num1 = Double.parseDouble(this.num1Field.getText());
					double num2 = Double.parseDouble(this.num2Field.getText());
					double res = num1 % num2;
					//呈现结果
					this.resulTextField.setText(String.format("%.2f", res));
				}
			
		}catch (Exception e) {
			//考虑到有人喜欢瞎玩程序，防止字母干扰程序的正常执行。这里直接在结果文本框中打出 Error
			e.printStackTrace();
			this.resulTextField.setText("Error !");
		}
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Calculator calculator = new Calculator("Calculator");
	}
}
```

效果图：

![输入图片说明](https://images.gitee.com/uploads/images/2020/1009/185453_202395fa_5550632.png "屏幕截图.png")

<br>

### 9.2 Java 文件处理

#### 9.2.1 File 类

该类是Java对计算机内部的**文件目录**和**文件**的抽象，用于表达一个文件夹或者文件。它拥有以下三种构造方法：

> File(String 路径名)
>
> File(String 路径名,String 文件名)
>
> File(File 文件对象,String 文件名)

源码如下：

```java
public File(String pathname) {
    if (pathname == null) {
        throw new NullPointerException();
    }
    this.path = fs.normalize(pathname);
    this.prefixLength = fs.prefixLength(this.path);
}

public File(String parent, String child) {
        if (child == null) {
            throw new NullPointerException();
        }
        if (parent != null) {
            if (parent.equals("")) {
                this.path = fs.resolve(fs.getDefaultParent(),
                                       fs.normalize(child));
            } else {
                this.path = fs.resolve(fs.normalize(parent),
                                       fs.normalize(child));
            }
        } else {
            this.path = fs.normalize(child);
        }
        this.prefixLength = fs.prefixLength(this.path);
    }

public File(File parent, String child) {
        if (child == null) {
            throw new NullPointerException();
        }
        if (parent != null) {
            if (parent.path.equals("")) {
                this.path = fs.resolve(fs.getDefaultParent(),
                                       fs.normalize(child));
            } else {
                this.path = fs.resolve(parent.path,
                                       fs.normalize(child));
            }
        } else {
            this.path = fs.normalize(child);
        }
        this.prefixLength = fs.prefixLength(this.path);
    }

```

为了避免堆叠方法的学习方式，我们通过例子来进行File类的学习。

> 需求:设计一个交互的GUI页面，可以进行文件检索

Demo流程：

1. 编写一个类进行文件夹和文件的创建。
2. 编写可视化类进行交互。
3. 编写文件查找类进行文件查找

代码及解释如下:

```java
package test;

import java.io.File;
import java.io.IOException;

/*
 * 这个类的目的是新建文件
 * */
public class AddFile {

	public AddFile() {
		// TODO Auto-generated constructor stub
	}

	public static void main(String[] args) {
		File folderFile = new File("D:\\del_test_folder");
		//判断文件夹是否存在,不存在则创建
		if(!folderFile.exists()) {
			folderFile.mkdir();
			String [] filenameStrings = {"a.txt","b.java","c.txt","d.cpp","e.c","f.java","g.cpp","f.txt"};
			
			for(String filename:filenameStrings) {
				//创建文件实例,无则创建,有则删除。
				File file = new File(folderFile,filename);
				if(!file.exists()) {
					try {
						file.createNewFile();
					} catch (IOException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				}else {
					file.delete();
				}
			}
		}else {
			//存在该文件夹,什么也不做.
		}

	}

}
```

效果图：

![输入图片说明](https://images.gitee.com/uploads/images/2020/1028/145124_63effd57_5550632.png "屏幕截图.png")

```java
package test;
/*
 * 该类用于文件搜索
 * */
import java.io.File;
import java.io.FilenameFilter;

public class FileSearch implements FilenameFilter {
	//实现FilenameFilter接口用于文件搜索
	String filenameString;
	public FileSearch(String filenameString) {
		this.filenameString = filenameString;
	}

	@Override
	public boolean accept(File dir, String name) {
		// TODO Auto-generated method stub
		return name.endsWith(this.filenameString);
	}

}

```

```java
package test;

/*
 * 这个类负责GUI
 * */
import java.awt.*;
import java.awt.event.*;
import java.io.*;

import javax.swing.*;

public class Window extends JFrame implements ActionListener {

	JLabel jLabel, jLabel2;
	JTextField jTextField, jTextField2;
	JTextArea jTextArea;
	JButton jButton;

	public Window(String title) {
		super(title);

		jLabel = new JLabel("Directory: ");
		jLabel2 = new JLabel("File name: ");
		jTextField = new JTextField(10);
		jTextField2 = new JTextField(10);
		jTextArea = new JTextArea(10, 10);
		jButton = new JButton("Search");

		this.add(jLabel);
		this.add(jTextField);
		this.add(jLabel2);
		this.add(jTextField2);
		this.add(jTextArea);
		this.add(jButton);

		this.jButton.addActionListener(this);
		this.setLayout(new FlowLayout());
		this.setBounds(200, 200, 150, 350);
		this.setVisible(true);
	}

	@Override
	public void actionPerformed(ActionEvent e) {
		String dirString = this.jTextField.getText();
		File dir = new File(dirString);
		if (dir.exists()) {
			String filenameString = this.jTextField2.getText();
			//调用listFiles方法搜索文件
			File[] filesStrings = dir.listFiles(new FileSearch(filenameString));
			for(File f:filesStrings) {
				this.jTextArea.append(f.getName()+"\n");
			}
		}

	}

	public static void main(String[] args) {
		new Window("Test");
	}

}

```

最终效果图:

![输入图片说明](https://images.gitee.com/uploads/images/2020/1028/150939_9f26e9de_5550632.png "屏幕截图.png")

<br>

#### 9.2.1 文件读写类（输入输出流）

输入输出流按照数据类型可以分为**字节型**和**字符型**。

关于流的方向，这里需要明确一下，$\color{red}{从文件到java为输入，从java到文件为输出}$

##### 字符字节流的类间关系

![](https://img2020.cnblogs.com/blog/1914083/202003/1914083-20200318143838087-1101416263.jpg)

现在我们开始演示，**字节型文件的输入输出**。

输入流 FileInputStream 构造方法（在java.io包中）：

```java
public FileInputStream(String name) throws FileNotFoundException {
    this(name != null ? new File(name) : null);
}

public FileInputStream(File file) throws FileNotFoundException {
    String name = (file != null ? file.getPath() : null);
    SecurityManager security = System.getSecurityManager();
    if (security != null) {
        security.checkRead(name);
    }
    if (name == null) {
        throw new NullPointerException();
    }
    if (file.isInvalid()) {
        throw new FileNotFoundException("Invalid file path");
    }
    fd = new FileDescriptor();
    fd.attach(this);
    path = name;
    open(name);
    altFinalizer = getFinalizer(this);
    if (altFinalizer == null) {
        FileCleanable.register(fd);       // open set the fd, register the cleanup
    }
}
```
FileInputStream Demo:

```java
package test;

import java.io.*;

public class IOTestA {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		try {
			FileInputStream fInputStream = new FileInputStream("D:\\a.txt");
			byte a[] = new byte[50];
			int n = 0;
			while((n=fInputStream.read(a,0,50))!=-1) {
				//n为实际读出的字节数目
				String string = new String(a,0,n);
				System.out.println(string);
			}
			fInputStream.close();//关闭输入流
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

}

```

> 输出结果:  hello world

输出流 FileOutputStream

构造方法和输入流类似。

FileOutputStream Demo:

```java
package test;

import java.io.*;

public class IOTestB {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		FileOutputStream fOutputStream;
		byte a[] = "祝您平安!".getBytes();//字符串转字节数组
		
		try {
			fOutputStream = new FileOutputStream("D:\\b.txt");
			fOutputStream.write(a);
			fOutputStream.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
}
```

![输入图片说明](https://images.gitee.com/uploads/images/2020/1104/160126_f8ad8b95_5550632.png "屏幕截图.png")

<br>

接下来，我们来说说字符型的输入输出流。

FileReader为输入流（读取），FileWriter为输出流（写入），它们的构造方法如下：

```java
public FileReader(String fileName) throws FileNotFoundException {
    super(new FileInputStream(fileName));
}

public FileReader(File file) throws FileNotFoundException {
    super(new FileInputStream(file));
}
```

由源码不难看出，FileReader是FileInputStream的子类。所以其用法也类似，Demo如下：

从a.txt中读，再写入c.txt。

```java
package test;

import java.io.*;

public class IOTestC {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		FileReader readFileReader;
		char c[] = new char[50];//注意:字符型的输入输出的载体是字符
		try {
			readFileReader = new FileReader("D:\\a.txt");
			FileWriter writer = new FileWriter("D:\\c.txt");
			
			int n = -1;
			while((n = readFileReader.read(c))!=-1) {
				writer.write(c,0,n);
			}
			writer.flush();//让系统快速刷入数据
			writer.close();
			readFileReader.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}

}

```

![输入图片说明](https://images.gitee.com/uploads/images/2020/1104/161335_81bd09df_5550632.png "屏幕截图.png")

<br>

#### 9.2.2 缓冲流

从功能上来看，FileReader类很难完成一次读取一行的功能。接下来我们要讲的是缓冲流，**BufferedReader**和**BufferedWrite**

他们的构造方法如下：

```java
public BufferedReader(Reader in) {
    this(in, defaultCharBufferSize);
}

public BufferedWriter(Writer out) {
    this(out, defaultCharBufferSize);
}
```

测试程序及结果如下：

```java
package test;

import java.io.*;

public class BufferedReadTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		FileReader fReader;
		FileWriter fWriter;
		try {
			fReader = new FileReader("D:\\a.txt");
			fWriter = new FileWriter("D:\\b.txt");
			BufferedReader bfReader = new BufferedReader(fReader);//实例化缓冲输入流对象
			BufferedWriter bfWriter = new BufferedWriter(fWriter);
			String string = "";
			while((string = bfReader.readLine())!=null) {//按行读取
				System.out.println(string);
				bfWriter.write(string + " --copied");
				bfWriter.newLine();//在输出文件中写一个换行
			}
			bfReader.close();
			fReader.close();
			bfWriter.close();
			fWriter.close();
			
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

	}

}

```

![输入图片说明](https://images.gitee.com/uploads/images/2020/1109/143548_7c03e0be_5550632.png "屏幕截图.png")

#### 9.2.3 随机流

有的时候我们想对特定的文件位置进行读写操作，或者边读边写，此时就要用到随机流了。

**RandomAccessFile**

构造方法如下：

```java
public RandomAccessFile(String name, String mode)
    throws FileNotFoundException
{
    this(name != null ? new File(name) : null, mode);
}

public RandomAccessFile(File file, String mode)
    throws FileNotFoundException
{
    this(file, mode, false);
}
```

其中，要重点说明一下mode属性，它的取值有4种

1. r:只读
2. rw:可读可写
3. rws:在rw的基础上，要求对文件的内容或元数据的修改同步到底层存储设备上
4. rwd:在rw的基础上，要求对文件的内容的修改同步到底层存储设备上

#### 9.2.4 综合样例



<br>

## Part 10 JSP技术

### 10.1 JSP是什么

**JSP（全称Java Server Pages）**是由Sun Microsystems公司主导创建的一种动态网页技术标准。JSP部署于网络服务器上，可以响应客户端发送的请求，并根据请求内容动态地生成HTML、XML或其他格式文档的Web网页，然后返回给请求者。JSP技术以Java语言作为脚本语言，为用户的HTTP请求提供服务，并能与服务器上的其它Java程序共同处理复杂的业务需求。
JSP将Java代码和特定变动内容嵌入到静态的页面中，实现以静态页面为模板，动态生成其中的部分内容。JSP引入了被称为“JSP动作”的XML标签，用来调用内建功能。另外，可以创建JSP标签库，然后像使用标准HTML或XML标签一样使用它们。标签库能增强功能和服务器性能，而且不受跨平台问题的限制。JSP文件在运行时会被其编译器转换成更原始的Servlet代码。JSP编译器可以把JSP文件编译成用Java代码写的Servlet，然后再由Java编译器来编译成能快速执行的二进制机器码，也可以直接编译成二进制码。

说人话就是：

1. JSP是一种基于C/S架构的动态网页技术
2. JSP的本质是HTML里嵌套Java代码

这种已经过时的技术虽然大厂已经不用，但是作为学生的我们还是需要学习，毕竟无论框架怎么改，过硬的编码能力和扎实的计算机网络基础才是核心，我在想能否通过JSP这种技术敲开我对整个软件设计开发的流程认识的进一步呢？

### 10.2 配置Tomcat和Eclipse

既然JSP是基于一种C/S架构的技术，那么服务器是必须要有的，它就是**Apache-Tomcat**，去官网下载Tomcat，然后让我们看看该配置什么。

[Tomcat 8.0版本链接](https://tomcat.apache.org/download-80.cgi)

首先第一步，遇事不决，设置环境变量。像配置JAVA_HOME那样配置CATALINA_HOME，我的如下：

![](https://images.gitee.com/uploads/images/2020/0621/172744_66987206_5550632.png)



然后让我们看看，Tomcat里有啥

![](https://images.gitee.com/uploads/images/2020/0621/173228_32e24840_5550632.png )

从bin开始说吧：

> bin : Tomcat服务器的一些操作命令，包括启动服务器，关闭服务器等
>
> conf: 服务器配置文件，可以设置服务器的端口，项目的寻找路径等
>
> lib: 里面包含了一些jar包
>
> log: 服务器的日志信息
>
> temp: 一些暂存文件
>
> **webapps**：项目的所属位置

![](https://images.gitee.com/uploads/images/2020/0621/173724_b6c0a819_5550632.png)

默认访问ROOT目录，让我们看看ROOT目录里有什么吧

![](https://images.gitee.com/uploads/images/2020/0621/173914_b3b4b100_5550632.png)

咱们主要看这两个东西，点开WEB-INF，里面有一个**web.xml**,$\color{red}{这个文件每个项目必须要有，它的意义是初始化页面信息的}$。

![](https://images.gitee.com/uploads/images/2020/0621/174228_f54f7d0e_5550632.png )

它用来设置欢迎页，它会通过**<welcome-file-list>**标签去找欢迎页：

```xml
<welcome-file-list>
        <welcome-file> index.jsp</welcome-file>

    </welcome-file-list>
```

注意：

**你所有的JSP代码，不能放在WEB-INF文件夹中，否则会找不到该文件**

看完了项目应该放哪，接下来看看怎么更改Tomcat的端口并设置项目的虚拟路径，以便跨目录访问JSP项目。

**点进conf文件夹找到server.xml**

![](https://images.gitee.com/uploads/images/2020/0621/174918_e62fa40c_5550632.png )

找到这个标签，port默认值为8080，由于端口冲突的问题，我把它改为了8888

为了跨目录访问项目我们有两种设置方式：

1. 在server.xml的host标签中中添加标签(需要重启服务器)

   ```xml
   <Context docBase="..." path="..." />
   ```

   docBase: 项目绝对路径

   path：可以写相对路径（相对于webapps），也可以写绝对路径

2. conf里面的Catalina中新建文件(不需要重启服务器)

   项目名.xml,然后把上面的代码抄一遍

让我们实际地动手部署一个项目吧。

我在桌面上新建了一个文件夹交Demo，作为我的JSP项目目录

配置server.xml

![](https://images.gitee.com/uploads/images/2020/0621/180152_6bc25a85_5550632.png)

启动服务器

![](https://images.gitee.com/uploads/images/2020/0621/180316_cbe636b2_5550632.png)

在浏览器中输入

```
localhost:8888/Demo
```

出现如下欢迎页：

![](https://images.gitee.com/uploads/images/2020/0621/180443_3fa37043_5550632.png)

开发一个项目最好还是要有IDE，我们采用Eclipse作为开发工具，在开始之前呢，需要给Eclipse安装插件，教程链接贴在下方：

[安装插件的教程](https://blog.csdn.net/weixin_41782253/article/details/82744220)

安装完毕之后我们就要新建一个jsp项目，咱们这么玩：

1. 配置Tomcat ，点开windows 搜索runtime

   ![](https://images.gitee.com/uploads/images/2020/0621/181850_643754d4_5550632.png)

2. 选择Apache服务器,并选择你的服务器版本![](https://images.gitee.com/uploads/images/2020/0621/181947_298cd5e9_5550632.png )

3. 设置路径,设置JRE，8.5版本的Tomcat需要JDK1.7及以上，我这里是按我自己的JDK设置的（JDK包括JRE）

![](https://images.gitee.com/uploads/images/2020/0621/182508_1c68e160_5550632.png)



4. Finish Apply and Close

5. 找到下边框的Server，没有的话去Windows里面找视图，再没有可能是插件装少了

   ![](https://images.gitee.com/uploads/images/2020/0621/182645_bb68932a_5550632.png)

6. 配置Servers,然后它会在根目录下创建一个Servers的文件夹

   ![](https://images.gitee.com/uploads/images/2020/0621/182732_8959ded1_5550632.png)

7. 点击 File ，New Others，找到Web ，选择**Dynamic Web Project**，next，起个名

8. 双击Servers

![](https://images.gitee.com/uploads/images/2020/0621/183053_23a0335a_5550632.png)

选择第二个**Use Tomcat installation**,这样Eclipse就会使用本地Tomcat，而不会自己做一个Tomcat副本

写一个index.jsp测试一下,右击运行服务器

![](https://images.gitee.com/uploads/images/2020/0621/183626_0a427765_5550632.png)



注意，更改jsp代码保存之后可以不用重启服务器，直接页面刷新就可以了。

### 10.3 JSP页面元素

a. **脚本 (Scriptlet)，共有 3 种如下**

```jsp
<%
	定义局部变量，Java语句
%>
```

```jsp
<%!
	定义全局变量或方法
%>
```

```jsp
<%=
	输出
%>
```

b. **指令**

> 配置指令 <%@page %>

<%@page %>下指定的属性：

language : JSP页面使用的语言

import：导入类

pageEncoding：JSP本身的编码

contentType：浏览器解析JSP的编码

```jsp
<%@page import="java.io.IOException"%>
<%@ page language="java" contentType="UTF-8"
    pageEncoding="UTF-8" import= "java.util.Date" import= "java.io.PrintWriter"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
    <!--注释-->
    
	Hello World Index.jsp
	<% 
    	//Java注释
    	/*Java注释 2*/
		String name = "zhangsan";
		out.print("hello"+name);
	%>
    
    <%--JSP注释--%>
	
    <%! 
	public String str = "aaa";
	
	public void myInit() throws IOException{  
		Date date = new Date();
		
	}
	
	%>
	
	<%="<br/>"+"bbb"+str +"<br/>"%>
</body>
</html>
```





### 10.4 JSP 内置对象

这些对象不需要new，就可以直接使用的。共有九个：

> out
>
> pageContext
>
> request
>
> response
>
> session
>
> application
>
> config
>
> page
>
> exception

#### 10.4.1 out：向客户端输出(输出对象)

#### 10.4.2 pageContext

#### 10.4.3 request

请求对象，存储客户端向服务端发送的请求信息

![](https://images.gitee.com/uploads/images/2020/0629/194917_f4e9152c_5550632.png )

常用方法：

**String getParameter(String name) //根据key返回value**

```
它可以根据传的字段名得到值。key-value.
比如：
getParameter("name")
就会返回
zs
```

**String [] getParameterValues(String name)** 

```
在原先基础之上追加一个hobbies，为了拿到多个值，我们可以用上述方法
```

**void setCharacterEncodeing("编码类型") //设置请求编码**

**getRequestDispatcher("b.jsp").forward(request,response) //请求转发(页面跳转至b.jsp)**

**ServerletContext getSeverContext() //获取项目的ServerletContext对象**

实践：设计登录界面，register.jsp和show.jsp,一个用来登录，一个用来跳转。

```jsp
<!--register.jsp-->
<%@page import="java.io.IOException"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" import= "java.util.Date" import= "java.io.PrintWriter"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	
	<form action = "show.jsp">
		用户名 :<input type = "text" name = "username"/> <br/>				
		密码 :<input type = "text" name = "password"/> <br/>
		
		年龄 :<input type = "text" name = "uage"/> <br/>
		爱好<br/>:
		<input type = "checkbox" name = "uhobbies" value = "足球"/>足球，
		<input type = "checkbox" name = "uhobbies" value = "篮球"/>篮球，
		<input type = "checkbox" name = "uhobbies" value = "乒乓球"/>乒乓球，
		<input type = "submit" value = "注册" >
	</form>
</body>
</html>
```

```jsp
<!--show.jsp-->
<%@page import="java.io.IOException"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" import= "java.util.Date" import= "java.io.PrintWriter"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
		request.setCharacterEncoding("UTF-8"); 
		String name = request.getParameter("username");
		String pwd = request.getParameter("password");
		int age = Integer.parseInt( request.getParameter("uage"));
		String [] hobbies = request.getParameterValues("uhobbies");
	%>
	
	注册成功，信息如下：<br/>
	姓名：<%= name%><br/>
	年龄：<%=age %><br/>
	密码：<%=pwd %><br/>
	爱好：<%
			for(String hobby:hobbies){
				out.print(hobby+"&nbsp;");
			}
		%><br/>
</body>
</html>
```

![](https://images.gitee.com/uploads/images/2020/0629/203548_aa0a35fa_5550632.png )

![](https://images.gitee.com/uploads/images/2020/0629/204232_6c85a447_5550632.png)

注意：默认提交是**GET方式(地址栏请求方式)**

改为form表单method改为POST方式后：

![](https://images.gitee.com/uploads/images/2020/0629/204513_1b64ef17_5550632.png )

推荐使用POST方法。

#### 10.4.5 response

响应对象(从服务器到客户端)

常用方法

> void addCookie(Cookie cookie); //服务端向客户端增加一个Cookie对象
>
> void sendRedirect(String location) throws IOException; //页面跳转的方式（重定向）
>
> void setContentType(String type)；//设置服务器content类型

**重定向实验-登录**

重定向，登录 login.jsp -> 判断check.jsp ->登录成功 success.jsp

login.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>登录测试</title>
</head>
<body>
	<form action="check.jsp" method = "post">
	用户名：<input type = "text" name = "uname"> <br/>
	密码：<input type = "password" name = "pwd"> <br/>
	<input type = "submit" value = "登录"> <br/>
	</form>
</body>
</html>
```

check.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
		request.setCharacterEncoding("utf-8");
		String usn = request.getParameter("uname");
		String pwd = request.getParameter("pwd");
		if(usn.equals("zs") && pwd.equals("123")){
			//重定向跳转
			response.sendRedirect("success.jsp");
		}else{
			out.print("Username or Password error!");
		}
	%>
</body>
</html>
```

success.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	登录成功！<br/>
	欢迎您：
	<%
		String name = request.getParameter("uname");
		out.print(name);
	%>
</body>
</html>
```

![](https://images.gitee.com/uploads/images/2020/0707/153217_0e3bae6c_5550632.png)

![](https://images.gitee.com/uploads/images/2020/0707/153246_7f4d55f8_5550632.png)

通过response对象的sendRedirect方法跳转页面（重定向）导致**数据丢失**

换成request对象的getRequestDispatcher请求转发试试

```jsp
request.getRequestDispatcher("success.jsp").forward(request,response);
```

![](https://images.gitee.com/uploads/images/2020/0707/153715_88cb32c6_5550632.png )

可以发现2个现象，首先是可以正常打印用户名了，其次，页面本身并没有跳转，还是在check.jsp而之前的重定向会让页面定位到success.jsp

![输入图片说明](https://images.gitee.com/uploads/images/2020/0921/164156_74f80e66_5550632.png "屏幕截图.png")

![输入图片说明](https://images.gitee.com/uploads/images/2020/0921/164220_551b89fe_5550632.png "屏幕截图.png")

**请求转发与重定向的区别**

![image-20200921164734123](C:\Users\micha\AppData\Roaming\Typora\typora-user-images\image-20200921164734123.png)

<br>

#### 10.4.6 session

session存在于服务端，Cookie (本地缓存) 存在于客户端，Cookie是服务端产生的，发给客户端保存。

Cookie的形式：key: value

Cookie类存在于javax.servlet.http.Cookie

> public Cookie(String name,String) //设置键值对
>
> String getName();
>
> String getValue();
>
> void setMaxAge(int expiry); // 最大有效时间

将Cookie发送给客户端-服务端准备Cookie

> response.addCookie(Cookie cookie)

客户端获取Cookie

> request.getCookies(); //必须拿到所有的Cookie,不能获得单独的一个单独Cookie对象。

<br>

实例一:

服务端通过response发送Cookie，客户端接收Cookie并遍历

```jsp
<%@page import="java.io.IOException"%>
<%@ page language="java" contentType="UTF-8"
	pageEncoding="UTF-8" import="java.util.Date"
	import="java.io.PrintWriter"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
		//服务端
		response.addCookie(new Cookie("usn","zs"));
		response.addCookie(new Cookie("pwd","123"));
		//页面跳转至客户端(转发或重定向)
		response.sendRedirect("result.jsp");
	%>
	
</body>
</html>
```

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
		//客户端
		Cookie[] cookies = request.getCookies();
		for(Cookie c:cookies){
			out.print(c.getName() + "---" + c.getValue() + "<br>");
		}
	%>
</body>
</html>
```

结果图:

![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/145423_4df74f93_5550632.png "屏幕截图.png")

<br>

实例二：使用Cookie，自动记录用户名密码。

login.jsp 用来登录

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>登录测试</title>
</head>
<body>
	<%!
    String uname;
	String pwd;
    %>
    
	<%
		Cookie[] cookies = request.getCookies();

	for (Cookie c : cookies) {
		if (c.getName().equals("usn")) {
			uname = c.getValue();
		}
		if (c.getName().equals("pwd")) {
			pwd = c.getValue();
		}
	}
	%>
	<form action="check.jsp" method="post">
		Username: <input type="text" name="usn" value="<%=(uname == null)?"":uname%>"> <br>
		Password: <input type="password" name="pwd" value="<%=(pwd==null)?"":pwd%>">
		<br> <input type="submit">

	</form>
</body>
</html>
```

check.jsp用于验证用户名和密码，并且向客户端发送Cookie

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
		request.setCharacterEncoding("utf-8");
		String usn = request.getParameter("usn");
		String pwd = request.getParameter("pwd");
		//将用户名密码加入Cookie
		Cookie cookie = new Cookie("name",usn);
		Cookie cookie2 = new Cookie("pwd",pwd);
		
		response.addCookie(cookie);
		response.addCookie(cookie2);
		if(usn != null && pwd != null){
			if(usn.equals("zs") && pwd.equals("123"))
			{
				request.getRequestDispatcher("success.jsp").forward(request,response);
			}else{
				out.print("Err");
			}
		}
	%>
</body>
</html>
```

success.jsp 客户端页面用于接收cookie，打印相关信息

效果图：

![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/151319_298e9fa5_5550632.png "屏幕截图.png")

![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/152628_6065da54_5550632.png "屏幕截图.png")

> Cookie 设置最大有效期
>
> > cookie.setMaxAge(int num);

Session对象，称为会话。例如：当你浏览一个网页从开始到结束，称为一次会话。

Session机制：

![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/153818_8f4b41c0_5550632.png "屏幕截图.png")

现在有，张三李四，王五，分别使用IE，Chrome，Firefox请求服务，那么在服务端就会存储这3个用户的session，通过**JSESSIONID**进行一一对应（就是之前Cookie里面那一串奇奇怪怪的东西）。每个Session对象会有一个SessionId，服务端还会产生一个Cookie，并且将该Cookie的 JESSIONID 和刚才SessionId的值绑定为键值对，在响应客户端的时候，将该cookie发送给客户端。

**总结**

a. Session存储于服务端

b. Session在同一个用户访问时共享

c. 用户在第一次访问时会产生一个SessionId，复制给Cookie中的 JSessionID 发送给客户端

**Session常用方法**

> String getId()：获取sessionId
>
> boolean isNew（）：判断是否为新用户
>
> viod inValidate()：使Session失效（退出，注销）
>
> void setAttribute()
>
> Object getAttribute()
>
> void setMaxInactiveInterval(秒)：设置最长非活动时间
>
> int getMaxInactiveInterval()：获取最长非活动时间

**实例**

第一次登录，成功之后，返回一个Cookie包括用户名，密码等信息。通过SessionId和JSESSIONID进行匹配。通过Session编写欢迎页。

![输入图片说明](https://images.gitee.com/uploads/images/2020/1003/154942_97bee52b_5550632.png "屏幕截图.png")

涉及页面3个，login.jsp，check.jsp，welcome.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Login</title>
</head>
<body>
	<form action="check.jsp" method="post">
		User name:<input type = "text" name = "usn"><br>
		Password:<input type="password" name ="pwd"><br>
		<input type="submit" value ="Login">
	</form>
</body>
</html>
```

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Check</title>
</head>
<body>
	<%
		request.setCharacterEncoding("UTF-8");
		String usn = request.getParameter("usn");
		String pwd = request.getParameter("pwd");
		if(usn!=null && pwd != null){
			if(usn.equals("zs" )&& pwd.equals("123")){
				//只有登录成功才会存在以下属性值
				session.setAttribute("usn", usn);
				session.setAttribute("pwd", pwd);
				request.getRequestDispatcher("welcome.jsp").forward(request, response);
			}else{
				out.print("Username or password error.");
				response.sendRedirect("login.jsp");
			}
		}else{
			out.print("Error");
		}
	
	%>
</body>
</html>
```

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Welcome</title>
</head>
<body>
	欢迎您：
	<%
		//通过Session拿值
		String usn = (String)session.getAttribute("usn");
		if(usn == null){
            //防止通过URL直接访问此页面
			response.sendRedirect("login.jsp");
		}else{
			out.print(usn);
		}
		
	%>
</body>
</html>
```

![输入图片说明](https://images.gitee.com/uploads/images/2020/1008/085730_5a1952de_5550632.png "屏幕截图.png")

<br>

#### 10.4.8 application

全局对象

常用方法:

> String getContextPath(): 获取虚拟路径
>
> String getRealPath(String path): 获取虚拟路径的绝对路径

![](https://images.gitee.com/uploads/images/2020/1003/163430_f71b8445_5550632.png)



<br>

#### 10.4.9 config

<br>

#### 10.4.10 page

<br>

#### 10.4.11 exception

<br>

#### 10.4.12 四种范围对象

范围从小到大为PageContext，request，session，application。它们都有如下方法

- Object getAttribute(String name)：根据属性名获取属性值
- void setAttribute(String name,Object obj)：不存在则设置，存在则修改
- void removeAttribute(String name)根据属性名删除对象

它们的作用范围依次是：当前页面，同一次请求，同一次会话，全局（整个项目）。

<br>

### 10.5 Java连接ava数据库（JDBC）

JDBC：Java DataBase Connectivity

它可以将Java代码和多种关系型数据库提供统一的访问方式。下图为Java程序，JDBC，数据库之间的关系。所以JDBC的核心就是提供API以便操作访问数据库。JDBC DriverManager作用是管理不同的数据库驱动。各种数据库驱动程序（由数据库厂商提供的jar包）作用是连接或直接操作数据库。

![输入图片说明](https://images.gitee.com/uploads/images/2020/1008/093248_fa6b72b8_5550632.png "屏幕截图.png")

JDBC API的主要功能核心就是3个。连库，执行SQL，拿到结果。

![输入图片说明](https://images.gitee.com/uploads/images/2020/1008/094029_11b490ab_5550632.png "屏幕截图.png")

具体通过以下**类，接口**

DriverManager：管理JDBC驱动

Connection：连库

Statement(PreparedStatement)：SQL增删改查

CallableStatement：调用存储过程

Result：结果集（ResultSet）

<br>

#### 10.5.1 JDBC访问数据库的具体步骤

1. 导入驱动程序，加载具体的类
2. 与数据库建立连接
3. 发送SQL，执行
4. 处理处理集（查询）

**数据库驱动 jar包**

Oracle ： ojdbc-x.har

MySQL ： mysql-connector-java-x.jar

SqlServer ：sqljdbc-x.jar

去官网找jar包

然后导入驱动类，先列举一下具体驱动类的名称

Oracle：oracle.jdbc.OracleDriver

MySQL：com.mysql.cj.jdbc.Driver

SqlSever：com.microsoft.sqlsever.jdbc.SQLServerDriver

然后还有特殊的连接字符串（数据库名放在这里【IP：端口之类的】）

Oracle：&nbsp;&nbsp;*jdbc:oracle:thin:@localhost:1521:ORCL*

MySQL:&nbsp;&nbsp; *jdbc:mysql://localhost:3306/数据库名*

SqlServer:&nbsp;&nbsp;*jdbc:microsoft:sqlserver:localhost:143；database=数据库实例名*

这些网上可以查到。不需要死记硬背。

具体写法如下：

```java
package demo1;

import java.sql.*;

public class JBDCDemo {

	//连接字符串
	private final static String URL = "jdbc:mysql://localhost:3306/test?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8";
	private final static String USERNAME = "root";
	private final static String PWD = "****";

	public JBDCDemo() {
		// TODO Auto-generated constructor stub
	}

	public static void update()  {
        // 函数用于增删改
		Connection connection = null;
		Statement statement = null;
		try {
            // 导入驱动，加载驱动类
			Class.forName("com.mysql.cj.jdbc.Driver");
            
			// 与数据库建立连接
			connection = DriverManager.getConnection(URL, USERNAME, PWD);
            
			// 发送sql并执行
			statement = connection.createStatement();
			String sqlString = "insert into student values(1,'zs','m',22);";
            //拿到影响行的结果
			int influence = statement.executeUpdate(sqlString);
			if (influence > 0) {
				System.out.println("influenced row :" + influence + " Success");
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				statement.close();
				connection.close();
			} catch (SQLException e) {
				// TODO: handle exception
				e.printStackTrace();
			}
			
		}

	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		update();
	}

}

```

执行结果：

![输入图片说明](https://images.gitee.com/uploads/images/2020/1008/105857_13ec2685_5550632.png "屏幕截图.png")

##### 技术总结

1. 去官网下载数据库驱动的jar包，将其导入至项目【Build path -> Add to build path】
2. 导入驱动类【Class.forName("com.mysql.cj.jdbc.Driver");】
3. 连接数据库，需要提供【连接字符串，用户名，密码】
4. 编写异常处理

<br>

#### 10.5.2  JDBC切换数据库 与 PreparedStatement

```java
import java.sql.*;

public class OracleJDBC {

	final static String CONN_STRING = "jdbc:oracle:thin:@localhost:1521:test";
	final static String USN = "system";
	final static String PWD = "****";

	public static void main(String[] args){
		//
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver");
			Connection connection = DriverManager.getConnection(CONN_STRING,USN,PWD);
			//准备SQL语句
			PreparedStatement preparedStatement = connection.prepareStatement("select * from employees");
			//执行SQL (SELECT 专用)
			ResultSet resultSet = preparedStatement.executeQuery();
			if(resultSet.next()) {
				System.out.println("Have data");
			}
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

	}

}
```

增删改都可以通过上述自定义函数数据，查询的写法如下：

```java
import java.sql.*;


public class JBDCDemo {

	//连接字符串
	private final static String URL = "jdbc:mysql://localhost:3306/test?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8";
	private final static String USERNAME = "root";
	private final static String PWD = "****";

	public JBDCDemo() {
		// TODO Auto-generated constructor stub
	}
	
	public static void query() {
		Connection connection = null;
		Statement statement = null;
		ResultSet resultSet = null;
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");// 导入驱动，加载驱动类
			// 与数据库建立连接
			connection = DriverManager.getConnection(URL, USERNAME, PWD);
			// 发送sql并执行
			statement = connection.createStatement();
			String sqlString = "select * from student;";
			//ResultSet 可以看成一张游标指向首行的表
			resultSet = statement.executeQuery(sqlString);
			while(resultSet.next()) {
				int sno = resultSet.getInt("sno");
				String snameString= resultSet.getString("sname");
				System.out.println("sno: " + sno + " sname: " + snameString);
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				if(resultSet != null){
					resultSet.close();
				}
				if(statement != null) {
					statement.close();
				}
				connection.close();
			} catch (SQLException e) {
				// TODO: handle exception
				e.printStackTrace();
			}		
		}
	}

	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		query();
	}

}
```

执行查询的函数为**statement.executeQuery**，返回**ResultSet**，可以把它当作带有游标的表，初始时，游标指在首行（表头），可以通过**next()**方法判断下一行是否为空。通过getXXX方法指明字段名，进行对应类型的取值。通过之前写的update方法追加**ls**。查询结果如下：



![输入图片说明](https://images.gitee.com/uploads/images/2020/1026/153251_16166e83_5550632.png "屏幕截图.png")

Connection除了可以产生 Statement ，还可以产生PreparedStatement，CallableStatement。

```java
Statement s1 = connection.createStatement();
PreparedStatement s2 = connection.prepareStatement(sql);
CallableStatement s3 = connection.prepareCall(sql);
```

![输入图片说明](https://images.gitee.com/uploads/images/2020/1026/154516_0fc63f5b_5550632.png "屏幕截图.png")

由源码可以看出，PreparedStatement是Statement的子接口。

```java
public static void query() {
		Connection connection = null;
		PreparedStatement preparedStatement = null;
		ResultSet resultSet = null;
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");// 导入驱动，加载驱动类
			// 与数据库建立连接
			connection = DriverManager.getConnection(URL, USERNAME, PWD);
			// 发送sql并执行
			//statement = connection.createStatement();
			String sqlString = "select * from student;";
			preparedStatement = connection.prepareStatement(sqlString);
			
			//ResultSet 可以看成一张游标指向首行的表
			resultSet = preparedStatement.executeQuery(sqlString);
			while(resultSet.next()) {
				int sno = resultSet.getInt("sno");
				String snameString= resultSet.getString("sname");
				System.out.println("sno: " + sno + " sname: " + snameString);
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				if(resultSet != null)
				{
					resultSet.close();
				}
				if(preparedStatement != null) {
					preparedStatement.close();
				}
				connection.close();
			} catch (SQLException e) {
				// TODO: handle exception
				e.printStackTrace();
			}
		}

	}
```

现在来看，PreparedStatement和Statement的在查询上的区别就在于**是否先执行SQL**。接下来，我们从代码角度看看增删改的区别。

```java
public static void update()  {// 增删改
		Connection connection = null;
		PreparedStatement statement = null;
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");// 导入驱动，加载驱动类
			// 与数据库建立连接
			connection = DriverManager.getConnection(URL, USERNAME, PWD);
			// 发送sql并执行
			statement = connection.prepareStatement("insert into student values(?,?,?,?);");
			statement.setInt(1, 4);
			statement.setString(2, "Jack");
			statement.setString(3, "fe");
			statement.setInt(4, 99);
			int influence = statement.executeUpdate();
			if (influence > 0) {
				System.out.println("influenced row :" + influence + "Success");
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				statement.close();
				connection.close();
			} catch (SQLException e) {
				// TODO: handle exception
				e.printStackTrace();
			}
			
		}

	}
```

![输入图片说明](https://images.gitee.com/uploads/images/2020/1026/155648_1564d28c_5550632.png "屏幕截图.png")

由此看出，PreparedStatement可以进行预编译，使用**?**代替SQL的内容，更加灵活。

<br>

#### 10.5.3  PreparedStatement 与 Statement的区别

推荐使用PreparedStatement对数据库进行操作。主要原因有二，简单，安全。

```java
package MySQLDemo;

import java.sql.*;


public class DBOperation {

	// 连接字符串
	private final static String URL = "jdbc:mysql://localhost:3306/test?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8";
	private final static String USERNAME = "root";
	private final static String PWD = "wangzheng10010";
	private Connection connection = null;
	private PreparedStatement preparedStatement = null;
	private ResultSet resultSet = null;

	public DBOperation() {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");// 导入驱动，加载驱动类
			this.connection = DriverManager.getConnection(URL, USERNAME, PWD);
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

	public ResultSet query(String sql, Object[] args) throws SQLException {
		this.preparedStatement = this.connection.prepareStatement(sql);
		
		if (args != null) {
			for (int i = 0; i < args.length; i++) {
				this.preparedStatement.setObject(i + 1, args[i]);
			}
		}
		this.resultSet = this.preparedStatement.executeQuery();
		return this.resultSet;
	}

	public int update(String sql, Object[] args) throws SQLException {
		int num = 0;
		this.preparedStatement = this.connection.prepareStatement(sql);
		if (args != null) {
			for (int i = 0; i < args.length; i++) {
				this.preparedStatement.setObject(i + 1, args[i]);
			}
		}
		num = this.preparedStatement.executeUpdate();

		return num;
	}

	public void closAll() {
		try {
			if (this.resultSet != null) {
				this.resultSet.close();
			}
			if (this.preparedStatement != null) {
				this.preparedStatement.close();
			}
			if (this.connection != null) {
				this.connection.close();
			}
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

	}
}


package MySQLDemo;

import java.sql.SQLException;

public class Test {

	public Test() {
		// TODO Auto-generated constructor stub
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		try {
			DBOperation dbOperation = new DBOperation();
			String sqlString = "insert into login(lid,username,password) values(?,?,?);";
			String [] argString = {"2","111","222"};
			dbOperation.update(sqlString, argString);
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

}

```

![输入图片说明](https://images.gitee.com/uploads/images/2020/1109/150952_cdc4debd_5550632.png "屏幕截图.png")

<br>

#### 10.5.4  JavaBean

为了结构化的整理项目，我们在JSP项目中，最好将Java代码和JSP页面分开书写，同时处于规定，我们将数据库操作的类命名为...Dao

(当然也可以不遵守这个规范)。

JavaBean的作用（将jsp代码中的java代码转移到一个java文件内）：

1. 提高代码复用性
2. 减轻jsp的复杂度

以后任何的相同操作，都可以直接调用这个JavaBean。

JavaBean（一个Java类）的定义：**1. 必须是public修饰的无参构造方法类 2.所有属性都是private，并提供set/get,如果是boolean，set可以改成is**。

样例如下：

![](https://images.gitee.com/uploads/images/2020/1109/155747_aed639fb_5550632.png)

在使用层面，JavaBean分为两类。

1. 封装业务逻辑
2. 封装数据（如上图的例子，实体类，通常是数据库中的表）

![输入图片说明](https://images.gitee.com/uploads/images/2020/1109/160443_2023f47d_5550632.png "屏幕截图.png")

上图是业务逻辑的JavaBean的示例

<br>

### 10.6 Jsp标记

#### 10.6.1 page 指令

page 指令就是之前Eclipse自动为我们生成的那行代码：

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
```

page指令通常定义的属性有4中：

- contentType
- import
- language
- pageEncoding

#### 10.6.2 include指令

用于把相同信息进行引用，下例中有index.jsp和a.jsp两个页面。

**index.jsp**

```jsp

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>index</title>
</head>
<body>
	<font color="red" size ="10">Avada kedavera</font>
	<table border="1">
		<% 
			for(int i = 0;i<20;i++){
				out.print("<tr>");
				for(int j = 0;j<20;j++){
					out.print("<td> </td>");
				}
				out.print("</tr>");
			}
		
		%>
	</table>
</body>
</html>
```

**index.jsp效果**

![输入图片说明](https://images.gitee.com/uploads/images/2020/1009/140546_13a91690_5550632.png "屏幕截图.png")

**a.jsp**

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<%@include file="index.jsp" %><br>
Expecto 
</body>
</html>
```

**最终效果**

![输入图片说明](https://images.gitee.com/uploads/images/2020/1009/140505_72185fba_5550632.png "屏幕截图.png")



<br>

### 10.7 Jsp 动作标记

#### 10.7.1 include 动作标记

#### 10.7.2 forward 动作标记

用于页面跳转。实例：设计3个页面，a.jsp,file01.jsp,file02.jsp

实验目的：测试forward动作标记的用法

实验流程：使用随机数向上取整，奇数跳转file01.jsp，偶数跳转file02.jsp

代码如下：

**a.jsp**

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<%
	long a = Math.round(Math.random());
	if( a%2 == 1){
		%>
		<jsp:forward page = "file01.jsp"></jsp:forward>
		
		<% 
	}else{
			%>
		<jsp:forward page = "file02.jsp"></jsp:forward>
			<%	
	}
	
%>
</body>
</html>
```

**file01.jsp**

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<font color="red" size = 10>Odd page</font>
</body>
</html>
```

**file02.jsp**

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<font color="green" size = 10>Even page</font>
</body>
</html>
```

**最终效果**

![输入图片说明](https://images.gitee.com/uploads/images/2020/1009/142829_008c99f7_5550632.png "屏幕截图.png")

#### 10.7.3 param 动作标记



### 10.8 MVC模式和Servlet流程

M：Model 模型

V：View 视图

C：Control 控制器

![输入图片说明](https://images.gitee.com/uploads/images/2020/1109/162244_8efd30af_5550632.png "屏幕截图.png")

![输入图片说明](https://images.gitee.com/uploads/images/2020/1109/162801_7f82d795_5550632.png "屏幕截图.png")

Servlet，是一些符合特定规则的Java类

1. 继承javax.servlet.http.HttpServlet
2. 重写其中的 doGet() 或doPost()方法

doGet()：接受并处理所有get提交方式的请求

doPost()：接受并处理所有post提交方式的请求

![输入图片说明](https://images.gitee.com/uploads/images/2020/1109/163956_2474868e_5550632.png "屏幕截图.png")

<br>

## Part 11 JVM系列

### 11.0 JVM 与 Java体系结构

![](https://images.gitee.com/uploads/images/2020/0702/161229_10de8180_5550632.png)

#### 0x00 Java代码执行流程



####  0x01 JVM的架构模型



#### 0x02 JVM的生命周期



#### 0x03 JVM的发展历程



### 11.1 内存与垃圾回收



### 11.2 字节码与类的加载



### 11.3 性能监控与调优



