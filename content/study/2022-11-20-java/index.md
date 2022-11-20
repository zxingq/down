# JavaSE_day06【面向对象基础--上】 

## 今日内容

- 类与对象
- 成员变量
- 成员方法

## 学习目标

- [ ] 初步了解面向对象的思想
- [ ] 能够明确类与对象关系
- [ ] 能够掌握类的定义格式
- [ ] 能够掌握创建对象格式
- [ ] 能够通过类访问类的静态成员变量和静态成员方法
- [ ] 能够通过对象访问对象的普通成员变量和普通成员方法
- [ ] 能够区别静态方法和普通方法
- [ ] 能够区别类变量与实例变量
- [ ] 能够区别成员变量与局部变量
- [ ] 能够理解方法的调用执行机制
- [ ] 能够理解方法的参数传递机制


# 第五章 面向对象基础（上）

## 5.1 面向对象思想概述

### 1、概述

Java语言是一种面向对象的程序设计语言，而面向对象思想（OOP）是一种程序设计思想，我们在面向对象思想的指引下，使用Java语言去设计、开发计算机程序。
这里的**对象**泛指现实中一切事物，每种事物都具备自己的**属性**和**行为**。面向对象思想就是在计算机程序设计过程中，参照现实中事物，将事物的属性特征、行为特征抽象出来，描述成计算机事件的设计思想。
它区别于面向过程思想（POP），强调的是通过调用对象的行为来实现功能，而不是自己一步一步的去操作实现。

### 2、面向对象与面向过程的区别

面向过程：POP: Process-Oriented Programming

​	以函数（方法）为最小单位

​	数据独立于函数之外

​	以过程，步骤为主，考虑怎么做

面向对象：OOP: Object Oriented Programming

​	以类/对象为最小单位，类包括：数据+方法

​	以对象（谁）为主，考虑谁来做，谁能做

面向对象仍然包含面向过程，只不过关注点变了，关注谁来做

程序员的角色：

面向过程：程序员是具体执行者

面向对象：程序员是指挥者

面向对象思想是一种更符合我们思考习惯的思想，它可以将复杂的事情简单化，并将我们从执行者变成了指挥者。

3、面向对象的基本特征

面向对象的语言中，包含了三大基本特征，即封装、继承和多态。

## 5.2 类和对象

环顾周围，你会发现很多对象，比如桌子，椅子，同学，老师等。桌椅属于办公用品，师生都是人类。那么什么是类呢？什么是对象呢？

### 什么是类

* **类**：是一类具有相同特性的事物的抽象描述，是一组相关**属性**和**行为**的集合。可以看成是一类事物的模板，使用事物的属性特征和行为特征来描述该类事物。

现实中，描述一类事物：

* **属性**：就是该事物的状态信息。
* **行为**：就是该事物能够做什么。

举例：小猫。

​	属性：名字、体重、年龄、颜色。
​	行为：走、跑、叫。

### 什么是对象

* **对象**：是一类事物的具体体现。对象是类的一个**实例**（对象并不是找个女朋友），必然具备该类事物的属性和行为。

现实中，一类事物的一个实例：一只小猫 。

举例：一只小猫。

​	属性：tom、5kg、2 years、yellow。
​	行为：溜墙根走、蹦跶的跑、喵喵叫。

### 类与对象的关系

- 类是对一类事物的描述，是**抽象的**。
- 对象是一类事物的实例，是**具体的**。
- **类是对象的模板，对象是类的实体**。

![](https://raw.githubusercontent.com/zxingq/Picture/main/202211172133122.jpg) 

## 5.3 类的定义和对象的创建

### 事物与类的对比

现实世界的一类事物：

​	**属性**：事物的状态信息。
​	**行为**：事物能够做什么。

 Java中用class描述事物也是如此：

​	**成员变量**：对应事物的**属性**
​	**成员方法**：对应事物的**行为**

### 类的定义格式

```java
public class ClassName {
  //成员变量
  //成员方法 
}
```

* **定义类**：就是定义类的成员，包括**成员变量**和**成员方法**。
* **成员变量**：和以前定义变量几乎是一样的。只不过位置发生了改变。**在类中，方法外**。
* **成员方法**：和以前写的main方法格式类似。只不过功能和形式更丰富了。在类中，方法外。

类的定义格式举例：

```java
public class Person {
  	//成员变量
  	String name；//姓名
    int age；//年龄
    boolean isMarried;
    
    public void walk(){
        System.out.println("人走路...");
    }
    public String display(){
        return "名字是：" + name + "，年龄是：" + age + "，Married：" + isMarried;
    }
}
```

### 对象的创建

创建对象：

```java
new 类名()//也称为匿名对象

//给创建的对象命名
//或者说，把创建的对象用一个引用数据类型的变量保存起来
类名 对象名 = new 类名();
```

那么，对象名中存储的是什么呢？答：对象地址

```java
class Student{
    
}
public class TestStudent{
    //Java程序的入口
    public static void main(String[] args){
        System.out.println(new Student());//Student@7852e922

        Student stu = new Student();
        System.out.println(stu);//Student@4e25154f
        
        int[] arr = new int[5];
		System.out.println(arr);//[I@70dea4e
    }
}
//Student和TestStudent没有位置要求，谁在上面谁在下面都可以
//但是如果TestStudent类的main中使用了Student类，那么要求编译时，这个Student已经写好了，不写是不行的
//如果两个类都在一个.java源文件中，只能有一个类是public的
```

发现学生对象和数组对象类似，直接打印对象名和数组名都是显示“类型@对象的hashCode值"，所以说类、数组都是引用数据类型，引用数据类型的变量中存储的是对象的地址，或者说指向堆中对象的首地址。

那么像“Student@4e25154f”是对象的地址吗？不是，因为Java是对程序员隐藏内存地址的，不暴露内存地址信息，所以打印对象时不直接显示内存地址，而是JVM提取了对象描述信息给你，默认提取的是对象的运行时类型@代表对象唯一编码的hashCode值。

![1561597909862](https://raw.githubusercontent.com/zxingq/Picture/main/202211172133966.png)

## 5.4 成员变量

### 1、成员变量的分类

实例变量：没有static修饰，也叫对象属性，属于某个对象的，通过对象来使用

类变量：有static修饰，也叫类变量，属于整个类的，不是属于某个实例

### 2、如何声明成员变量？

```java
【修饰符】 class 类名{
    【修饰符】 数据类型  属性名;    //属性有默认值
    【修饰符】 数据类型  属性名 = 值; //属性有初始值
}
```

> 说明：属性的类型可以是Java的任意类型，包括基本数据类型、引用数据类型（类、接口、数组等）

例如：声明一个中国人的类

```java
class Chinese{
	static String country;
	String name;
    char gender = '男';//显式赋值
}
```

### 3、如何在类外面访问成员变量？

#### （1）类变量

```java
类名.静态成员变量  //推荐

对象名.静态成员变量 //不推荐
```

#### （2）实例变量

```java
对象名.普通成员变量  //只能使用这种方式
```

例如：

```java
public class TestChinese {
	public static void main(String[] args) {
		//类名.静态成员变量
		System.out.println(Chinese.country);
		//错误，普通成员变量必须通过对象.进行访问
//		System.out.println(Chinese.name);
		
		Chinese c1 = new Chinese();
		//对象名.普通成员变量
		System.out.println(c1.name);
		//静态的成员变量也可以通过对象.进行访问
		//对象名.普通成员变量
		System.out.println(c1.country);
        System.out.println(c1.gender);
	}
}
class Chinese{
	static String country;
	String name;
    char gender = '男';
}

```

### 4、成员变量的特点

#### （1）成员变量有默认值

|          | 浮点数（float，double）        | 0.0      |
| -------- | ------------------------------ | -------- |
|          | 字符（char）                   | '\u0000' |
|          | 布尔（boolean）                | false    |
|          | 数据类型                       | 默认值   |
| 基本类型 | 整数（byte，short，int，long） | 0        |
| 引用类型 | 数组-，类，接口                | null     |

#### （2）类变量的值是所有对象共享的，而实例变量的值是每个对象独立的

```java
public class TestChinese {
	public static void main(String[] args) {
		Chinese c1 = new Chinese();
		Chinese c2 = new Chinese();
		
		c1.name = "张三";
		c2.name = "李四";
        c2.gender = '女';
		
//		c1.country = "中国";
		Chinese.country = "中国";//推荐
		
		System.out.println("c1.country = " + c1.country + ",c1.name = " + c1.name + ",c1.gender = " + c1.gender);
		System.out.println("c2.country = " + c2.country + ",c2.name = " + c2.name + ",c2.gender = " + c2.gender);
	}	
}
class Chinese{
	static String country;
	String name;
    char gender = '男';
}

```

### 5、成员变量的内存图

​	内存是计算机中重要的部件之一，它是与CPU进行沟通的桥梁。其作用是用于暂时存放CPU中的运算数据，以及与硬盘等外部存储器交换的数据。只要计算机在运行中，CPU就会把需要运算的数据调到内存中进行运算，当运算完成后CPU再将结果传送出来。我们编写的程序是存放在硬盘中的，在硬盘中的程序是不会运行的，必须放进内存中才能运行，运行完毕后会清空内存。Java虚拟机要运行程序，必须要对内存进行空间的分配和管理，每一片区域都有特定的处理数据方式和内存管理方式。

![1561465258546](https://raw.githubusercontent.com/zxingq/Picture/main/202211172133556.png)

| 区域名称   | 作用                                                         |
| ---------- | ------------------------------------------------------------ |
| 程序计数器 | 程序计数器是CPU中的寄存器，它包含每一个线程下一条要执行的指令的地址 |
| 本地方法栈 | 当程序中调用了native的本地方法时，本地方法执行期间的内存区域 |
| 方法区     | 存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。 |
| 堆内存     | 存储对象（包括数组对象），new来创建的，都存储在堆内存。      |
| 虚拟机栈   | 用于存储正在执行的每个Java方法的局部变量表等。局部变量表存放了编译期可知长度的各种基本数据类型、对象引用，方法执行完，自动释放。 |

```java
class Test08FieldSave{
	public static void main(String[] args){
		Chinese c1 = new Chinese();
		c1.name = "张三";
		System.out.println(c1.country);//静态变量，也可以使用"对象名."进行访问
		System.out.println(c1.name);//普通成员变量通过"对象名."进行访问
		
		
		Chinese c2 = new Chinese();
		c2.name = "李四";
		System.out.println(c2.country);
		System.out.println(c2.name);
		
		System.out.println("----------------------------------");
		//其中一个对象将静态变量的值修改了，其他对象都会改变
		//因为静态变量只存一份
		c1.country = "中华人民共和国";
		System.out.println(c1.country);
		System.out.println(c2.country);
		System.out.println(Chinese.country);
		
		
		//其中一个对象将普通成员变量修改了，其他对象不受影响
		c1.name = "张三丰";
		System.out.println(c1.name);
		System.out.println(c2.name);
	}
	
}

class Chinese{
	static String country = "中国";//静态成员变量，所有中国人的国家的名称是一样，只需要存储一份
	String name;//普通成员变量，每一个中国人的姓名是独立，每一个对象单独存储
}

```

<img src="https://raw.githubusercontent.com/zxingq/Picture/main/202211172133573.png" style="zoom:80%;" />

```java
class MyDate{
	int year;
	int month;
	int day;
}
class Employee{
	String name;
	MyDate birthday;
}
class Test09FieldExer3{
	public static void main(String[] args){
		//创建两个员工对象
		Employee e1 = new Employee();
		Employee e2 = new Employee();
		
		//为两个员工对象的成员变量赋值
		e1.name = "张三";
		e1.birthday = new MyDate();
		
		e2.name = "李四";
		e2.birthday = new MyDate();
		
		e1.birthday.year = 2000;
		e1.birthday.month = 1;
		e1.birthday.day = 1;
		
		e2.birthday.year = 2000;
		e2.birthday.month = 3;
		e2.birthday.day = 8;
		
		System.out.println("第一个员工，姓名：" + e1.name +"，生日：" + e1.birthday.year + "年" + e1.birthday.month + "月" + e1.birthday.day + "日");
		System.out.println("第二个员工，姓名：" + e2.name +"，生日：" + e2.birthday.year + "年" + e2.birthday.month + "月" + e2.birthday.day + "日");
	}
}

```



![](https://raw.githubusercontent.com/zxingq/Picture/main/202211172143068.png)

### 6、成员变量练习题

（1）声明一个圆的图形类，有属性：半径
	在测试类的main中，创建圆的2个对象，为半径属性赋值，并显示两个圆的半径值和面积值
	提示：圆周率为Math.PI

（2）声明一个银行账户类，有属性：利率、账号、余额

​	在测试类的main中，创建账户类的两个对象，其中所有账户的利率是相同的，都是0.035，而账号和余额是不同的，并打印显示

（3）声明一个MyDate类型，有属性：年，月，日

​		  声明另一个Employee类型，有属性：姓名（String类型），生日（MyDate类型）

在测试类中的main中，创建两个员工对象，并为他们的姓名和生日赋值，并显示



## 5.5 成员方法

成员变量是用来存储对象的数据信息的，那么如何表示对象的行为功能呢？就要通过方法来实现

### 5.5.1 方法的概念

方法也叫函数，是一个独立功能的定义，是一个类中最基本的功能单元。

把一个功能封装为方法的目的是，可以实现代码重用，从而简少代码量。

### 5.5.2  方法的原则

方法的使用原则：

（1）必须先声明后使用

>  类，变量，方法等都要先声明后使用

（2）不调用不执行，调用一次执行一次。

### 5.5.3 成员方法的分类

成员方法分为两类：

* 实例方法：没有static修饰的方法，必须通过实例对象来调用。
* 静态方法：有static修饰的方法，也叫类方法，可以由类名来调用。

### 5.5.4 如何声明方法

1、方法声明的位置必须在类中方法外

2、语法格式

```java
【修饰符】 返回值类型 方法名(【参数列表：参数类型1 参数名1,参数类型2 参数名, ...... 】){
        方法体；
        【return 返回值;】
}

```

- 修饰符： 修饰符后面一一介绍，例如：public，static等都是修饰符
- 返回值类型： 表示方法运行的结果的数据类型，方法执行后将结果返回到调用者
  - 基本数据类型
  - 引用数据类型
  - 无返回值类型：void
- 方法名：给方法起一个名字，见名知意，能准确代表该方法功能的名字
- 参数列表：方法内部需要用到其他方法中的数据，需要通过参数传递的形式将数据传递过来，可以是基本数据类型、引用数据类型、也可以没有参数，什么都不写
- 方法体：特定功能代码
- return：结束方法，并将方法的结果返回去，
  - 如果返回值类型不是void，方法体中必须保证一定有return 返回值;语句，并且要求该返回值结果的类型与声明的返回值类型一致或兼容。
  - 如果返回值类型为void时，return 后面不用跟返回值，甚至也可以没有return语句。
  - return语句后面就不能再写其他代码了，否则会报错：Unreachable code

声明位置示例：

```java
类{
    方法1(){
        
    }
    方法2(){
        
    }
}

```

错误示例：

```java
类{
    方法1(){
        方法2(){  //位置错误
        
   		}
    }
}

```

#### 示例一：

声明一个圆的图形类：

​	属性（成员变量）：半径，

​	成员方法：求面积的方法，返回圆对象信息的方法

​	在测试类的main中，创建圆的2个对象，为半径属性赋值，调用两个方法进行测试
​	提示：圆周率为Math.PI

```java
class Circle{
	double radius;
	double area() {
		return Math.PI * radius * radius;
	}
}

```

> Circle不同的对象，半径值不同，那么面积也不同，所以这里area()是非静态的

#### 示例二：

声明一个计算工具类CountTools：

​	方法1：求两个整数的最大值

```java
class CountTools{
	static int max(int a, int b) {
        return a > b ? a : b;
	}
}

```

> CountTools只是一个工具类，求两个整数最大值的功能，和CountTools对象无关，所以这里max方法声明为静态的更好，当然也可以声明为非静态的，就是调用的时候需要创建CountTools对象而已。

### 5.5.5 如何在其他类中调用方法

#### （1）实例方法

```java
对象名.普通方法(【实参列表】)  //必须通过对象来访问

```

示例代码：

```java
public class TestCircle {
	public static void main(String[] args) {
		Circle c1 = new Circle();
		c1.radius = 1.2;
		System.out.println("c1的面积：" + c1.area());
		//普通方法只能通过"对象."进行访问
//		System.out.println("c1的面积：" + Circle.area());
        
		Circle c2 = new Circle();
		c2.radius = 2.5;
		System.out.println("c2的面积：" + c2.area());
	}
}
class Circle{
	double radius;
	public double area() {
		return Math.PI * radius * radius;
	}
}

```

#### （2）类方法

```java
类名.类方法(【实参列表】)  //推荐

对象名.类方法(【实参列表】) //不推荐

```

示例：

```java
public class TestCount {
	public static void main(String[] args) {
		System.out.println(CountTools.max(4, 1));
		
		//静态方法也可以通过“对象.”访问，就是麻烦点
		CountTools c = new CountTools();
		System.out.println(c.max(2, 5));
	}
}
class CountTools{
	static int max(int a, int b) {
		return a > b ? a : b;
	}
}

```

#### （3）总结

* 形参：在定义方法时方法名后面括号中声明的变量称为形式参数（简称形参）即形参出现在方法定义时。
* 实参：调用方法时方法名后面括号中的使用的值/变量/表达式称为实际参数（简称实参）即实参出现在方法调用时。

总结：

（1）调用时，需要传“实参”，实参的个数、类型、顺序顺序要与形参列表一一对应

​		如果方法没有形参，就不需要也不能传实参。

（2）调用时，如果方法有返回值，可以接受或处理返回值结果，当然也可以不接收，那么此时返回值就丢失了。

​		如果方法的返回值类型是void，不需要也不能接收和处理返回值结果。

### 5.5.6 在本类中访问本类的成员变量和成员方法

**直接用，不需要加“对象名."和"类名."**

唯一例外：**静态方法中不能直接访问本类的非静态的成员变量和成员方法**

```java
class Circle{
	double radius;
	
	//写一个方法，可以返回“圆对象”的详细信息
	String getDetailInfo(){
		return "半径：" + radius + "，面积：" + area() +"，周长：" + perimeter();
	}
	
	//写一个方法，可以返回“圆对象”的面积
	double area(){
		return Math.PI*radius*radius;
	}
	
	//写一个方法，可以返回“圆对象”的周长
	double perimeter(){
		return 2*Math.PI*radius;
	}

}

```

```java
class Test{
		
	static void test(){
		System.out.println("");
	}
	void method(){
		 test();
	}
    
    public static void main(String[] args){
        method();//错误
        test();//正确
    }
}

```

### 5.5.7 方法的声明与调用练习

1、声明数学工具类MathTools

（1）静态方法1：可以比较两个整数是否相同
（2）静态方法2：可以判断某个数是否是素数
（3）静态方法3：可以返回某个整数所有的约数（约数：从1到这个数之间所有能把它整除的数）
在Test测试类的main中调用测试

2、声明数组工具类ArraysTools

（1）静态方法1：可以实现给任意整型数组实现从小到大排序
（2）静态方法2：可以遍历任意整型数组，返回结果效果：[元素1，元素2，元素3。。。]

3、声明矩形类

（1）包含属性：长、宽

（2）包含3个方法：

​	求面积、

​	求周长、

​	返回矩形对象的信息：长：xx，宽：xx，面积：xx，周长：xx

4、声明一个圆类，有半径radius成员变量

​     声明一个图形工具类GraphicTools，包含一个静态方法可以返回两个圆中面积大的那一个圆的方法

​	在测试类中测试

### 5.5.8 方法调用内存分析

方法不调用不执行，调用一次执行一次，每次调用会在栈中有一个入栈动作，即给当前方法开辟一块独立的内存区域，用于存储当前方法的局部变量的值，当方法执行结束后，会释放该内存，称为出栈，如果方法有返回值，就会把结果返回调用处，如果没有返回值，就直接结束，回到调用处继续执行下一条指令。

栈结构：先进后出，后进先出。

示例一：

```java
public class TestCount {
	public static void main(String[] args) {
        int a = 4;
        int b = 2;
		int m = CountTools.max(a, b));
	}
}
class CountTools{
	static int max(int a, int b) {
		return a > b ? a : b;
	}
}

```

![1572349992849](https://raw.githubusercontent.com/zxingq/Picture/main/202211172134689.png)

示例二：

```java
public class TestCircle {
	public static void main(String[] args) {
		Circle c1 = new Circle();
		c1.radius = 1.2;
		int area1 = c1.area();
		
		Circle c2 = new Circle();
		c2.radius = 2.5;
		int area2 = c2.area();
	}
}
class Circle{
	double radius;
	public double area() {
		return Math.PI * radius * radius;
	}
}

```

![1572350522409](https://raw.githubusercontent.com/zxingq/Picture/main/202211172134966.png)

示例三：

```java
public class Test {
	public static void main(String[] args) {
		int[] arr = {2,4,1,5,3};
		
		ArrayUtil.sort(arr);
		
		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i]);
		}
	}
}
class ArrayUtil{
	public static void sort(int[] arr){
		for (int i = 1; i < arr.length; i++) {
			for (int j = 0; j < arr.length - i; j++) {
				if(arr[j] > arr[j+1]){
					int temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}
			}
		}
	}
}

```

![1572350909017](https://raw.githubusercontent.com/zxingq/Picture/main/202211172134400.png)

### 5.5.9 方法的参数传递机制

* 方法的参数传递机制：实参给形参赋值
  * 方法的形参是**基本数据类型**时，**形参值的改变不会影响实参**；
  * 方法的形参是**引用数据类型**时，**形参地址值的改变不会影响实参，但是形参地址值里面的数据的改变会影响实参**，例如，修改数组元素的值，或修改对象的属性值。
    * 注意：String、Integer等特殊类型容易错

示例代码1：

```java
class Test{
    public static void swap(int a, int b){
        int temp = a;
        a = b;
        b = temp;
	}

	public static void main（String[] args){
        int x = 1;
        int y = 2;
        swap(x,y);//调用完之后，x与y的值不变
    }
}


```

示例代码2：

```java
class Test{
    public static void change(MyData my){
        my.num *= 2;
    }
    
    public static void main(String[] args){
        MyData m = new MyData();
        m.num = 1;
        
        change(m);//调用完之后，m对象的num属性值就变为2
    }
}

class MyData{
    int num;
}

```

示例代码3：

```java
public class Test {
	public static void main(String[] args) {
		int[] arr = {2,4,1,5,3};
		
		ArrayUtil.sort(arr);
		
		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i]);
		}
	}
}
class ArrayUtil{
	public static void sort(int[] arr){
		for (int i = 1; i < arr.length; i++) {
			for (int j = 0; j < arr.length - i; j++) {
				if(arr[j] > arr[j+1]){
					int temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}
			}
		}
	}
}

```

陷阱1：

```java
/*
陷阱1：在方法中，形参 = 新new对象，那么就和实参无关了
*/
class Test{
    public static void change(MyData my){
        my = new MyData();//形参指向了新对象
        my.num *= 2;
    }
    
    public static void main(String[] args){
        MyData m = new MyData();
        m.num = 1;
        
        change(m);//调用完之后，m对象的num属性值仍然为1
    }
}

class MyData{
    int num;
}

```

陷阱2：见字符串和包装类部分

```java
public class Test {
	public static void main(String[] args) {
		StringUtil util = new StringUtil();
		String str = "尚硅谷";
		util.change(str);
		System.out.println(str);
	}
}
class StringUtil{
	public void change(String str){
		str += "你好";//String对象不可变，一旦修改就会产生新对象
	}
}

```

### 5.5.10 成员变量与局部变量的区别

#### 1、变量的分类

* 成员变量
  * 静态变量
  * 实例变量

* 局部变量

#### 2、区别

1、声明位置和方式
（1）静态变量：在类中方法外，并且有static修饰
（2）实例变量：在类中方法外，没有static修饰
（3）局部变量：在方法体 { } 中或方法的形参列表、代码块中

2、在内存中存储的位置不同
（1）静态变量：方法区
（2）实例变量：堆
（3）局部变量：栈

3、生命周期
（1）静态变量：和类的生命周期一样，因为它的值是该类所有对象共享的，早于对象的创建而存在。
（2）实例变量：和对象的生命周期一样，随着对象的创建而存在，随着对象被GC回收而消亡，
			而且每一个对象的实例变量是独立的。
（3）局部变量：和方法调用的生命周期一样，每一次方法被调用而在存在，随着方法执行的结束而消亡，
			而且每一次方法调用都是独立。

4、作用域
（1）静态变量和实例变量：不谈作用域
在本类中，唯一的限制，**静态方法或静态代码块中不能使用非静态的**，其他都可以直接使用。
在其他类中，能不能使用看修饰符（public,protected,private等）
（2）局部变量：有作用域
出了作用域就不能使用

5、修饰符（后面来讲）
（1）静态变量：很多
public,protected,private,final,volatile等，一定有的是static
（2）实例变量
public,protected,private,final,volatile,transient等
（3）局部变量
final

public,protected,private：权限修饰符
final：是否是常量，即值是否可以修改
volatile：和多线程有关
transient：是否序列化，和IO有关	

6、默认值
（1）静态变量：有默认值
（2）实例变量：有默认值
（3）局部变量：没有，必须初始化
		其中的形参比较特殊，靠实参给它初始化。

## 5.6 可变参数

在**JDK1.5**之后，如果我们定义一个方法时，此时某个形参的类型可以确定，但是形参的个数不确定，那么我们可以使用可变参数。

格式：

```
【修饰符】 返回值类型 方法名(【非可变参数部分的形参列表,】参数类型... 形参名){  }

```

要求：

（1）一个方法最多只能有一个可变参数

（2）如果一个方法包含可变参数，那么可变参数必须是形参列表的最后一个

```
【修饰符】 返回值类型 方法名(【非可变参数部分的形参列表,】参数类型[] 形参名){  }
public static void  fun(String s1,double d,int...nums){ }

```

只是后面这种定义，在调用时必须传递数组，而前者更灵活，既可以传递数组，又可以直接传递数组的元素，这样更灵活了。

## 5.7 方法重载

- **方法重载**：指在同一个类中，允许存在一个以上的同名方法，只要它们的参数列表不同即可，与修饰符和返回值类型无关。
- 参数列表：数据类型个数不同，数据类型不同，数据类型顺序不同。
- 重载方法调用：JVM通过方法的参数列表，调用不同的方法。

#### 示例一：比较两个数据是否相等

比较两个数据是否相等。参数类型分别为两个`byte`类型，两个`short`类型，两个`int`类型，两个`long`类型，并在`main`方法中进行测试。 

```java
public class Method_Demo6 {
    public static void main(String[] args) {
        //定义不同数据类型的变量
        byte a = 10;
        byte b = 20;
        short c = 10;
        short d = 20;
        int e = 10;
        int f = 10;
        long g = 10;
        long h = 20;
        // 调用
        System.out.println(compare(a, b));
        System.out.println(compare(c, d));
        System.out.println(compare(e, f));
        System.out.println(compare(g, h));
    }
    // 两个byte类型的
    public static boolean compare(byte a, byte b) {
        System.out.println("byte");
        return a == b;
    }

    // 两个short类型的
    public static boolean compare(short a, short b) {
        System.out.println("short");
        return a == b;
    }

    // 两个int类型的
    public static boolean compare(int a, int b) {
        System.out.println("int");
        return a == b;
    }

    // 两个long类型的
    public static boolean compare(long a, long b) {
        System.out.println("long");
        return a == b;
    }
}

```

#### 示例二：求各种最大值

用重载实现：
定义方法求两个整数的最大值
定义方法求三个整数的最大值
定义方法求两个小数的最大值

```java
//求两个整数的最大值
public int max(int a,int b){
    return a>b?a:b;
}
	
//求三个整数的最大值
public int max(int a, int b, int c){
    return max(max(a,b),c);
}
	
//求两个小数的最大值
public double max(double a, double b){
    return a>b?a:b;
}

```

## 5.8  对象数组

数组是用来存储一组数据的容器，一组基本数据类型的数据可以用数组装，那么一组对象也可以使用数组来装。

即数组的元素可以是基本数据类型，也可以是引用数据类型。当元素是引用数据类型是，我

们称为对象数组。

> 注意：对象数组，首先要创建数组对象本身，即确定数组的长度，然后再创建每一个元素对象，如果不创建，数组的元素的默认值就是null，所以很容易出现空指针异常NullPointerException。

### 示例一：

（1）定义圆Circle类，包含radius半径属性，getArea()求面积方法，getPerimeter()求周长方法，String getInfo()返回圆对象的详细信息的方法

（2）在测试类中创建长度为5的Circle[]数组，用来装5个圆对象，并给5个圆对象的半径赋值为[1,10)的随机值

```java
class Test16_ObjectArray{
	public static void main(String[] args){
		//要在数组中存储5个圆对象
		//声明一个可以用来存储圆对象的数组
		Circle[] arr = new Circle[5];
		//for(int i=0; i<arr.length; i++){
		//	System.out.println(arr[i]);
		//}
		//System.out.println(arr[0].radius);//NullPointerException
		
		//给元素赋值
		//元素的类型是：Circle，应该给它一个Circle的对象
		//arr[0] = 1.2;//错误的
		//arr[0]相当于它是一个Circle类型的变量，也是对象名，必须赋值为对象
		/*
		arr[0] =  new Circle();
		arr[0].radius = 1.2;
		System.out.println(arr[0].radius);
		*/
		
		//创建5个对象，半径随机赋值为[1,10)的随机值
		//Math.random()==>[0,1)
		//Math.random()*9==>[0,9)
		//Math.random()*9+1==>[1,10)
		for(int i=0; i<arr.length; i++){
			arr[i] = new Circle();//有对象才有半径
			arr[i].radius = Math.random()*9+1;
		}
		
		
		//遍历显示圆对象的信息
		for(int i=0; i<arr.length; i++){
			//arr[i]是一个Circle的对象，就可以调用Circle类中的属性和方法
			System.out.println(arr[i].getInfo());
		}
	}
}
class Circle{
	double radius;
	public double getArea(){
		return 3.14 * radius * radius;
	}
	public double getPerimeter(){
		return 3.14 * 2 * radius;
	}
	public String getInfo(){
		return "半径：" + radius +"，面积：" + getArea() + "，周长：" + getPerimeter();
	}
}

```



### 练习1

（1）定义学生类Student

​	声明姓名和成绩实例变量，

​	getInfo()方法：用于返回学生对象的信息

（2）测试类ObjectArrayTest的main中创建一个可以装3个学生对象的数组，并且按照学生成绩排序，显示学生信息

```java
public class ObjectArrayTest {
	public static void main(String[] args) {
		Student[] arr = new Student[3];
		arr[0] = new Student();
		arr[0].name = "张三";
		arr[0].score = 89;
		
		arr[1] = new Student();
		arr[1].name = "李四";
		arr[1].score = 84;
		
		arr[2] = new Student();
		arr[2].name = "王五";
		arr[2].score = 85;
		
		for (int i = 1; i < arr.length; i++) {
			for (int j = 0; j < arr.length-1; j++) {
				if(arr[j].score > arr[j+1].score){
					Student temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}
			}
		}
		
		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i].getInfo());
		}
	}
}
class Student{
	String name;
	int score;
	public String getInfo(){
		return "姓名：" + name + ",成绩：" + score;
	}
}

```

```java
class Test18_ObjectArrayExer2_2{
	public static void main(String[] args){
		//创建一个可以装3个学生对象的数组
		Student[] arr = new Student[3];//只是申明这个数组，可以用来装3个学生，此时里面没有学生对象
		
		//从键盘输入
		java.util.Scanner input = new java.util.Scanner(System.in);
		for(int i=0;i<arr.length; i++){
			System.out.println("请输入第" + (i+1) + "个学生信息：");
			arr[i] = new Student();
			
			System.out.print("姓名：");
			arr[i].name = input.next();
			
			System.out.print("成绩：");
			arr[i].score = input.nextInt();
		}
		
		//先显示一下目前的顺序
		for(int i=0; i<arr.length; i++){
			System.out.println(arr[i].getInfo());
		}
		
		System.out.println("-------------------------------");
		//冒泡排序
		for(int i=1; i<arr.length; i++){
			for(int j=0; j<arr.length-i; j++){
				//arr[j] > arr[j+1]//错误的
				if(arr[j].score > arr[j+1].score){
					//交换两个元素，这里是两个学生对象，所以temp也得是Student类型
					Student temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}
			}
		}
		//再显示一下目前的顺序
		for(int i=0; i<arr.length; i++){
			System.out.println(arr[i].getInfo());
		}
	}
}
class Student{
	String name;
	int score;//使用int或double都可以
	
	public String getInfo(){
		return "姓名：" + name +"，成绩：" + score;
	}
}

```



# JavaSE_day07【面向对象基础--中】

## 今日内容

* 封装
* 权限修饰符
* 包
* 构造器
* 代码块

## 教学目标

* [ ] 理解封装的概念
* [ ] 掌握权限修饰符的使用
* [ ] 掌握属性的封装
* [ ] 理解包的作用
* [ ] 掌握包的声明与导入
* [ ] 掌握构造器的声明与使用
* [ ] 掌握this关键字的使用
* [ ] 会声明标准的JavaBean

# 第六章 面向对象基础--中

## 6.1 封装

### 6.1.1 封装概述

#### 1、为什么需要封装？

* 我要用洗衣机，只需要按一下开关和洗涤模式就可以了。有必要了解洗衣机内部的结构吗？有必要碰电动机吗？
* 我们使用的电脑，内部有CPU、硬盘、键盘、鼠标等等，每一个部件通过某种连接方式一起工作，但是各个部件之间又是独立的
* 现实生活中，每一个个体与个体之间是有边界的，每一个团体与团体之间是有边界的，而同一个个体、团体内部的信息是互通的，只是对外有所隐瞒。

面向对象编程语言是对客观世界的模拟，客观世界里每一个事物的内部信息都是隐藏在对象内部的，外界无法直接操作和修改，只能通过指定的方式进行访问和修改。封装可以被认为是一个保护屏障，防止该类的代码和数据被其他类随意访问。适当的封装可以让代码更容易理解与维护，也加强了代码的安全性。

随着我们系统越来越复杂，类会越来越多，那么类之间的访问边界必须把握好，面向对象的开发原则要遵循“高内聚、低耦合”，而“高内聚，低耦合”的体现之一：

* 高内聚：类的内部数据操作细节自己完成，不允许外部干涉；
* 低耦合：仅对外暴露少量的方法用于使用

隐藏对象内部的复杂性，只对外公开简单的接口。便于外界调用，从而提高系统的可扩展性、可维护性。通俗的讲，把该隐藏的隐藏起来，该暴露的暴露出来。这就是封装性的设计思想。

#### 2、如何实现封装呢？

通俗的讲，封装就是把该隐藏的隐藏起来，该暴露的暴露出来。那么暴露的程度如何控制呢？就是依赖访问控制修饰符，也称为权限修饰符来控制。

访问控制修饰符来控制相应的可见边界，边界有如下：

（1）类

（2）包

（3）子类

（4）模块：Java9 之后引入

权限修饰符：public,protected,缺省,private

| 修饰符    | 本类 | 本包 | 其他包子类 | 其他包非子类 | 其他模块                 |
| --------- | ---- | ---- | ---------- | ------------ | ------------------------ |
| private   | √    | ×    | ×          | ×            | ×                        |
| 缺省      | √    | √    | ×          | ×            | ×                        |
| protected | √    | √    | √          | ×            | ×                        |
| public    | √    | √    | √          | √            | 默认不可以，可以建立依赖 |

外部类：public和缺省

成员变量：public,protected,缺省,private

成员方法：public,protected,缺省,private

构造器：public,protected,缺省,private



### 6.1.2 成员变量/属性私有化问题

**<span style="color:red">成员变量（field）私有化</span>之后，提供标准的<span style="color:red">get/set</span>方法，我们把这种成员变量也称为<span style="color:red">属性（property）</span>。**或者可以说只要能通过get/set操作的就是事物的属性，哪怕它没有对应的成员变量。

#### 1、成员变量封装的目的

* 隐藏类的实现细节
* 让使用者只能通过事先预定的方法来访问数据，**从而可以在该方法里面加入控制逻辑，限制对成员变量的不合理访问**。**还可以进行数据检查，从而有利于保证对象信息的完整性**。
* **便于修改，提高代码的可维护性**。主要说的是隐藏的部分，在内部修改了，如果其对外可以的访问方式不变的话，外部根本感觉不到它的修改。例如：Java8->Java9，String从char[]转为byte[]内部实现，而对外的方法不变，我们使用者根本感觉不到它内部的修改。

#### 2、实现步骤

1. 使用 `private` 修饰成员变量

```java
private 数据类型 变量名 ；
```

代码如下：

```java
public class Chinese {
    private static String country;
    private String name;
  	private int age;
    private boolean marry;
}
```

2. 提供 `getXxx`方法 / `setXxx` 方法，可以访问成员变量，代码如下：

```java
public class Chinese {
  	private static String country;
    private String name;
  	private int age;
    private boolean marry;
    
    public static void setCountry(String c){
        country = c;
    }
    
    public static String getCountry(){
        return country;
    }

	public void setName(String n) {
		name = n;
    }

    public String getName() {
        return name;
	}

    public void setAge(int a) {
        age = a;
    }

    public int getAge() {
        return age;
    }
    
    public void setMarry(boolean m){
        marry = m;
    }
    
    public boolean isMarry(){
        return marry;
    }
}
```

#### 3、如何解决局部变量与成员变量同名问题

当局部变量与类变量（静态成员变量）同名时，在类变量前面加“类名."；

当局部变量与实例变量（非静态成员变量）同名时，在实例变量前面加“this.”

```java
public class Chinese {
  	private static String country;
    private String name;
  	private int age;
    
    public static void setCountry(String country){
        Chinese.country = country;
    }
    
    public static String getCountry(){
        return country;
    }

	public void setName(String name) {
		this.name = name;
    }

    public String getName() {
        return name;
	}

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}
```

#### 4、 练习

（1）定义矩形类Rectangle，

​	声明静态变量sides，初始化为4，表示矩形边长的总数量；

​	声明实例变量长和宽

​	全部私有化，并提供相应的get/set方法

（2）在测试类中创建Rectangle对象，并调用相应的方法测试

（2）测试类ObjectArrayTest的main中创建一个可以装3个学生对象的数组，并且按照学生成绩排序，显示学生信息



### 6.1.3 包（Package）

#### 1、包的作用

（1）可以避免类重名：有了包之后，类的全名称就变为：包.类名

（2）分类组织管理众多的类

例如：

* java.lang----包含一些Java语言的核心类，如String、Math、Integer、 System和Thread等，提供常用功能
* java.net----包含执行与网络相关的操作的类和接口。
* java.io ----包含能提供多种输入/输出功能的类。
* java.util----包含一些实用工具类，如集合框架类、日期时间、数组工具类Arrays，文本扫描仪Scanner，随机值产生工具Random。
* java.text----包含了一些java格式化相关的类
* java.sql和javax.sql----包含了java进行JDBC数据库编程的相关类/接口
* java.awt和java.swing----包含了构成抽象窗口工具集（abstract window toolkits）的多个类，这些类被用来构建和管理应用程序的图形用户界面(GUI)。

（3）可以控制某些类型或成员的可见范围

如果某个类型或者成员的权限修饰缺省的话，那么就仅限于本包使用

#### 2、声明包的语法格式

```java
package 包名;
```

> 注意：
>
> (1)必须在源文件的代码首行
>
> (2)一个源文件只能有一个声明包的语句

包的命名规范和习惯：
（1）所有单词都小写，每一个单词之间使用.分割
（2）习惯用公司的域名倒置

例如：com.atguigu.xxx;

> 建议大家取包名时不要使用“java.xx"包

#### 3、如何在命令行编译和运行声明包的Java文件（了解）

编译格式：

```
javac -d class文件存放路径 源文件路径名.java
```

例如：

```java
package com.atguigu.demo;

public class TestPackage {
	public static void main(String[] args) {
		System.out.println("hello package");
	}
}
```

编译：

```java
javac -d . TestPackage.java
```

> 其中 . 表示在当前目录生成包目录

运行：

```java
java com.atguigu.demo.TestPackage

```

> 定位到com目录的外面才能正确找到这个类
>
> 使用类的全名称才能正确运行这个类

![1561887467445](https://raw.githubusercontent.com/zxingq/Picture/main/202211181703507.png)

#### 4、如何跨包使用类

前提：被使用的类或成员的权限修饰符是>缺省的，即可见的

（1）使用类型的全名称

例如：java.util.Scanner input = new java.util.Scanner(System.in);

（2）使用import 语句之后，代码中使用简名称

import语句告诉编译器到哪里去寻找类。

import语句的语法格式：

```java
import 包.类名;
import 包.*;
import static 包.类名.静态成员;

```

> 注意：
>
> 使用java.lang包下的类，不需要import语句，就直接可以使用简名称
>
> import语句必须在package下面，class的上面
>
> 当使用两个不同包的同名类时，例如：java.util.Date和java.sql.Date。一个使用全名称，一个使用简名称



示例代码：

```java
package com.atguigu.bean;

public class Student {
	// 成员变量
	private String name;
	private int age;

	// 构造方法
	public Student() {
	}

	public Student(String name, int age) {
		this.name = name;
		this.age = age;
	}

	// 成员方法
	public void setName(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public int getAge() {
		return age;
	}
}

```

```java
package com.atguigu.test;

import java.util.Scanner;
import java.util.Date;
import com.atguigu.bean.Student;

public class Test{
    public static void main(String[] args){
        Scanner input = new Scanner(System.in);
        Student stu = new Student();
        String str = "hello";
        
        Date now = new Date();
        java.sql.Date d = new java.sql.Date(346724566);        
    }
}

```



## 6.2 构造器（Constructor)

我们发现我们new完对象时，所有成员变量都是默认值，如果我们需要赋别的值，需要挨个为它们再赋值，太麻烦了。我们能不能在new对象时，直接为当前对象的某个或所有成员变量直接赋值呢。

可以，Java给我们提供了构造器。

#### 1、构造器的作用

在创建对象的时候为实例变量赋初始值。

> **注意：构造器只为实例变量初始化，不为静态类变量初始化**

#### 2、构造器的语法格式

构造器又称为构造方法，那是因为它长的很像方法。但是和方法还有有所区别的。

```java
【修饰符】 构造器名(){
    // 实例初始化代码
}
【修饰符】 构造器名(参数列表){
	// 实例初始化代码
}

```

代码如下：

```java
public class Student {
	private String name;
	private int age;
	// 无参构造
  	public Student() {} 
 	// 有参构造
  	public Student(String name,int age) {
		this.name = name;
    	this.age = age; 
	}
  	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
}

```

注意事项：

1. 构造器名必须与它所在的类名必须相同。
2. 它没有返回值，所以不需要返回值类型，甚至不需要void
3. 如果你不提供构造器，系统会给出无参数构造器，并且该构造器的修饰符默认与类的修饰符相同
4. 如果你提供了构造器，系统将不再提供无参数构造器，除非你自己定义。
5. 构造器是可以重载的，既可以定义参数，也可以不定义参数。
6. 构造器的修饰符只能是权限修饰符，不能被其他任何修饰

#### 3、练习

（1）声明一个员工类，

* 包含属性：编号、姓名、薪资、性别，要求属性私有化，提供get/set，
* 提供无参构造器和有参构造器
* 提供getInfo()

（2）在测试类的main中分别用无参构造和有参构造创建员工类对象，调用getInfo

```java
public class TestEmployee {
	public static void main(String[] args){
		//分别用无参构造和有参构造创建对象，调用getInfo
		Employee e1 = new Employee();
		System.out.println(e1.getInfo());
		
		Employee e2 = new Employee("1001","张三",110000,'男');
		System.out.println(e2.getInfo());
		
		e2.setSalary(120000);
		System.out.println(e2.getInfo());
		
		System.out.println("e1薪资：" + e1.getSalary());
	}
}
class Employee{
	private String id;
	private String name;
	private double salary;
	private char gender;
	
	//提供无参构造器和有参构造器
	public Employee(){
		
	}
	public Employee(String id, String name){
		this.id = id;
		this.name = name;
	}
	public Employee(String id, String name, double salary, char gender){
		this.id = id;
		this.name = name;
		this.salary = salary;
		this.gender = gender;
	}
	
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public double getSalary() {
		return salary;
	}
	public void setSalary(double salary) {
		this.salary = salary;
	}
	public char getGender() {
		return gender;
	}
	public void setGender(char gender) {
		this.gender = gender;
	}
	
	//提供getInfo()
	public String getInfo(){
		return "编号：" + id + "，姓名：" + name + "，薪资：" + salary + "，性别：" +gender;
	}
}

```

## 6.3 标准JavaBean

`JavaBean` 是 Java语言编写类的一种标准规范。符合`JavaBean` 的类，要求：

（1）类必须是具体的和公共的，

（2）并且具有无参的构造方法，

（3）成员变量私有化，并提供用来操作成员变量的`set` 和`get` 方法。

```java
public class ClassName{
  //成员变量
    
  //构造方法
  	//无参构造方法【必须】
  	//有参构造方法【建议】
  	
  //getXxx()
  //setXxx()
  //其他成员方法
}

```

 编写符合`JavaBean` 规范的类，以学生类为例，标准代码如下：

```java
public class Student {
	// 成员变量
	private String name;
	private int age;

	// 构造方法
	public Student() {
	}

	public Student(String name, int age) {
		this.name = name;
		this.age = age;
	}

	// get/set成员方法
	public void setName(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public int getAge() {
		return age;
	}
    
    //其他成员方法列表
    public String getInfo(){
        return "姓名：" + name + "，年龄：" + age;
    }
}

```

测试类，代码如下：

```java
public class TestStudent {
	public static void main(String[] args) {
		// 无参构造使用
		Student s = new Student();
		s.setName("柳岩");
		s.setAge(18);
		System.out.println(s.getName() + "---" + s.getAge());
        System.out.println(s.getInfo());

		// 带参构造使用
		Student s2 = new Student("赵丽颖", 18);
		System.out.println(s2.getName() + "---" + s2.getAge());
        System.out.println(s2.getInfo());
	}
}

```

# JavaSE_day08【继承、初始化】

## 今日内容

- 继承
- 方法重写
- this关键字
- super关键字
- final修饰符
- 类初始化
- 实例初始化

## 学习目标

- [ ] 能够写出类的继承格式
- [ ] 能够说出继承的特点
- [ ] 能够说出方法重写的概念以及和重载的区别
- [ ] 能够使用this关键字解决问题
- [ ] 能够使用super关键字解决问题
- [ ] 掌握final的使用
- [ ] 能够分析类初始化过程（为面试服务）
- [ ] 能够分析实例初始化过程（为面试服务）

# 第六章 面向对象基础--中（续）

## 6.4 继承

### 6.4.1 继承的概述

#### 生活中的继承

* 财产：富二代

* 样貌：如图所示：

  ![](https://raw.githubusercontent.com/zxingq/Picture/main/202211202041966.jpg)

  ![](https://raw.githubusercontent.com/zxingq/Picture/main/202211202041284.jpg)

  ![](E:\大数据\01-java基础\day01—6\第一阶段课件\第一阶段课件\day08_note\imgs\继承3.jpg)

* 才华：如图所示：

  ![](https://raw.githubusercontent.com/zxingq/Picture/main/202211202041133.jpg)

#### 继承的由来

如图所示：

![](E:\大数据\01-java基础\day01—6\第一阶段课件\第一阶段课件\day08_note\imgs\猫狗继承1.jpg)

多个类中存在相同属性和行为时，将这些内容抽取到单独一个类中，那么多个类中无需再定义这些属性和行为，只需要和抽取出来的类构成某种关系。如图所示：

![](https://raw.githubusercontent.com/zxingq/Picture/main/202211202041905.jpg)

其中，多个类可以称为**子类**，也叫**派生类**；多个类抽取出来的这个类称为**父类**、**超类（superclass）**或者**基类**。

继承描述的是事物之间的所属关系，这种关系是：`is-a` 的关系。例如，图中猫属于动物，狗也属于动物。可见，父类更通用，子类更具体。我们通过继承，可以使多种事物之间形成一种关系体系。

#### 继承的好处

* 提高**代码的复用性**。

* 提高**代码的扩展性**。

* 类与类之间产生了关系，是学习**多态的前提**。

### 6.4.2 继承的格式

通过 `extends` 关键字，可以声明一个子类继承另外一个父类，定义格式如下：

```java
【修饰符】 class 父类 {
	...
}

【修饰符】 class 子类 extends 父类 {
	...
}

```

继承演示，代码如下：

```java
/*
 * 定义动物类Animal，做为父类
 */
class Animal {
    // 定义name属性
	String name; 
    // 定义age属性
    int age;
	// 定义动物的吃东西方法
	public void eat() {
		System.out.println(age + "岁的" + name + "在吃东西");
	}
}

/*
 * 定义猫类Cat 继承 动物类Animal
 */
class Cat extends Animal {
	// 定义一个猫抓老鼠的方法catchMouse
	public void catchMouse() {
		System.out.println("抓老鼠");
	}
}

/*
 * 定义测试类
 */
public class ExtendDemo01 {
	public static void main(String[] args) {
        // 创建一个猫类对象
		Cat cat = new Cat()；
      
        // 为该猫类对象的name属性进行赋值
		cat.name = "Tom";
      
      	// 为该猫类对象的age属性进行赋值
		cat.age = 2;
        
        // 调用该猫的catchMouse()方法
		cat.catchMouse();
		
      	// 调用该猫继承来的eat()方法
      	cat.eat();
	}
}

演示结果：
抓老鼠
2岁的Tom在吃东西
```

### 6.4.3 继承的特点一：成员变量

#### 1、父类成员变量私有化（private）

* 父类中的成员，无论是公有(public)还是私有(private)，均会被子类继承。
* 子类虽会继承父类私有(private)的成员，但子类不能对继承的私有成员直接进行访问，可通过继承的get/set方法进行访问。如图所示：

![](https://raw.githubusercontent.com/zxingq/Picture/main/202211191744612.jpg)

代码如下：

```java
/*
 * 定义动物类Animal，做为父类
 */
class Animal {
    // 定义name属性
	private String name; 
    // 定义age属性
    public int age;
	// 定义动物的吃东西方法
	public void eat() {
		System.out.println(age + "岁的" + name + "在吃东西");
	}
}

/*
 * 定义猫类Cat 继承 动物类Animal
 */
class Cat extends Animal {
	// 定义一个猫抓老鼠的方法catchMouse
	public void catchMouse() {
		System.out.println("抓老鼠");
	}
}

/*
 * 定义测试类
 */
public class ExtendDemo01 {
	public static void main(String[] args) {
        // 创建一个猫类对象
		Cat cat = new Cat()；
      
        // 为该猫类对象的name属性进行赋值
		//cat.name = "Tom";// 编译报错
      
      	// 为该猫类对象的age属性进行赋值
		cat.age = 2;
        
        // 调用该猫的catchMouse()方法
		cat.catchMouse();
		
      	// 调用该猫继承来的eat()方法
      	cat.eat();
	}
}
```

如图所示：

eclipse中Debug查看对象成员变量值的情况截图如下：

![](https://raw.githubusercontent.com/zxingq/Picture/main/202211191747660.jpg)

idea中Debug查看对象成员变量值的情况截图如下：

![1576579518956](https://raw.githubusercontent.com/zxingq/Picture/main/202211192023851.png)

#### 2、父子类成员变量重名

我们说父类的所有成员变量都会继承到子类中，那么如果子类出现与父类同名的成员变量会怎么样呢？

父类代码：

```java
public class Father {
	public int i=1;
	private int j=1;
	public int k=1;
	public int getJ() {
		return j;
	}
	public void setJ(int j) {
		this.j = j;
	}
}
```

子类代码：

```java
public class Son extends Father{
	public int i=2;
	private int j=2;
	public int m=2;
}	
```

现在想要在子类Son中声明一个test()方法，并打印这些所有变量的值，该如何实现？

```java
public class Son extends Father{
	public int i=2;
	private int j=2;
	public int m=2;
	
	public void test() {
		System.out.println("父类继承的i：" + super.i);
		System.out.println("子类的i：" +i);
//		System.out.println(super.j);
		System.out.println("父类继承的j：" +getJ());
		System.out.println("子类的j：" +j);
		System.out.println("父类继承的k：" +k);
		System.out.println("子类的m：" +m);
	}	
}	
```

结论：

（1）当父类的成员变量私有化时，在子类中是无法直接访问的，所以是否重名不影响，如果想要访问父类的私有成员变量，只能通过父类的get/set方法访问；

（2）当父类的成员变量非私有时，在子类中可以直接访问，所以如果有重名时，就需要加“super."进行区别。

使用格式：

```java
super.父类成员变量名
```

以上test()调用结果：

```java
public class TestSon{
	public static void main(String[] args){
		Son s = new Son();
		s.test();
	}
}
```

```java
父类继承的i：1
子类的i：2
父类继承的j：1
子类的j：2
父类继承的k：1
子类的m：2

```

eclipse中Debug查看对象的成员变量的值截图如下：

![1572422069292](https://raw.githubusercontent.com/zxingq/Picture/main/202211191749265.png)

idea中Debug查看对象的成员变量的值截图如下：

![1576579731205](https://raw.githubusercontent.com/zxingq/Picture/main/202211191749417.png)

> 说明：虽
>
> 然我们可以区分父子类的重名成员变量，但是实际开发中，我们不建议这么干。

### 6.4.4 继承的特点二：成员方法

我们说父类的所有方法子类都会继承，但是当某个方法被继承到子类之后，子类觉得父类原来的实现不适合于子类，该怎么办呢？我们可以进行方法重写 (Override)

#### 1、方法重写

比如新的手机增加来电显示头像的功能，代码如下：

```java
class Phone {
	public void sendMessage(){
		System.out.println("发短信");
	}
	public void call(){
		System.out.println("打电话");
	}
	public void showNum(){
		System.out.println("来电显示号码");
	}
}

//智能手机类
class NewPhone extends Phone {
	
	//重写父类的来电显示号码功能，并增加自己的显示姓名和图片功能
	public void showNum(){
		//调用父类已经存在的功能使用super
		super.showNum();
		//增加自己特有显示姓名和图片功能
		System.out.println("显示来电姓名");
		System.out.println("显示头像");
	}
}

public class ExtendsDemo06 {
	public static void main(String[] args) {
      	// 创建子类对象
      	NewPhone np = new NewPhone()；
        
        // 调用父类继承而来的方法
        np.call();
      
      	// 调用子类重写的方法
      	np.showNum();

	}
}


```

> 小贴士：这里重写时，用到super.父类成员方法，表示调用父类的成员方法。

注意事项：

1.@Override：写在方法上面，用来检测是不是有效的正确覆盖重写。这个注解就算不写，只要满足要求，也是正确的方法覆盖重写。建议保留

2.必须保证父子类之间方法的名称相同，参数列表也相同。
3.子类方法的返回值类型必须【小于等于】父类方法的返回值类型（小于其实就是是它的子类，例如：Student < Person）。

> 注意：如果返回值类型是基本数据类型和void，那么必须是相同

4.子类方法的权限必须【大于等于】父类方法的权限修饰符。
小扩展提示：public > protected > 缺省 > private

5.几种特殊的方法不能被重写

* 静态方法不能被重写
* 私有等在子类中不可见的方法不能被重写
* final方法不能被重写

#### 2、方法的重载

（1）同一个类中

```java
class Test{
	public int max(int a, int b){
		return a > b ? a : b;
	}
	public double max(double a, double b){
		return a > b ? a : b;
	}
	public int max(int a, int b,int c){
		return max(max(a,b),c);
	}
}

```

（2）父子类中

```java
class Father{
	public void print(int i){
		System.out.println("i = " + i);
	}
}
class Son extends Father{
	public void print(int i,int j){
		System.out.println("i = " + i  ",j = " + j);
	}
}

```

> 对于Son类，相当于有两个print方法，一个形参列表是(int i)，一个形参列表(int i, int j)

### 6.4.5 继承的特点三：构造方法

当类之间产生了关系，其中各类中的构造方法，又产生了哪些影响呢？

首先我们要回忆两个事情，构造方法的定义格式和作用。

1. 构造方法的名字是与类名一致的。

   所以子类是**无法继承**父类构造方法的。

2. 构造方法的作用是初始化实例变量的，而子类又会从父类继承所有成员变量

   所以子类的初始化过程中，**必须**先执行父类的初始化动作。子类的构造方法中默认有一个`super()` ，表示调用父类的实例初始化方法，父类成员变量初始化后，才可以给子类使用。代码如下：

```java
class Fu {
  private int n;
  Fu(){
    System.out.println("Fu()");
  }
}
class Zi extends Fu {
  Zi(){
    // super（），调用父类构造方法
    super();
    System.out.println("Zi（）");
  }  
}
public class ExtendsDemo07{
  public static void main (String args[]){
    Zi zi = new Zi();
  }
}
输出结果：
Fu（）
Zi（）

```

如果父类没有无参构造怎么办？

```java
public class Person {
	private String name;
	private int age;
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
	//其他成员方法省略
}

```

```java
public class Student extends Person{
	private int score;
}

```

此时子类代码报错。

解决办法：在子类构造器中，用super(实参列表)，显示调用父类的有参构造解决。

```java
public class Student extends Person{
	private int score;

	public Student(String name, int age) {
		super(name, age);
	}
	public Student(String name, int age, int score) {
		super(name, age);
		this.score = score;
	}
	
	//其他成员方法省略
}

```

结论：

子类对象实例化过程中必须先完成从父类继承的成员变量的实例初始化，这个过程是通过调用父类的实例初始化方法来完成的。

* super()：表示调用父类的无参实例初始化方法，要求父类必须有无参构造，而且可以省略不写；
* super(实参列表)：表示调用父类的有参实例初始化方法，当父类没有无参构造时，子类的构造器首行必须写super(实参列表)来明确调用父类的哪个有参构造（其实是调用该构造器对应的实例初始方法）
* super()和super(实参列表)都只能出现在子类构造器的首行

### 6.4.6 继承的特点四：单继承限制

1. Java只支持单继承，不支持多继承。

```java
//一个类只能有一个父类，不可以有多个父类。
class C extends A{} 	//ok
class C extends A，B...	//error

```

2. Java支持多层继承(继承体系)。

```java
class A{}
class B extends A{}
class C extends B{}

```

> 顶层父类是Object类。所有的类默认继承Object，作为父类。

3. 子类和父类是一种相对的概念。

   例如：B类对于A来说是子类，但是对于C类来说是父类

4. 一个父类可以同时拥有多个子类

### 6.4.7 继承练习

#### 练习1

（1）父类Graphic图形
包含属性：name（图形名），属性私有化，不提供无参构造，只提供有参构造
包含求面积getArea()：返回0.0
求周长getPerimeter()方法：返回0.0
显示信息getInfo()方法：返回图形名称、面积、周长

（2）子类Circle圆继承Graphic图形
包含属性：radius
重写求面积getArea()和求周长getPerimeter()方法，显示信息getInfo()加半径信息

（3）子类矩形Rectange继承Graphic图形
包含属性：length、width
重写求面积getArea()和求周长getPerimeter()方法

```java
public class Graphic {
	private String name;

	public Graphic(String name) {
		super();
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public double getArea() {
		return 0.0;
	}

	public double getPerimeter() {
		return 0.0;
	}

	/*
	 * this对象：调用当前方法的对象，如果是Graphic对象，那么就会执行Graphic的getArea()和getPerimeter()
	 * this对象：调用当前方法的对象，如果是Circle对象，那么就会执行Circle的getArea()和getPerimeter()
	 * this对象：调用当前方法的对象，如果是Rectangle对象，那么就会执行Rectangle的getArea()和getPerimeter()
	 */
	public String getInfo() {
		return "图形：" + name + "，面积：" + getArea() + ",周长：" + getPerimeter();
	}
}

```

```java
public class Circle extends Graphic {
	private double radius;

	public Circle(String name, double radius) {
		super(name);
		this.radius = radius;
	}

	public double getRadius() {
		return radius;
	}

	public void setRadius(double radius) {
		this.radius = radius;
	}

	@Override//表示这个方法是重写的方法
	public double getArea() {
		return Math.PI * radius * radius;
	}

	@Override//表示这个方法是重写的方法
	public double getPerimeter() {
		return Math.PI * radius * 2;
	}

	/*@Override//表示这个方法是重写的方法
	public String getInfo() {
		return super.getInfo() + "，半径：" + radius;
	}*/
	
}


```

```java
public class Rectangle extends Graphic {
	private double length;
	private double width;
	
	public Rectangle(String name, double length, double width) {
		super(name);
		this.length = length;
		this.width = width;
	}

	public double getLength() {
		return length;
	}

	public void setLength(double length) {
		this.length = length;
	}

	public double getWidth() {
		return width;
	}

	public void setWidth(double width) {
		this.width = width;
	}

	@Override
	public double getArea() {
		return length*width;
	}

	@Override
	public double getPerimeter() {
		return 2*(length + width);
	}
}


```

```java
public class TestGraphicExer3 {
	public static void main(String[] args) {
		Graphic g = new Graphic("通用图形");
		System.out.println(g.getInfo());
		
		Circle c = new Circle("圆", 1.2);
		System.out.println(c.getInfo());//调用getInfo()方法的对象是c
		
		Rectangle r = new Rectangle("矩形", 3, 5);
		System.out.println(r.getInfo());
	}
}

```

#### 练习2 

（1）声明一个银行储蓄卡类，

​	包含属性：账户，余额

​	包含取款 public void withdraw(double money)

​		    存款 pubic void save(double money)

​           获取账户信息： public String getInfo() 可以返回账户和余额

（2）声明一个银行信用卡类，继承储蓄卡类

​	增加属性：可透支额度，最多可透支金额

​	重写存款 public void withdraw(double money)，可透支

​	       存款 pubic void save(double money)，需要恢复可透支额度

（3）在测试类中，分别创建两种卡对象，测试

#### 练习3

1、声明父类：Person类
包含属性：姓名，年龄，性别
属性私有化，get/set
包含getInfo()方法：例如：姓名：张三，年龄：23，性别：男

2、声明子类：Student类，继承Person类
新增属性：score成绩
属性私有化，get/set
包含getInfo()方法：例如：姓名：张三，年龄：23，性别：男，成绩：89

3、声明子类：Teacher类，继承Person类
新增属性：salary薪资
属性私有化，get/set
包含getInfo()方法：例如：姓名：张三，年龄：23，性别：男，薪资：10000

```java
public class Person {
	private String name;
	private int age;
	private char gender;
	public Person(String name, int age, char gender) {
		super();
		this.name = name;
		this.age = age;
		this.gender = gender;
	}
	public Person() {
		super();
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public char getGender() {
		return gender;
	}
	public void setGender(char gender) {
		this.gender = gender;
	}
	
	//包含getInfo()方法：例如：姓名：张三，年龄：23，性别：男
	public String getInfo(){
		return "姓名：" + name + "，年龄：" + age +"，性别：" + gender;
	}
}

```

```java
public class Student extends Person {
	private int score;

	public Student() {
	}

	public Student(String name, int age, char gender, int score) {
		setName(name);
		setAge(age);
		setGender(gender);
		this.score = score;
	}

	public int getScore() {
		return score;
	}

	public void setScore(int score) {
		this.score = score;
	}
	//包含getInfo()方法：例如：姓名：张三，年龄：23，性别：男，成绩：89
	public String getInfo(){
		//方式一：
//		return "姓名：" + getName() + "，年龄：" + getAge() + "，成绩：" + score;
		
		//方法二：
		return super.getInfo() + "，成绩：" + score;
	}
	
}

```

```java
public class Teacher extends Person {
	private double salary;

	public Teacher() {
	}

	public Teacher(String name, int age, char gender, double salary) {
		setName(name);
		setAge(age);
		setGender(gender);
		this.salary = salary;
	}

	public double getSalary() {
		return salary;
	}

	public void setSalary(double salary) {
		this.salary = salary;
	}
	
	//包含getInfo()方法：例如：姓名：张三，年龄：23，性别：男，薪资：10000
	public String getInfo(){
		return super.getInfo() + "，薪资：" + salary;
	}
}


```

```java
public class TestPersonExer2 {
	public static void main(String[] args) {
		Person p = new Person("张三", 23, '男');
		System.out.println(p.getInfo());
		
		Student s = new Student("陈琦", 25, '男', 89);
		System.out.println(s.getInfo());
		
		Teacher t = new Teacher("柴林燕", 18, '女', 11111);
		System.out.println(t.getInfo());
	}
}

```

## 6.5 final关键字

final：最终的，不可更改的，它的用法有：

### 1、修饰类

表示这个类不能被继承，没有子类

```java
final class Eunuch{//太监类
	
}
class Son extends Eunuch{//错误
	
}

```

### 2、修饰方法

表示这个方法不能被子类重写

```java
class Father{
	public final void method(){
		System.out.println("father");
	}
}
class Son extends Father{
	public void method(){//错误
		System.out.println("son");
	}
}

```

### 3、声明常量

final修饰某个变量（成员变量或局部变量），表示它的值就不能被修改，即常量，常量名建议使用大写字母。

> 如果某个成员变量用final修饰后，没有set方法，并且必须初始化（可以显式赋值、或在初始化块赋值、实例变量还可以在构造器中赋值）

```java
public class Test{
    public static void main(String[] args){
    	final int MIN_SCORE = 0;
    	final int MAX_SCORE = 100;
    }
}
class Chinese{
	public static final String COUNTRY = "中华人民共和国";	
	private String name;
	public Chinese( String name) {
		super();
		this.name = name;
	}
	public Chinese() {
		super();
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	//final修饰的没有set方法
	public static String getCountry() {
		return COUNTRY;
	}
}

```



## 6.6 成员变量初始化

### 6.6.1 成员变量初始化方式

#### 1、成员变量有默认值

| 类别     | 具体类型                       | 默认值   |
| -------- | ------------------------------ | -------- |
| 基本类型 | 整数（byte，short，int，long） | 0        |
|          | 浮点数（float，double）        | 0.0      |
|          | 字符（char）                   | '\u0000' |
|          | 布尔（boolean）                | false    |
|          | 数据类型                       | 默认值   |
| 引用类型 | 数组，类，接口                 | null     |

我们知道类中成员变量都有默认值，但是现在我们要为成员变量赋默认值以外的值，我们该怎么办呢？

#### 2、显式赋值

```java
public class Student{
    public static final String COUNTRY = "中华人民共和国";
	private static String school = "尚硅谷";
	private String name;
	private char gender = '男';
}

```

> 显式赋值，一般都是赋常量值

#### 3、代码块

如果成员变量想要初始化的值不是一个硬编码的常量值，而是需要通过复杂的计算或读取文件、或读取运行环境信息等方式才能获取的一些值，该怎么办呢？

* 静态初始化块：为静态变量初始化


```java
【修饰符】 class 类名{
    static{
		静态初始化
	}
}


```

* 实例初始化：为实例变量初始化


```java
【修饰符】 class 类名{
    {
		实例初始化块
	}
}

```

**静态初始化块**：在类初始化时由类加载器调用执行，每一个类的静态初始化只会执行一次，早于实例对象的创建。

**实例初始化块**：每次new实例对象时自动执行，每new一个对象，执行一次。

```java
public class Student{
	private static String school;
	private String name;
	private char gender;
	
	static{
		//获取系统属性，这里只是说明school的初始化过程可能比较复杂
		school = System.getProperty("school");
		if(school==null) {
			school = "尚硅谷";
		}
	}
	{
		String info = System.getProperty("gender");
		if(info==null) {
			gender = '男';
		}else {
			gender = info.charAt(0);
		}
	}
	public static String getSchool() {
		return school;
	}
	public static void setSchool(String school) {
		Student.school = school;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public char getGender() {
		return gender;
	}
	public void setGender(char gender) {
		this.gender = gender;
	}

}

```

#### 4、构造器

我们发现，显式赋值和实例初始化块为每一个实例对象的实例变量初始化的都是相同的值，那么我们如果想要不同的实例对象初始化为不同的值，怎么办呢？此时我们可以考虑使用构造器，在new对象时由对象的创建者决定为当前对象的实例变量赋什么值。

> **注意：构造器只为实例变量初始化，不为静态类变量初始化**

为实例变量初始化，再new对象时由对象的创建者决定为当前对象的实例变量赋什么值。

#### 5、setter方法

一般用于修改成员变量的值。



### 6.6.2 类初始化

1、类初始化的目的：为类中的静态变量进行赋值。

2、实际上，类初始化的过程时在调用一个<clinit>()方法，而这个方法是编译器自动生成的。编译器会将如下两部分的**所有**代码，**按顺序**合并到类初始化<clinit>()方法体中。

（1）静态类成员变量的显式赋值语句

（2）静态代码块中的语句

3、整个类初始化只会进行一次，如果子类初始化时，发现父类没有初始化，那么会先初始化父类。

#### 示例代码1：单个类

```java
public class Test{
    public static void main(String[] args){
    	Father.test();
    }
}
class Father{
	private static int a = getNumber();//这里调用方法为a变量显式赋值的目的是为了看到这个过程
	static{
		System.out.println("Father(1)");
	}
	private static int b = getNumber();
	static{
		System.out.println("Father(2)");
	}
	
	public static int getNumber(){
		System.out.println("getNumber()");
		return 1;
	}
	
	public static void test(){
		System.out.println("Father:test()");
	}
}

```

```java
运行结果：
getNumber()
Father(1)
getNumber()
Father(2)
Father:test()

```

![1562070829002](https://raw.githubusercontent.com/zxingq/Picture/main/202211192023342.png)

#### 示例代码2：父子类

```java
public class Test{
    public static void main(String[] args){
    	Son.test();
        System.out.println("-----------------------------");
        Son.test();
    }
}
class Father{
	private static int a = getNumber();
	static{
		System.out.println("Father(1)");
	}
	private static int b = getNumber();
	static{
		System.out.println("Father(2)");
	}
	
	public static int getNumber(){
		System.out.println("Father:getNumber()");
		return 1;
	}
}
class Son extends Father{
	private static int a = getNumber();
	static{
		System.out.println("Son(1)");
	}
	private static int b = getNumber();
	static{
		System.out.println("Son(2)");
	}
	
	public static int getNumber(){
		System.out.println("Son:getNumber()");
		return 1;
	}
	
	public static void test(){
		System.out.println("Son:test()");
	}	
}

```

```java
运行结果：
Father:getNumber()
Father(1)
Father:getNumber()
Father(2)
Son:getNumber()
Son(1)
Son:getNumber()
Son(2)
Son:test()
-----------------------------
Son:test()

```

结论：

每一个类都有一个类初始化方法<clinit>()方法，然后子类初始化时，如果发现父类加载和没有初始化，会先加载和初始化父类，然后再加载和初始化子类。一个类，只会初始化一次。



### 6.6.3 实例初始化

1、实例初始化的目的：为类中非静态成员变量赋值

2、实际上我们编写的代码在编译时，会自动处理代码，整理出一个<clinit>()的类初始化方法，还会整理出一个或多个的<init>(...)实例初始化方法。一个类有几个实例初始化方法，由这个类就有几个构造器决定。

**实例初始化方法的方法体，由四部分构成**：

（1）super()或super(实参列表)    这里选择哪个，看原来构造器首行是哪句，没写，默认就是super()

（2）非静态实例变量的显示赋值语句

（3）非静态代码块

（4）对应构造器中的代码

特别说明：其中（2）和（3）是按顺序合并的，（1）一定在最前面（4）一定在最后面

3、执行特点：

* 创建对象时，才会执行，
* 调用哪个构造器，就是指定它对应的实例初始化方法
* 创建子类对象时，父类对应的实例初始化会被先执行，执行父类哪个实例初始化方法，看用super()还是super(实参列表)

#### 示例代码1：单个类

```java
public class Test{
    public static void main(String[] args){
    	Father f1 = new Father();
    	Father f2 = new Father("atguigu");
    }
}
class Father{
	private int a = getNumber();
	private String info;
	{
		System.out.println("Father(1)");
	}
	Father(){
		System.out.println("Father()无参构造");
	}
	Father(String info){
		this.info = info;
		System.out.println("Father(info)有参构造");
	}
	private int b = getNumber();
	{
		System.out.println("Father(2)");
	}
	
	public int getNumber(){
		System.out.println("Father:getNumber()");
		return 1;
	}
}

```

```java
运行结果：
Father:getNumber()
Father(1)
Father:getNumber()
Father(2)
Father()无参构造
Father:getNumber()
Father(1)
Father:getNumber()
Father(2)
Father(info)有参构造

```

![1562072678317](https://raw.githubusercontent.com/zxingq/Picture/main/202211192025303.png)

#### 示例代码2：父子类

```java
public class Test{
    public static void main(String[] args){
    	Son s1 = new Son();
        System.out.println("-----------------------------");
    	Son s2 = new Son("atguigu");
    }
}
class Father{
	private int a = getNumber();
	private String info;
	{
		System.out.println("Father(1)");
	}
	Father(){
		System.out.println("Father()无参构造");
	}
	Father(String info){
		this.info = info;
		System.out.println("Father(info)有参构造");
	}
	private int b = getNumber();
	{
		System.out.println("Father(2)");
	}
	
	public static int getNumber(){
		System.out.println("Father:getNumber()");
		return 1;
	}
}
class Son extends Father{
	private int a = getNumber();
	{
		System.out.println("Son(1)");
	}
	private int b = getNumber();
	{
		System.out.println("Son(2)");
	}
	public Son(){
		System.out.println("Son()：无参构造");
	}
	public Son(String info){
		super(info);
		System.out.println("Son(info)：有参构造");
	}
	public static int getNumber(){
		System.out.println("Son:getNumber()");
		return 1;
	}
}

```

```java
运行结果：
Father:getNumber()
Father(1)
Father:getNumber()
Father(2)
Father()无参构造
Son:getNumber()
Son(1)
Son:getNumber()
Son(2)
Son()：无参构造
-----------------------------
Father:getNumber()
Father(1)
Father:getNumber()
Father(2)
Father(info)有参构造
Son:getNumber()
Son(1)
Son:getNumber()
Son(2)
Son(info)：有参构造

```

#### 示例代码3：父子类，方法有重写

```java
public class Test{
    public static void main(String[] args){
    	Son s1 = new Son();
    	System.out.println("-----------------------------");
    	Son s2 = new Son("atguigu");
    }
}
class Father{
	private int a = getNumber();
	private String info;
	{
		System.out.println("Father(1)");
	}
	Father(){
		System.out.println("Father()无参构造");
	}
	Father(String info){
		this.info = info;
		System.out.println("Father(info)有参构造");
	}
	private int b = getNumber();
	{
		System.out.println("Father(2)");
	}
	
	public int getNumber(){
		System.out.println("Father:getNumber()");
		return 1;
	}
}
class Son extends Father{
	private int a = getNumber();
	{
		System.out.println("Son(1)");
	}
	private int b = getNumber();
	{
		System.out.println("Son(2)");
	}
	public Son(){
		System.out.println("Son()：无参构造");
	}
	public Son(String info){
		super(info);
		System.out.println("Son(info)：有参构造");
	}
	public int getNumber(){
		System.out.println("Son:getNumber()");
		return 1;
	}
}

```

```java
运行结果：
Son:getNumber()  //子类重写getNumber()方法，那么创建子类的对象，就是调用子类的getNumber()方法，因为当前对象this是子类的对象。
Father(1)
Son:getNumber()
Father(2)
Father()无参构造
Son:getNumber()
Son(1)
Son:getNumber()
Son(2)
Son()：无参构造
-----------------------------
Son:getNumber()
Father(1)
Son:getNumber()
Father(2)
Father(info)有参构造
Son:getNumber()
Son(1)
Son:getNumber()
Son(2)
Son(info)：有参构造

```

### 6.6.4 类初始化与实例初始化

类初始化肯定优先于实例初始化。

类初始化只做一次。

实例初始化是每次创建对象都要进行。

```java
public class Test{
    public static void main(String[] args){
    	Son s1 = new Son();
    	System.out.println("----------------------------");
    	Son s2 = new Son();
    }
}
class Father{
	static{
		System.out.println("Father:static");
	}
	{
		System.out.println("Father:not_static");
	}
	Father(){
		System.out.println("Father()无参构造");
	}
}
class Son extends Father{
	static{
		System.out.println("Son:static");
	}
	{
		System.out.println("Son:not_static");
	}
	Son(){
		System.out.println("Son()无参构造");
	}
}

```

```java
运行结果：
Father:static
Son:static
Father:not_static
Father()无参构造
Son:not_static
Son()无参构造
----------------------------
Father:not_static
Father()无参构造
Son:not_static
Son()无参构造

```









## 6.7 this和super关键字

### 6.7.1 this关键字

#### 1、this的含义

this代表当前对象

#### 2、this使用位置

* this在实例初始化相关的代码块和构造器中：表示正在创建的那个实例对象，即正在new谁，this就代表谁
* this在非静态实例方法中：表示调用该方法的对象，即谁在调用，this就代表谁。
* this不能出现在静态代码块和静态方法中

#### 3、this使用格式

（1）this.成员变量名

* 当方法的局部变量与当前对象的成员变量重名时，就可以在成员变量前面加this.，如果没有重名问题，就可以省略this.
* this.成员变量会先从本类声明的成员变量列表中查找，如果未找到，会去从父类继承的在子类中仍然可见的成员变量列表中查找

（2）this.成员方法

* 调用当前对象的成员方法时，都可以加"this."，也可以省略，实际开发中都省略
* 当前对象的成员方法，先从本类声明的成员方法列表中查找，如果未找到，会去从父类继承的在子类中仍然可见的成员方法列表中查找

（3）this()或this(实参列表)

* 只能调用本类的其他构造器


* 必须在构造器的首行


* 如果一个类中声明了n个构造器，则最多有 n - 1个构造器中使用了"this(【实参列表】)"，否则会发生递归调用死循环


### 6.7.2  super关键字

#### 1、super的含义

super代表当前对象中从父类的引用的

#### 2、super使用的前提

* 通过super引用父类的xx，都是在子类中仍然可见的
* 不能在静态代码块和静态方法中使用super

#### 3、super的使用格式

（1）super.成员变量

在子类中访问父类的成员变量，特别是当子类的成员变量与父类的成员变量重名时。

```java
public class Person {
	private String name;
	private int age;
	//其他代码省略
}
public class Student extends Person{
	private int score;
	//其他成员方法省略
}
public class Test{
    public static void main(String[] args){
    	Student stu = new Student();
    }
}

```

![1561984785190](https://raw.githubusercontent.com/zxingq/Picture/main/202211192045591.png)

```java
public class Test{
    public static void main(String[] args){
    	Son s = new Son();
    	s.test(30);
    }
}
class Father{
	int a = 10;
}
class Son extends Father{
	int a = 20;
	public void test(int a){
		System.out.println(super.a);//10
		System.out.println(this.a);//20
		System.out.println(a);//30
	}
}

```

（2）super.成员方法

在子类中调用父类的成员方法，特别是当子类重写了父类的成员方法时

```java
public class Test{
    public static void main(String[] args){
    	Son s = new Son();
    	s.test();
    }
}
class Father{
	public void method(){
		System.out.println("aa");
	}
}
class Son extends Father{
	public void method(){
		System.out.println("bb");
	}
	public void test(){
		method();//bb
		this.method();//bb
		super.method();//aa
	}
}

```

（3）super()或super(实参列表)

在子类的构造器首行，用于表示调用父类的哪个实例初始化方法

> super() 和 this() 都必须是在构造方法的第一行，所以不能同时出现。

### 6.7.3  就近原则和追根溯源原则

#### 1、找变量

* **没有super和this**
  * 在构造器、代码块、方法中如果出现使用某个变量，先查看是否是当前块声明的局部变量，
  * 如果不是局部变量，先从当前执行代码的本类去找成员变量
  * 如果从当前执行代码的本类中没有找到，会往上找父类的（非private，跨包还不能是缺省的）

* **this** ：代表当前对象
  * 通过this找成员变量时，先从当前执行代码的本类中找，没有的会往上找父类的（非private，跨包还不能是缺省的）。

* **super** ：代表父类的
  * 通过super找成员变量，直接从当前执行代码所在类的父类找
  * super()或super(实参列表)只能从直接父类找
  * 通过super只能访问父类在子类中可见的（非private，跨包还不能是缺省的）


> 注意：super和this都不能出现在静态方法和静态代码块中，因为super和this都是存在与**对象**中的

#### 2、找方法

* 没有super和this
  * 先从当前对象（调用方法的对象）的本类找，如果没有，再从直接父类找，再没有，继续往上追溯

* this
  * 先从当前对象（调用方法的对象）的本类找，如果没有，再从父类继承的可见的方法列表中查找

* super
  * 直接从当前对象（调用方法的对象）的父类继承的可见的方法列表中查找

#### 3、找构造器

* this()或this(实参列表)：只从本类中，不会再往上追溯
* super()或super(实参列表)：只从直接父类找，不会再往上追溯

#### 4、练习

##### （1）情形1

```java
class Father{
	int a = 10;
	int b = 11;
}
class Son extends Father{
	int a = 20;
	
	public void test(){
		//子类与父类的属性同名，子类对象中就有两个a
		System.out.println("父类的a：" + super.a);//10    直接从父类局部变量找
		System.out.println("子类的a：" + this.a);//20   先从本类成员变量找
		System.out.println("子类的a：" + a);//20  先找局部变量找，没有再从本类成员变量找
		
		//子类与父类的属性不同名，是同一个b
		System.out.println("b = " + b);//11  先找局部变量找，没有再从本类成员变量找，没有再从父类找
		System.out.println("b = " + this.b);//11   先从本类成员变量找，没有再从父类找
		System.out.println("b = " + super.b);//11  直接从父类局部变量找
	}
	
	public void method(int a){
		//子类与父类的属性同名，子类对象中就有两个成员变量a，此时方法中还有一个局部变量a
		System.out.println("父类的a：" + super.a);//10  直接从父类局部变量找
		System.out.println("子类的a：" + this.a);//20  先从本类成员变量找
		System.out.println("局部变量的a：" + a);//30  先找局部变量
	}
    
    public void fun(int b){
        System.out.println("b = " + b);//13  先找局部变量
		System.out.println("b = " + this.b);//11  先从本类成员变量找
		System.out.println("b = " + super.b);//11  直接从父类局部变量找
    }
}
public class TestInherite2 {
	public static void main(String[] args) {
		Son son = new Son();
		System.out.println(son.a);//20
		System.out.println(son.b);//11
		
		son.test();
		
		son.method(30);
        
        son.fun(13);
	}
}

```

##### （2）情形2

```java
public class Test{
    public static void main(String[] args){
    	Son s = new Son();
    	System.out.println(s.getNum());//10   没重写，先找本类，没有，找父类
    	
    	Daughter d = new Daughter();
    	System.out.println(d.getNum());//20  重写了，先找本类
    }
}
class Father{
	protected int num = 10;
	public int getNum(){
		return num;
	}
}
class Son extends Father{
	private int num = 20;
}
class Daughter extends Father{
	private int num = 20;
	public int getNum(){
		return num;
	}
}

```

##### （3）情形3

```java
public class Test{
    public static void main(String[] args){
    	Son s = new Son();
    	s.test();
    	
    	Daughter d = new Daughter();
    	d.test();
    }
}
class Father{
	protected int num = 10;
	public int getNum(){
		return num;
	}
}
class Son extends Father{
	private int num = 20;
	public void test(){
		System.out.println(getNum());//10  本类没有找父类
		System.out.println(this.getNum());//10  本类没有找父类
		System.out.println(super.getNum());//10  本类没有找父类
	}
}
class Daughter extends Father{
	private int num = 20;
	public int getNum(){
		return num;
	}
	public void test(){
		System.out.println(getNum());//20  先找本类
		System.out.println(this.getNum());//20  先找本类
		System.out.println(super.getNum());//10  直接找父类
	}
}

```

# 