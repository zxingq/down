---
title: ' python'
author: Xingqi
date: '2022-10-18'
slug: python
categories: []
tags: []
---
# 

# python进阶

### 面向对象编程(oop)

面向过程：

1.把完成某一个需求的所有步骤从头到尾逐步实现

2.根据开发需求，将一些独立功能的代码，封装成一个又一个函数

3.最后完成的代码，就是顺序的调用不同的函数

**特点**

1.注重步骤与过程，不注重职责与分工

2.如果需求复杂，代码会变得很复杂

3.开发复杂项目，没有固定的套路，开发难度大!

**面向对象**

面向对象本身就是对面向过程的封装

侧重谁来做事情

如何从面向过程编程思想过渡到面向对象编程？-------->根据这个对对象以及对应的行为,抽象出对应的类.

**类和对象使面向对象编程的两个核心概念**



#### **类**

类是一类具有相同特征的，是抽象的，负责定义对象

类与对象的关系：

类是模板，对象根据对象这个模板创建出来的，应该先有类，再有对象

类只有一个，而对象可以有多个。

类到对象是一个实例化的过程



属性和变量的区别以及判断依据

- 变量是可以改变的量值
- 属性是属于某个对象的特征

访问权限

- 根据不同的位置存在不同的访问权限
- 属性:只能通过对象来进行访问

**类的作用**:

根据抽象的类,生产出具体的对象.

例举生活中的类:钱

对象:具体的1毛,5毛,100元

类的三要素：类名，属性，方法

对象的特征描述，通常定义为属性，对象具有的动作，通常定义为方法

**实例方法**

- 类体中定义实例方法 

  - ​	 Python要求实例方法的第一个形参必须为self，也就是实例对象本身，因此实例方法至少应该有一个self参数。 

- 在类体外将一个函数直接赋值给一个对象实例 

  - 这种动态定义实例方法，本质上就是动态增加实例变量，只是这个实例变量比较特殊，是个函数类型，对应的赋值也是一个函数。因此上述方法定义的实例方法，与类体中定义的方法还是有差别的，对这种方法Python 不会将实例对象自动绑定到方法的第一个参数，即使将第一个参数命名为 self 也没有用。

  - ```Python
    class Kls(object):
        def __init__(self, data):
            self.data = data
    
        def printd(self):
            print(self.data)
    
    
    ik1 = Kls('leo')
    ik2 = Kls('lee')
    
    ik1.printd()
    ik2.printd()
    结果：
    leo
    lee
    ```

**类方法**

- Python 的类方法采用装饰器`@classmethod`来定义 

- ```python
  class Kls(object):
      num_inst = 0
  
      def __init__(self):
          Kls.num_inst = Kls.num_inst + 1
  
      @classmethod
      def get_no_of_instance(cls):
          return cls.num_inst
  
  
  ik1 = Kls()
  ik2 = Kls()
  
  print ik1.get_no_of_instance()
  print Kls.get_no_of_instance()
  结果：
  2
  2
  ```

   由于在调用类方法时，只需要将类型本身传递给类方法，因此，既可以通过类也可以通过实例来调用类方法。 

**静态方法**

 既可以通过类调用，也可以通过示例调用 

```python
class Person:
    @staticmethod #装饰器的作用：在保证原函数不变的情况下，直接给这个函数增加一些功能
    def jingtai(cls):
        print("这是一个类方法")
        
Person.jingtai()

p = Person()
p.jingtai()

func = Person.jingtai
func()

```

**元类**：

创建类对象的类(type)， 元类就是用来创建这些类（对象）的，元类就是类的类

```python
>>> age = 35
>>> age . __class__
< type 'int' >
>>> name = 'bob'
>>> name . __class__
< type 'str' >
>>> def foo( ) : pass
>>> foo . __class__
< type 'function' >
>>> class Bar( object ) : pass
>>> b = Bar ( )
>>> b . __class__
< class '__main__.Bar' >


>>> a . __class__. __class__
< type 'type' >
>>> age . __class__. __class__
< type 'type' >
>>> foo . __class__. __class__
< type 'type' >
>>> b . __class__. __class__
< type 'type' >
```

 元类就是创建类这种对象的东西。如果你喜欢的话，可以把元类称为“类工厂”（不要和工厂类搞混了）。type就是Python的内建元类，当然了，你也可以创建自己的元类。 

公有化属性：

![1659752993081](https://github.com/zxingq/down/raw/main/img/1659752993081.png)


私有化属性

_x：受保护属性

- 在类与子类内部可以访问，在模块外访问受警告，跨模块访问报错

- ```python
  class Animal:
      _x = 10
      def test(self):
          print(Animal._x)
          print(self._x)
       pass
  #--------------------
  class Dog(Animal):
      def test2(self):
          print(Dog._x)
          print(self._x)
       pass
  
  a = Animal()
  a.test()		#类的内部访问
  
  d = Dog()
  d.test2()		#延伸类的访问
  
  print(Animal._x)		#模块的其他部分,可以强行访问，有警告
  print(Dog._x)
  print(a._x)
  print(b._x)
  
  import xxx              #可以访问
  print(xxx.a)
  from xxx import *        #这种跨模块访问，不能访问
  print(a)
  
  ```

私有化属性：（双下划线），只能在类的内部访问

- 数据保护
- 数据过滤

```python
class Person:
    #作用：当我们创建好一个实例对对象之后，会自动调用这个方法，来初始化这对象
    #init是单词初始化initialization的省略形式
    def __init__(self)
    	self.__age = 18
    def setAge(self,value):
        #过滤处理
        #判定前面一个对象是否是后面的类型
        if isinstance(value,int) and 0<value<200:
        	self.__age = value
        else:
            print("您输入的数据有误，请重新输入")
    def getAge(self):
        return self.__age
    
        
p1 = Person()
p1.setAge(20)
p2 = Person()
print(p1.getAge())   #访问age

print(p1.__age)      #报错，只能在类内部访问
print(p2.__age)

```

1. **经典类：没有继承object**
2. **新式类：继承object**

- property在新式类种的使用

- ```python
  class Person(object):
     def __init__(self):
         self.__age = 18
            @property
            def age(self):
                return self.__age
            @age.setter
            def age(self, value):
                delf.__age = value
   
     p = Person()
     p.age = 20    #既可以读取也可以设置
   
  ```

 在经典类中，property只会关联读取方法，不会关联设置和删除方法。 

##### 内置特殊方法

-  通过定义`__str__`，就可以通过`print(<对象>)`来查看指定的返回值 

```python
class Person:
    def __init__(self,n,a):
        self.name = n
        self.age = a
    def __str__(self):
        return "这个人的姓名是%s，这个人的年龄是%s"%(self.name, self.age)
p1 = Person("zpc",18) #可创建不同的对象

s=str(p1)
print(s)

```

-  `__repr__`面向的对象是开发人员（解释器）；`__str__`面向的对象是用户。 

1. 触发`__repr__`的方法：
   1. `s=repr(p1) print(s)`
   2. 在交互模式里面将对象名称写出，敲回车

- `__call__`的作用：使得对象具有当作函数来调用的能力(将对象变为可调用对象) 

  - ```python
    class PenFactory:
        def __init__(self, p_type):
            self.p_type = p_type       #这个类只有一个属性
        def __call__(self, p_color):
            print("创建了一个%s类型的画笔，他是%s颜色的"%(self.p_type, p_color))
    gangbiF = penFactory("钢笔")       #创建一个对象
    gangbiF('红色')
    
    ```

    

- 面向对象的切片操作

```Python
class Person1:
    def __init__(self):
        self.items = [1, 2, 3, 4, 5, 6, 7, 8]  # 定义了一个items属性

    def __setitem__(self, key, value):
        if isinstance(key,slice):
            self.items[key] = value  # 注意切片操作只能修改，不能新增
        # self.items.[key.start: key.stop: key.step] = value  #这样赋值也可以

    def __getitem__(self, key):
        return (key.items[key])  # 这里可能有错

    def __delitem__(self, key):
        del self[key]
p = Person1()
p[0: 4: 2] = ["a", "b"]
print(p.items)
结果：
['a', 2, 'b', 4, 5, 6, 7, 8]
```

比较操作

![1659792902954](https://github.com/zxingq/down/raw/main/img/1659792902954.png)

```python
import functools
@functools.total_ordering      #此装饰器会自动补全所需要的方法
class Person2:
    def __lt__(self, other):
        print('lt')
        return True
    def __eq__(self, other):
        print('eq')
a=Person2()
b=Person2()
print(a>b)
print(Person2.__dict__)
结果：
lt
False
{'__module__': '__main__', '__lt__': <function Person2.__lt__ at 0x000001CE01944670>, '__eq__': <function Person2.__eq__ at 0x000001CE01944700>, '__dict__': <attribute '__dict__' of 'Person2' objects>, '__weakref__': <attribute '__weakref__' of 'Person2' objects>, '__doc__': None, '__hash__': None, '__gt__': <function _gt_from_lt at 0x000001CE017A2D30>, '__le__': <function _le_from_lt at 0x000001CE017A2DC0>, '__ge__': <function _ge_from_lt at 0x000001CE017A2E50>}

```

##### **描述器**

1. 概念和作用：描述器是一个对象，可以描述一个属性的操作；其作用是对属性的操作做验证和过滤，如对一个人的年龄赋值时，不能赋值为负数，这是需要验证和过滤，但由于属性数量多，不能在赋值前进行验证，所以用到描述器，每次验证时就会进入描述器中进行相关操作

2. 多个属性时，由于操作内容不同，在主类中代码会过于繁琐，为简化代码，将属性的操作方法封装到类中，在主类中对方法类的实例对象进行操作即可 

3. ```python
   class Age:        #描述器类
       def __get__(self, instance, owner):
           print("get")
       def __set__(self, instance, value):
           print("set")
       def __delete__(self, instance):
           print("delete")
           
   class Person:     #主类
       age = Age()   
       
   p = Person()
   p.age = 10
   
   ```

##### 生命周期

指的是一个对象，从诞生到消亡的过程，当一个对象被创建时，会在内存中分配相应的内存空间进行存储，当这个对象不再使用，为了节约内存，就会将这个对象释放

- **监听对象生命周期**

  - `__new__`方法

  - `__init__`方法

  - `__del__`方法

  - ```Python
    #coding:gbk
    class Person:
        #将计数设置位私有属性，不能被在类的外部进行改变
        __PersonCount=0
        def __init__(self):
            print("人的个数+1")
            #采用类方法将数量进行改变
            self.__class__.__PersonCount += 1
        def __del__(self):
            print('人的数量-1')
            self.__class__.__PersonCount-=1
    
        @classmethod
        def log(cls):
            print("当前人的数量为%d位" %cls.__PersonCount)
    
    p1=Person()
    p2=Person()
    del p1
    Person.log()
    结果：
    人的个数+1
    人的个数+1
    人的数量-1
    当前人的数量为1位
    人的数量-1
    ```

    

##### 内存管理机制

- 存储方面

  - 在python种万物皆对象
  - 所有对象都会在内存中开辟一块空间存储
  - 对于整数和短小的字符，python会进行缓存；不会创建多个相同对象
  - 容器对象，存储的其他对象，仅仅是其他对象的引用，并不是其他对象本身

- **垃圾回收方面**

- 和许多其它的高级语言一样，Python使用了垃圾回收器来自动销毁那些不再使用的对象。每个对象都有一个引用计数，当这个引用计数为0时Python能够安全地销毁这个对象。

- **弱引用** 

- 在对象群组内部使用弱引用（即不会在引用计数中被计数的引用）有时能避免出现引用环，因此弱引用可用于解决循环引用的问题。 

- ```python 
  >>> import sys#sys模块是与python解释器交互的一个接口
  >>> import weakref
  >>> class Man():
  ...     def __init__(self, name):
  ...             self.name = name
  ...
  >>> man0 = Man('zhe')    # 增加一个引用  count = 1 
  >>> sys.getrefcount(man0)
  2
  >>> r = weakref.ref(man0)   # 增加一个弱引用  count = 1  
  >>> sys.getrefcount(man0)
  2
  >>> r   # 获取弱引用所指向的对象
  <weakref at 0x0000026AF3974688; to 'Man' at 0x0000026AF398C710>
  >>> man1 = r()
  >>> man0 is man1
  True
  >>> sys.getrefcount(man0)
  3
  >>> man0 = None
  >>> man1 = None
  >>> r   # 当对象引用计数为零时，弱引用失效。
  <weakref at 0x0000026AF3974688; dead>
  
  ```

  

  - 立即回收使用的主要算法就是引用计数

  - 正是因为有引用，对象才会在内存中存在。当对象的引用数量归零后，垃圾回收程序会把对象销毁。

  - 引用计数器

    - 一个对象会记录自身被引用的个数

    - ```python
      class Person:
          pass
      p1 = Person()  #计数器+1
      print(sys.getrefcount(p1))  #这里输出的是2
      p2 = p1     #计数器+1 这个过程将p2指向Person()的内存
      
      del p2      #计数器-1
      del p1      #计数器-1
      
      ```

      

  - 垃圾回收

  - 特殊场景

  ##### 案例：利用面向对象的知识结合装饰器和私有属性等相关内容进行计算器的加减乘运算，并进行语音播报

  ```python
  #coding:gbk
  
  import win32com.client
  class Caculator:
      def __creat_say_zsq(word=""):
          def __say_zsq(func):
              def inner(self, n):
                  self.__say(word + str(n))
                  return func(self, n)
              return inner
          return __say_zsq
      def __say(self, word):
          # 1.创建了一个播报对象
          speaker = win32com.client.Dispatch("SAPI.SpVoice")
          # 2.通过这个播报对象直接播报相应的语音字符串就可
          speaker.Speak(word)
  # 下面分析一下这个函数，最外层creat_say_zsq是一个函数，他创建了一个装饰器，传入参数，并将装饰器返回！
      def __check_num_zsq(func):
          def inner(self, n):  # 这个函数的返回值要跟被修饰函数的返回值相同
              if not isinstance(n, int):
                  raise TypeError("当前这个数据的类型有问题，应该是一个整形数据")
              return func(self, n)  # 因为这个func有返回值，所以是return(func(self, n))
          return inner
      @__check_num_zsq  # 先验证再播放
      @__creat_say_zsq()
      def __init__(self, num):
          self.__result = num
      @__check_num_zsq
      @__creat_say_zsq("加上")
      def jia(self, n):
          self.__result += n
          return self
      @__check_num_zsq
      @__creat_say_zsq("减去")
      def jian(self, n):
  
          self.__result -= n
          return self
      @__check_num_zsq
      @__creat_say_zsq("乘以")
      def cheng(self, n):
          self.__result *= n
          return self
      def clear(self):
          self.__result = 0
          self.__say("将计算结果进行清零之后")
          return self
  
      def show(self):
          self.__say("计算机的结果是：%d" % self.__result)
          print("计算机的结果是：%d" % self.__result)
          return self
  c1 = Caculator(2)
  c1.jia(6).jian(4).cheng(5).show().clear().jia(2).cheng(13).show()
  
  
  结果:
  计算机的结果是：20
  计算机的结果是：26
  ```

  object与type的区别

  ![]("https://github.com/zxingq/down/raw/main/img/1660114580420.png")

- type创建了object和int，Dog等不同的类。type和Dog等类又继承object

抽象与现实名词解释**

 **抽象指对现实世界问题和实体的本质表现、行为和特征建模** 

- 抽象不仅定义了这种模型的数据属性，还定义了这些模型的接口，对某种抽象的实现就是对此数据与相关接口的现实化。

**封装/接口**

- 封装描述了对数据/信息进行隐藏的观念，它对数据属性提供接口和访问函数。通过任何客户端直接对数据的访问，无视接口与封装性都是背道而驰的，除非程序员允许这些操作。作为实现的一部分，客户端根本就不需要知道在封装之后，数据属性是如何组织的。在 Python中，所有的类属性都是公开的，但名字可能被“混淆”了，以阻止未经授权的访问，但仅此而已，再没有其他预防措施了。这就需要在设计时，对数据提供相应的接口，以免客户程序通过不规范的操作来存取封装的数据属性。

**派生/继承/继承结构**

> **派生**描述了子类的创建，新类保留已存类类型中所有需要的数据和行为，但允许修改或者其他的自定义操作，都不会修改原类的定义。
>
> **继承**描述了子类属性从祖先类继承这样一种方式。从前面的例子中，技工可能比顾客多个汽车技能属性，但单独的来看，每个都“是一个”人。继承结构表示多“代”派生，可以描述成一个“族谱”，连续的子类，与祖先类都有关系。 
>
> 泛化表示所有子类与其父类及祖先类**有一样的特点**，所以子类可以认为同祖先类是“是一个”(is-a)的关系，因为一个派生对象(实例)是祖先类的一个“例子”。比如，技工“是一个”人，车“是一个”交通工具等。 
>
> 多态的概念指出了对象如何通过他们共同的属性和动作来操作及访问，而不需考虑他们具体的类多态表明了动态(后来又称运行时)绑定的存在，允计重载及运行时类型确定和验证。 

**类和对象使面向对象编程的两个核心概念**



**类**

类是一类具有相同特征的，是抽象的，负责定义对象

类与对象的关系：

类是模板，对象根据对象这个模板创建出来的，应该先有类，再有对象

类只有一个，而对象可以有多个。

类的三要素：类名，属性，方法

对象的特征描述，通常定义为属性，对象具有的动作，通常定义为方法

**类的初始化方法**

当使用类名()创建对象时，会自动：

1.为对象再内存中分配空间-----创建对象

2.为对象的属性设置初始值-----初始化方法（init）

这个初始化方法就是__init__方法，是内置方法

内置方法和属性

![image-20220309205321753](https://github.com/zxingq/down/raw/main/img/image-20220309205321753.png)



```python
class Cat():
    def __init__(self,new_name):
        self.name=new_name
        print("我是小猫%s,我来了"%self.name)
    #__del__内置函数在其他方法执行完之后才执行
    def __del__(self):
        print("我是小猫%s,我去了"%self.name)
    #当print(对象)时，要返回的不是class类与地址时，str可以返回字符串
    def __str__(self):
        return "我是小猫[%s]"%self.name
tom=Cat("Tom")
print(tom)


结果
D:\python进阶学习\venv\Scripts\python.exe D:/python进阶学习/面向对象/内置方法.py
我是小猫Tom,我来了
我是小猫[Tom]
我是小猫Tom,我去了
```

**封装**

1.将属性和方法封装在一个类中

2.外界使用类创建对象，然后让对象调用方法

3.对象方法的细节都被封装在类的内部

- 好处：

  - 使用起来更加的方便
    - 类似于向外界提供一个工具箱
  - 保证数据更加安全
    - 可以控制数据为只读
    - 可以拦截数据的写操作

  - 利于代码的维护
    - 

一个对象的属性可以是另一个方法

在定义属性时，如果不知道设置什么初始值，可以设置为none

none关键字表示什么都没有

None表示一个空对象，没有方法与属性，是一个特殊的常量

可以将none赋值给任何一个变量



身份运算符

身份运算符用于比较两个对象是否相同

![image-20220310203529172](https://github.com/zxingq/down/raw/main/img/image-20220310203529172.png)

is 与==的区别

is用于判断两个变量引用对象是否为同一个

==用于判断引用变量的值是否相等



**私有属性和私有方法**

在实际开发中，对象的某些属性或方法可能只希望在对象的内部被使用，而不希望在外部被访问到

在定义私有属性或方法时，在方法或属性名前面增加两个下划线



**继承**

在python中继承指资源的使用权

父类（超类，基类）

子类（派生类）

继承实现代码的引用，相同的代码即不需要重写

继承：子类拥有父类的所有方法和属性

继承的传递性：子类拥有父类与父类的父类的属性 

重写：在子类中定义一个跟父类相同的方法



多继承：可以让子类对象同时拥有多个父类的对象

注意：在编写方法时，如果父类之间有相同的方法，应该尽量避免方法名相同

print(C.__mro__)用于多继承判断方法执行路径，次序

**多态**

多态不同的子类对象，调用相同的父类方法，产生不同的执行结果

- 多态可以增加代码的灵活性

- 以继承和重写父类方法为前提

- 是调用方法的技巧，不会影响到类的内部使用



```python
class Dog(object):
    def __init__(self,name):
        self.name=name
    def game(self):
        print("%s快快乐乐的玩耍"%self.name)

class Xioatianquan(Dog):
    def game(self):
        print("%s在天上快快乐乐的玩耍"%self.name)

class Person(object):
    def __init__(self,name):
        self.name=name

    def person_and_dog_game(self,dog):
        print("%s和他的宠物[%s]愉快的玩耍"
              %(self.name,dog.name))
        #调用狗玩耍的方法
        dog.game()

#创建应该狗的对象
wangcai=Dog("旺财")
#创建应该狗的子类，哮天犬狗对象
xiaotianquan=Xioatianquan("哮天犬")
#创建应该人对象
xiaoming=Person("小明")
#调用方法即狗与人玩耍的方法
xiaoming.person_and_dog_game(wangcai)
xiaoming.person_and_dog_game(xiaotianquan)

结果
D:\python进阶学习\venv\Scripts\python.exe D:/python进阶学习/面向对象/多态.py
小明和他的宠物[旺财]愉快的玩耍
旺财快快乐乐的玩耍
小明和他的宠物[哮天犬]愉快的玩耍
哮天犬在天上快快乐乐的玩耍
```

类方法：方法内部只需要访问实例属性

**静态方法**

- 在开发时，如果需要在类中封装一个方法，这个方法：

  - 既不需要访问实例属性或者调用实例方法

  - 也不需要访问类属性或者调用类方法

  在这个时候，可以把这个方法封装成一个静态方法

  

**单例**

1.单例设计模式

- 设计模式

  - 设计模式是前人工作的总结和提炼，通常，被人们广泛流传的设计模式都是针对**某一特定问题**的成熟解决方案

  - 使用设计模式是为了可重用代码，让代码更容易让他人理解，保证代码可靠性

- 单例设计模式
  - 目的：让类创建的对象在系统中只有唯一的一个实例
  - 每一次执行类名()返回的对象，内存地址是相同的

2.__new__方法

- __new__是一个由object基类提供的内置的静态方法，其作用有两个：
  - 在内存中为对象分配空间
  - 返回对象的引用

```python
class Player(object):
    def __new__(cls, *args, **kwargs):
        #new方法的作用，就是在内存中为对象分配空间
        #返回对象的引用
        print("创建对象，分配内存")
        instanc=super().__new__(cls)
        #返回对象的引用
        return instanc
    def __init__(self):
        print("将对象进行初始化")
#创建对象
player=Player()
#打印对象所在的内存地址
print(player)

结果：
创建对象，分配内存
将对象进行初始化
<__main__.Player object at 0x000001EC2FB3D7F0>
```

```python
class Player(object):
    instance = None
    def __new__(cls, *args, **kwargs):

        #判断类属性是否为空，为空就为其分配农村
        if cls.instance is None:
            #调用父类方法，为第一个对象分配空间
            cls.instance=super().__new__(cls)

        #返回类属性保存的引用对象
        return cls.instance


    #单例模式设计，让初始化方法只执行一次
    if_init=False
    def __init__(self):
        #判断初始化动作是否执行过
        if Player.if_init:
            return
        #如果已经执行过，返回引用
        print("初始化播放器")
        #修改类属性的标记，让初始化动作只执行一次，增加对象
        #初始化动作不再执行
        Player.if_init=True

player1=Player()
print(player1)
player2=Player()
print(player2)


结果：
初始化播放器
<__main__.Player object at 0x000001C4F0F7D7F0>
<__main__.Player object at 0x000001C4F0F7D7F0>

```

#### 异常

1.异常的概念

![image-20220314210229185](https://github.com/zxingq/down/raw/main/img/image-20220314210229185.png)



2.错误类型的捕获

- 在程序执行时，出错的错误类型不止一种

```python
try:
    num=int(input("请输入一个整数"))
    result=8/num
    print(result)
except ValueError:
    print("请输入整数")
except Exception as error:
    print("未知错误类型%s"%error)
#如果代码块执行没有出现错误，else就不执行
else:
    print("尝试成功，没有代码块错误")
#finally，不管代码执行是否成功，finally都执行
finally:
    print("程序运行结束")
print("-"*40)


结果：    
请输入一个整数2
4.0
尝试成功，没有代码块错误
程序运行结束
--------------------------

```



4.抛出raise异常

场景应用

![image-20220314214307966](https://github.com/zxingq/down/raw/main/img/image-20220314214307966.png)

```python
def password():
    passwd=input("请输入密码")
    #判断密码长度>8则密码正确
    if len(passwd)>=8:
        return
    #密码长度不够，抛出异常
    print("密码长度不够!!")
    #主动抛出异常的结果作为参数即ex传递给result在控制台输出
    ex=Exception("密码长度不够")
    #抛出异常
    raise ex
try:
    print(password())
except Exception as result:
    print("错误---%s"%result)
    
    
结果：
请输入密码a
密码长度不够!!
错误---密码长度不够

```

**文件**

1.打开文件

2.读写文件

read方法可以一次性读入并返回文件的所有内容

3.关闭文件

如果忘记关闭文件，会造成系统资源的消耗影响后续文件的打开

**文件指针**

文件指针标记在执行了read方法后，会移动到读取内容的末尾

文件打开方式：

![image-20220321213918531](https://github.com/zxingq/down/raw/main/img/image-20220321213918531.png)



### 项目：

使用pygame创建图形窗口

1.小游戏的目标初始化和退出

2.理解游戏中的坐标

3.创建游戏主窗口p

4，简单游戏循环

要描述一个矩形区域使用pygame.Rect用来描述矩形区域

Reat(x,y,weight,height)

2.创建游戏窗口

pygame.display.set_mode()  -----返回的结果是游戏窗口

要使窗口一直在---无限循环在游戏中称为游戏循环

while True

​			pass

理解图像并进行图像绘制

1.使用pygame.image.load加载图像数据

2.使用游戏屏幕对象，调用bit方法将图像绘制到指定位置

3.调用pygame.display.updata()方法更新整个屏幕显示

![image-20220323203109263](https://github.com/zxingq/down/raw/main/img/image-20220323203109263.png)



![image-20220323211255947](https://github.com/zxingq/down/raw/main/img/image-20220323211255947.png)

游戏时钟

创建时钟对象，通过无限循环，将图像进行动画

pygame.time.clock

刷新帧率clock.tick(60)

- 更新我方飞机的位置

  - 创建飞机对象纪录飞机初始位置play_rect=pygame.Rect(x,y,weight,height)

    

  - 修改飞机的位置

  - play_rect.(x或y)改变-或+=1

  - 在循环中使用blit绘制飞机图像交替使用背景和飞机的绘制，实现飞机不出现残影screen.dblit(bg,(0,0))   scree.blit(my_play,play_rect)

在游戏循环中的监听事件

用户对游戏进行的操作，程序判断处用户所作的操作

，并进行响应。

退出循环

![image-20220323221813177](https://github.com/zxingq/down/raw/main/img/image-20220323221813177.png)

​		

```python
#列表就纪录了用户游戏时进行的操作
event_list=pygame.event.get()
for event in event_list:
    #判断操作是否为退出循环
    if event.type==pygame.QUIT:
        #quit卸载所有模块
        pygame.quit()
        print("退出游戏！！！！")
        #exit退出
        exit()

```

#### 精灵和精灵组

精灵和精灵组是python提供的高级类

- 在刚刚完成的案例中，图像加载，位置变换，绘制图像都需要程序员编写代码处理

  ![image-20220324170326058](https://github.com/zxingq/down/raw/main/img/image-20220324170326058.png)

```
pygame.sprite.Sprite---存储图像数据image的对象和位置rect的对象

```

**某个子类的父类不是object基类要在初始化方法中主动调用父类的方法**

```python
**某个子类的父类不是object基类要在初始化方法中主动调用父类的方法**
super().__init__

```

游戏主框架

采用私有属性方法，可以保证直接对私有属性直接进行改变，不用再进行初始化设置

![image-20220324205107516](https://github.com/zxingq/down/raw/main/img/image-20220324205107516.png)

在开发时

为了保证代码的可行性，尽量不要使用魔法数字（固定数字）

如果要使用一些数字最好把它设置为固定的常量

![](https://github.com/zxingq/down/raw/main/img/image-20220324211313667.png)

通过实例定义的变量只能被实例方法访问，而直接在类中定义的静态变量(如本例的name变量)即可以被实例方法访问，也可以被静态方法和类方法访问。实例方法不能被静态方法和类方法访问，但静态方法和类方法可以被实例方法访问。

绘制背景图像让主角相当于没有位置变化

![image-20220325101542911](https://github.com/zxingq/down/raw/main/img/image-20220325101542911.png)

- 设置背景图像
  - 判断背景图像是否移出屏幕，如果移出屏幕，将图像移动到屏幕上方，形成交替效果

![image-20220325102103265](https://github.com/zxingq/down/raw/main/img/image-20220325102103265.png)

```python
import random
import pygame

# 屏幕大小的常量
SCREEN_RECT = pygame.Rect(0, 0, 480, 700)
# 刷新的帧率
FRAME_PER_SEC = 60
# 创建敌机的定时器常量
CREATE_ENEMY_EVENT = pygame.USEREVENT
# 英雄发射子弹事件
HERO_FIRE_EVENT = pygame.USEREVENT + 1


class GameSprite(pygame.sprite.Sprite):
    """飞机大战游戏精灵"""

    def __init__(self, image_name, speed=1):
        # 调用父类的初始化方法
        super().__init__()

        # 定义对象的属性
        self.image = pygame.image.load(image_name)
        self.rect = self.image.get_rect()
        self.speed = speed

    def update(self):
        # 在屏幕的垂直方向上移动
        self.rect.y += self.speed


class Background(GameSprite):
    """游戏背景精灵"""

    def __init__(self, is_alt=False):

        # 1. 调用父类方法实现精灵的创建(image/rect/speed)
        super().__init__("./picture/background.png")

        # 2. 判断是否是交替图像，如果是，需要设置初始位置
        if is_alt:
            self.rect.y = -self.rect.height

    def update(self):

        # 1. 调用父类的方法实现
        super().update()

        # 2. 判断是否移出屏幕，如果移出屏幕，将图像设置到屏幕的上方
        if self.rect.y >= SCREEN_RECT.height:
            self.rect.y = -self.rect.height


class Enemy(GameSprite):
    """敌机精灵"""

    def __init__(self):
        # 1. 调用父类方法，创建敌机精灵，同时指定敌机图片
        super().__init__("./picture/enemy1.png")

        # 2. 指定敌机的初始随机速度 1 ~ 3
        self.speed = random.randint(1, 3)

        # 3. 指定敌机的初始随机位置
        self.rect.bottom = 0

        max_x = SCREEN_RECT.width - self.rect.width
        self.rect.x = random.randint(0, max_x)

    def update(self):
        # 1. 调用父类方法，保持垂直方向的飞行
        super().update()

        # 2. 判断是否飞出屏幕，如果是，需要从精灵组删除敌机
        if self.rect.y >= SCREEN_RECT.height:
            # print("飞出屏幕，需要从精灵组删除...")
            # kill方法可以将精灵从所有精灵组中移出，精灵就会被自动销毁
            self.kill()

    def __del__(self):
        # print("敌机挂了 %s" % self.rect)
        pass


class Hero(GameSprite):
    """英雄精灵"""

    def __init__(self):

        # 1. 调用父类方法，设置image&speed
        super().__init__("./picture/hero1.png", 0)

        # 2. 设置英雄的初始位置
        self.rect.centerx = SCREEN_RECT.centerx
        self.rect.bottom = SCREEN_RECT.bottom - 120

        # 3. 创建子弹的精灵组
        self.bullets = pygame.sprite.Group()

    def update(self):

        # 英雄在水平方向移动
        self.rect.x += self.speed

        # 控制英雄不能离开屏幕
        if self.rect.x < 0:
            self.rect.x = 0
        elif self.rect.right > SCREEN_RECT.right:
            self.rect.right = SCREEN_RECT.right

    def fire(self):
        print("发射子弹...")

        for i in (0, 1, 2):
            # 1. 创建子弹精灵
            bullet = Bullet()

            # 2. 设置精灵的位置
            bullet.rect.bottom = self.rect.y - i * 20
            bullet.rect.centerx = self.rect.centerx

            # 3. 将精灵添加到精灵组
            self.bullets.add(bullet)


class Bullet(GameSprite):
    """子弹精灵"""

    def __init__(self):
        # 调用父类方法，设置子弹图片，设置初始速度
        super().__init__("./picture/bullet1.png", -2)

    def update(self):
        # 调用父类方法，让子弹沿垂直方向飞行
        super().update()

        # 判断子弹是否飞出屏幕
        if self.rect.bottom < 0:
            self.kill()

    def __del__(self):
        print("子弹被销毁...")


```



```python
import pygame
from plane_sprites1 import *


class PlaneGame(object):
    """飞机大战主游戏"""

    def __init__(self):
        print("游戏初始化")

        # 1. 创建游戏的窗口
        self.screen = pygame.display.set_mode(SCREEN_RECT.size)
        # 2. 创建游戏的时钟
        self.clock = pygame.time.Clock()
        # 3. 调用私有方法，精灵和精灵组的创建
        self.__create_sprites()

        # 4. 设置定时器事件 - 创建敌机　1s
        pygame.time.set_timer(CREATE_ENEMY_EVENT, 1000)
        pygame.time.set_timer(HERO_FIRE_EVENT, 500)

    def __create_sprites(self):

        # 创建背景精灵和精灵组
        bg1 = Background()
        bg2 = Background(True)

        self.back_group = pygame.sprite.Group(bg1, bg2)

        # 创建敌机的精灵组
        self.enemy_group = pygame.sprite.Group()

        # 创建英雄的精灵和精灵组
        self.hero = Hero()
        self.hero_group = pygame.sprite.Group(self.hero)

    def start_game(self):
        print("游戏开始...")

        while True:
            # 1. 设置刷新帧率
            self.clock.tick(FRAME_PER_SEC)
            # 2. 事件监听
            self.__event_handler()
            # 3. 碰撞检测
            self.__check_collide()
            # 4. 更新/绘制精灵组
            self.__update_sprites()
            # 5. 更新显示
            pygame.display.update()

    def __event_handler(self):

        for event in pygame.event.get():

            # 判断是否退出游戏
            if event.type == pygame.QUIT:
                PlaneGame.__game_over()
            elif event.type == CREATE_ENEMY_EVENT:
                # print("敌机出场...")
                # 创建敌机精灵
                enemy = Enemy()

                # 将敌机精灵添加到敌机精灵组
                self.enemy_group.add(enemy)
            elif event.type == HERO_FIRE_EVENT:
                self.hero.fire()
            # elif event.type == pygame.KEYDOWN and event.key == pygame.K_RIGHT:
            #     print("向右移动...")

        # 使用键盘提供的方法获取键盘按键 - 按键元组
        keys_pressed = pygame.key.get_pressed()
        # 判断元组中对应的按键索引值 1
        if keys_pressed[pygame.K_RIGHT]:
            self.hero.speed = 2
        elif keys_pressed[pygame.K_LEFT]:
            self.hero.speed = -2
        else:
            self.hero.speed = 0

    def __check_collide(self):

        # 1. 子弹摧毁敌机
        pygame.sprite.groupcollide(self.hero.bullets, self.enemy_group, True, True)

        # 2. 敌机撞毁英雄
        enemies = pygame.sprite.spritecollide(self.hero, self.enemy_group, True)

        # 判断列表时候有内容
        if len(enemies) > 0:
            # 让英雄牺牲
            self.hero.kill()

            # 结束游戏
            PlaneGame.__game_over()

    def __update_sprites(self):

        self.back_group.update()
        self.back_group.draw(self.screen)

        self.enemy_group.update()
        self.enemy_group.draw(self.screen)

        self.hero_group.update()
        self.hero_group.draw(self.screen)

        self.hero.bullets.update()
        self.hero.bullets.draw(self.screen)

    @staticmethod
    def __game_over():
        print("游戏结束")

        pygame.quit()
        exit()


if __name__ == '__main__':
    # 创建游戏对象
    game = PlaneGame()

    # 启动游戏
    game.start_game()


```

> 



 





### 类的内置函数

- issubclass(A，B):用于判断A是否为B的子类
- hasattr(c1,'x'):x是否为实例化对象c1的一个属性。

#### 魔法方法

- `__init__()`: 构造器，当一个实例被创建的时候调用的初始化方法。 

- `__new__(cls, [...])`  : 
  - (1)是在一个对象实例化的时候所调用的第一个方法，所以它才是真正意义上的构造方法。
  - (2)它的第一个参数是这个类，其他的参数是用来直接传递给 __init__ 方法。
  - （3）__new__ 决定是否要使用该 __init__ 方法，因为 __new__ 可以调用其他类的构造方法或者直接返回别的实例对象来作为本类的实例，如果 __new__ 没有返回实例对象，则 __init__ 不会被调用。
  - （4）__new__ 主要是用于继承一个不可变的类型比如一个 tuple 或者 string。



```python
class g(float):
    """千克转克"""
    def __new__(cls, kg):
        return float.__new__(cls, kg * 2)

a = g(50) # 50千克转为克
print(a) 	# 100
print(a + 100)	# 200 由于继承了float，所以可以直接运算，非常方便！


```



- `__del__()`方法：析构器，当一个实例被销毁时自动调用的方法 

- ```python
  class Washer:
      def __del__(self):
          """
          当删除对象时，解释器会自动调用del方法
          """
          print('对象已删除！')
  
  haier = Washer() 
  
  ```

- 算数运算：

  - __add__(self,other)

  - __sub__(self,other)

  - ```python
    class New_int(int):
        def __add__(self,other):
            return int.__sub__(self,other)
        def __sub__(self,other):
            return int.__add__(self,other)
    a=Newint(3)
    b=Newint(5)
    print(a+b)
    print(a-b)
    #结果：
    -2
    8
    
    
    ```

#### 迭代器

一个可迭代对象一定能通过for循环进行访问，能通过for循环访问的不一定是可迭代对象

描述符就是将某种特殊类型的类的实例指派给另一个类的属性。

当解释器需要迭代对象时，会自动调用iter(x)

- ```python
  一个对象只要含有__iter__方法那么它就是一个可迭代对象。
  
  .一个类（对象）只要含有“__iter__”、"__next__"两个方法，就将其称为迭代器。
  
  对于__iter__方法，它需要具有一个可以返回一个迭代器对象的功能
  
  对于__next__方法，它需要标记并返回下一个迭代器对象。
  
  ```

 迭代器是一个可以**记住遍历位置**的对象，因此不会像列表那样一次性全部生成，而是可以等到用的时候才生成，因此**节省了大量的内存资源**。迭代器对象从集合中的第一个元素开始访问，直到所有的元素被访问完。迭代器有两个方法：__iter__（）和__next__（）方法。 

```python
#coding:gbk
from collections.abc import Iterable
from collections.abc import  Iterator
import time
class Myclass(object):
    def __init__(self):
        self.name=list()
        self.name_num=0
    def add(self,name):
        self.name.append(name)
    def __iter__(self):
        return self
    def __next__(self):
        if self.name_num < len(self.name):
            result=self.name[self.name_num]
            self.name_num+=1
            return result
        else:
            raise StopIteration
classment=Myclass()
classment.add('赵晓璐')
classment.add('韩孝胥')
classment.add('孙晓名')

print("判断是否是可迭代的对象：", isinstance(classment, Iterable))

print("判断是否是迭代器：", isinstance(classment, Iterator))

for name in classment:
    print(name)
    time.sleep(2)
    
 结果：
判断是否是可迭代的对象： True
判断是否是迭代器： True
赵晓璐
韩孝胥
孙晓名

Process finished with exit code 0


```

```python
class Fibonacci(object):
    """斐波那契数列得迭代器"""
    def __init__(self,nums):
        self.nums = nums   # 传入参数，生成斐波那契数列的个数
        self.a = 0   
        self.b = 1
        self.i =0    # 用于记忆生成的个数
    def __iter__(self):
        return self
 
    def __next__(self):
           
       ret = self.a   # 记忆第一个数
 
       if self.i < self.nums:
            self.a, self.b = self.b,self.a +self.b
            self.i += 1
            return ret
       else:
           raise StopIteration   # 停止迭代
 
nums = int(input("请输入需要生成Fibonacci数列项的个数："))
fobo = Fibonacci(nums)
 
for num in fobo:
    print(num)
 
 结果：
请输入需要生成Fibonacci数列项的个数：12
0
1
1
2
3
5
8
13
21
34
55
89

Process finished with exit code 0

```

注意：

- 可迭代对象**不一定**是迭代器。

- 迭代器**一定**是可迭代对象。

- 容器类型（list tuple dict str set ）是**可迭代对象**但不是迭代器。

#### 生成器

生成器函数会生成一个生成器对象。在python社区中，大多数情况下将迭代器与生成器视为同一个概念。

只要python函数的定义体中有yield关键字，该函数就是生成器函数。调用生成器函数，会返回一个生成器对象。

```python
import re
import reprlib
class Sentence:
    def __init__(self,text):
        self.text=text
        self.words = re.compile('\w+').findall(self.text)
    def __repr__(self):
        return 'Sentence(%s)'%reprlib.repr(self.text)
    def __iter__(self):
        for word in self.words:
            yield word
        return
s=Sentence('No matter where you are')
for word in s:
    print(word)
结果：
No
matter
where
you
are

Process finished with exit code 0


```

**惰性实现**

上面的生成器函数，它是在构建self.words这样一个列表来进行正则表达式文本单词匹配，但是这样耗费的空间与资源特别大。**因此采用re.finditr函数来替换re.findall**，它返回的不是一个列表，而是一个生成器。

```python
#coding:gbk
import re
import reprlib
class sentence:
    def __init__(self,text):
        self.text=text
    def __repr__(self):
        return 'Sentence(%s)'%reprlib.repr(self.text)
    # def __iter__(self):
    #     for match in re.compile('\w+').finditer(self.text):
    #         yield match.group()
    #可以将上面的代码简化为
    def __iter__(self):
        return (match.group()for match in re.compile('\w+').finditer(self.text))
s1=sentence('No matter where you are')
for word in s1:
    print(word)
结果：
No
matter
where
you
are

Process finished with exit code 0

```

如果生成器表达式要分成多行写，我倾向于定义生成器函数。

```Python
#coding:gbk
class Dchashul:
    def __init__(self,begin,step,end=10):
        self.begin=begin
        self.step=step
        self.end=end
    def __iter__(self):
        #用type得知self.begin+self.step的类型，并将result先赋值为self.begin的值
        result=type(self.begin+self.step)(self.begin)
        forever=self.end is None
        index=0
        while forever or result<self.end:
            yield result
            index +=1
            result=self.begin+self.step*index
d=Dchashul(1,2)
print(list(d))
结果：
[1, 3, 5, 7, 9]

Process finished with exit code 0

```

**itertools模块的使用**

```python
#coding:gbk
import itertools

def dchashul_gen(begin,step,end):
    first=type(begin+step)(begin)
    ap_gen=itertools.count(first,step)
    if end:
        ap_gen=itertools.takewhile(lambda n:n<end,ap_gen)
        # # itertools.takewhile函数不同，它会生成一个使用另一个生成器的生成器
        # gen = itertools.takewhile(lambda n: n < 3, itertools.count(1, 0.5))
        return list(ap_gen)
result=dchashul_gen(1,2,10)
print(result)

结果：
[1, 3, 5, 7, 9]

Process finished with exit code 0

```

### 函数

一.函数

**1**.函数定义的代码必须在函数调用的上方

**2**.函数的文档注释：

为了知道函数具有什么样的作用，可以采用函数注释

在函数名字下方使用三个“，格式为"""求和”“”,在调用函数的时候选中函数名称再按住ctrl+Q就可以查看函数作用。

**形参**：定义函数时，小括号中的函数，在函数的内部中作为变量使用

**实参**：调用函数时，小括号中的函数

```
def sum1(num1,num2):
    """实数求和"""
    result=num1+num2
    print("%d=%d+%d"%(result,num1,num2))
sum1(3,6)

```

```python
#定义一个函数可以增加函数的灵活度
def printline(char,n):
    print(char*n)
printline("#",20)
def printlines(char,times):
    a=0;
    while a<5:
        printline(char,times)
        a+=1
printlines("#",40)

```

**3**.使用模块中的函数

模块就相当于一个工具包。

模块可以使曾经编写过的代码更方便自己的重复使用

**模块**也可能是一个**标识符**

二.高级数据类型

len:统计列表中的数据总数

count:统计列表中相同数据出现的次数。

del:将数据从列表中删除，连同内存删除。

**函数：**封装了独立功能，可以直接调用

方法：和函数类似，同样是封装了独立的功能

方法需要通过对象来调用，表示针对这个对象要做的操作

**元组：*元组与列表相似，不同之处在于元素不能进行修改*

列表和元组都是有序的集合

字典是一个无序的数据集合。

**切片**：左闭右开  str[:]完整的字符串，字典不能进行切片

str[开始的字符:结束的字符:切片的长度] str[-1]:最后一个元素

str[-1::-1]:从最后一个元素向前进行切片，即为倒序。

![image-20220303215038763](https://github.com/zxingq/down/raw/main/img/image-20220303215038763.png)
**语法进阶**

看到赋值语句，首先把注意力放在等号的右侧

调用函数时，本质上传递的是实参保存数据的引用，而不是实参保存的数据 ！

return  语句返回的是保存数据的引用，而不是数据

**可变类型与不可变类型**：

注意：1.可变类型的数据变化，是通过方法实现的

2.如果给一个可变类型的变量，赋值一个新的数据，引用（内存地址）会修改

 字典中的key只能使用不可变类型的数据 ，不可变类型的数据有整型，字符串型，元组型

**哈希**

接受一个不可变类型的数据作为参数

返回结果是一个整型，哈希是一种算法，其作用就是提取数据的特征码

**局部变量和全局变量**

局部变量：定义在函数内部的变量，只能在函数内部使用    在函数执行结束后，系统内部的局部变量将会被系统收回

在python中不能在函数内部直接修改全局变量

global关键字会告诉解释器后面的变量是一个全局变量，再使用赋值语句时，就不会创建局部变量

shift+F6可以修改全局变量的名字

**函数的参数和返回值的作用**

返回值是函数完成工作后，最后给调用者的一个结果

问题2:

*如果传递参数是**可变类型**，在函数内部，使用方法修改了数据的内容，同样会影响到外部的数据*

*缺省参数*

定义函数时，可以给某个参数指定一个默认值，具有默认值的参数就叫做缺省参数

注意：1.带有参数值的缺省参数要放在所有参数的后面  **def quesheng(name,header=True):**

2.调用带有多个缺省参数的函数，需要指定参数名，这样才能知道参数的对应关系**quesheng("小梦",gender=False)**

多值参数：在参数前面增加一个星号，可以接收一个元组

​					在参数前面增加两个星号，可以增加一个字典

```python
def demo(num,*nums,**numss):
    """
    多值参数
    :param num: 用逗号分离，接收1这个数字
    :param nums:在参数前面增加一个星号，接收一个元组
    :param numss:在参数前面增加两个星号了，接收一个字典
    """
    print(num)
    print(nums)
    print(numss)
demo(1,2,3,4,5,name="小明",age=18)

```

**递归**

特点：1.函数自己调用自己

2.一定要拥有出口，即循环条件，否则会造成死循环

#### 内置函数

运行Python代码需要一个叫做 Python解释器 的东西，解释器也是一个程序，它为Python使用者提供了一些常用的功能，并取了独一无二的名字，这就是我们所说的**“内置函数”**。

就是由于Python内置函数，伴随着Python解释器一起启动，因此内置函数不需要导入，就可以直接使用。


- `input()`：该函数接受一个标准输入数据，返回为 string 类型。 

  - ```python
    x = input("请输入你的姓姓名：")
    print(f"我的名字是{x}")
    
    ```

- `enumerate()`：该函数获取一个集合（例如，元组），并将其作为枚举对象返回。 

  - ```python
    x = ["张三","李四","王五"]
    for index, value in enumerate(x):
        print(f"我叫{value}，我在列表中的索引是{index}")
    
    
    ```

- `eval()`：该函数用来执行一个字符串表达式，并返回表达式的值。 

  - ```python
    x = 50
    eval( '3 * x' )
    x = 'print("打印这个字符串")'
    eval(x)
    
    
    ```

- `format()`：该函数用于字符串格式化。 

  - ```python
    "{:.2f}".format(3.1415926)
    
    "{0} {1}".format("hello", "world")
    
    ```

- `map()`：该函数会根据提供的函数，对指定序列做映射。 

  - ```python
    list(map(func,[1,2,3,4,5]))
    
    list(map(lambda x: x * 2, [1, 2, 3, 4, 5]) )
    
    ```

- `print()`：该函数用于打印输出。 

  - ```python
    print("Hello World")  
    
    print("www","baidu","com",sep=".")  # 设置间隔符
    
    ```

- `range()`：在Python3中，该函数返回的是一个可迭代对象（类型是对象），而不是列表类型， 所以打印的时候不会打印列表。 

  - ```python
    list(range(1,10))
    list(range(1,10,2)) # 指定步长
    
    ```

- `reversed()`：该函数没有返回值，但是会对列表的元素进行反向排序。 

  - ```python
    x = ["a", "b", "c", "d"]
    for i in reversed(x):
        print(i)
    
    ```

- `zip()`：该函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的对象，这样做的好处是节约了不少的内存。 

  - ```python
    a = [1,2,3]
    b = [4,5,6]
    list(zip(a,b))
    for i,j in zip(a,b):
        print(f"打印{i}，再打印{j}")
    
    ```

    

#### 匿名函数

定义： 在定义函数的时候，不想给函数起一个名字。这个时候就可以用lambda来定义一个匿名函数 ,python的简单句法限制了lambda函数的定义体只能使用纯表达式。（lambda表达式的定义体中不能赋值，也不能使用while和try等python语句）

**传递多个参数**

```python
func = lambda x, y, z: x + y + z
ret = func(1, 2, 3)
print(ret)
结果：
6

```

**使用if...else...语句**

```python
func = lambda x, y: x if x > y else y
ret = func(2, 6)
print(ret)
结果:
6

```

**使用max函数求字典最大值**

```python
dic = {'age1': 12, 'age2': 13, 'age3': 14}
 
ret = max(dic, key=lambda x: dic[x])
print(ret)
结果：
age3

```

**元组转化为字典并生成列表**

```python
a = (('a'), ('b'))
b = (('c'), ('d'))
 
ret = list(map(lambda x: {x[0]: x[1]}, zip(a, b)))
print(ret)
结果：
[{'a':'c'},{'b','d'}]

```

**map函数在匿名函数的使用**

map函数就是将列表里面的元素进行遍历并把遍历的元素作为参数传递到函数里面

```python
mobj=map(lambda x:x**2,[1,2,3,4,5])
print(list(mobj))
結果：
[1, 4, 9, 16, 25]

```

**使用lambda表达式反转拼接**

```python
fruits=['strawberry','fig','apple','cherry','raspberry','banana']
fruits_sort=sorted(fruits,key=lambda x:x[::-1])
print(fruits_sort)
结果：
['banana', 'apple', 'fig', 'raspberry', 'strawberry', 'cherry']

```

#### **高阶函数**

 **定义**：一个函数接收另一个函数作为参数，或者把函数函数作为结果返回的函数称之为高阶函数。 

```python
def add(x , y , f):
    return f(x) + f(y)
print add(-5 , 6 , abs)
结果：
11

```

 把函数A作为另一个函数B的参数传入，那么函数B称为高阶函数，函数式编程就是指这种高度抽象的编程范式。 

最为人熟知的高阶函数有：

- map
- filter
- reduce
- apply

#### 闭包

函数内部的的属性，都是有生命周期，都是在函数执行期间

 python中的闭包从表现形式上定义（解释）为：如果在一个内部函数里，对在外部作用域（但不是在全局作用域）的变量进行引用，那么内部函数就被认为是闭包(closure). 

闭包内的闭包函数私有化了变量，完成数据封装，类似与面向对象。

```python
list1=[1,2,3,4,5]
def func(obj):
    print('func',obj)
    def fun1():
        obj[2] += 1
        print('this is fun1',obj)
    return fun1
var=func(list1)
var()
var()
var()
结果：
func [1, 2, 3, 4, 5]
this is fun1 [1, 2, 4, 4, 5]
this is fun1 [1, 2, 5, 4, 5]
this is fun1 [1, 2, 6, 4, 5]

Process finished with exit code 0

```



#### 装饰器（语法糖）

简而言之，**python装饰器就是用于拓展原来函数功能的一种函数**。 这个函数的特殊之处在于它的返回值也是一个函数，使用python装饰器的好处就是在不用更改原函数的代码前提下给函数增加新的功能。 （基于闭包）

装饰器可调用的对象，其参数是另一个函数。

- 装饰器的两大特性：
  - 能把被装饰的函数替换成其他函数
  - 装饰器在加载模块时立即执行

装饰器将逻辑部分代码与计数部分代码（其他代码分开。）

#既不需要侵入，也不需要函数重复执行

```python
#coding:gbk
import time
#创建一个函数用于判断传入的数是否为质数
def Decorator(func):
    #这里定义的函数的功能用于计算程序执行的时间
    #*args指代从print_prime函数里面传进来的参数，不限制个数
    def wrapper(*args):
        start=time.time()
        result=func(*args)
        end=time.time()
        print("{}到{}内的质数查找总共用了{:.4}s".format(*args,(end-start)))
        return result
    return wrapper

def prime_num(num):
    if num<2:
        return False
    elif num==2:
        return True
    else:
        for i in range(2,num):
            if num%i==0:
                return False
        return True
#创建一个函数，属于逻辑部分代码，用于判断区间内的质数个数
#在这引入装饰器，用于将逻辑部分的代码与计算时间部分的代码区分开
@Decorator
#当程序读到装饰符的时候就执行print_prime相当于执行wrapper这个函数开始对质数计数
def print_prime(minnum,maxnum):
    count = 0
    for i in range(minnum,maxnum):
        if prime_num(i):
            count+=1
    return count
count1=print_prime(1,1000)
print(count1)
结果：
1到1000内的质数查找总共用了0.00399s
168
Process finished with exit code 0

```

这里的deco函数就是最原始的装饰器，它的参数是一个函数，然后返回值也是一个函数。其中作为参数的这个函数func()就在返回函数wrapper()的内部执行。然后在函数func()前面加上@deco，func()函数就相当于被注入了计时功能，现在只要调用func()，它就已经变身为“新的功能更多”的函数了。
所以这里装饰器就像一个注入符号：有了它，拓展了原来函数的功能既不需要侵入函数内更改代码，也不需要重复执行原函数。
 **多个装饰器执行的顺序就是从最后一个装饰器开始，执行到第一个装饰器，再执行函数本身。**

```Python
#coding:gbk
import time

def deco01(func):
    def wrapper(*args, **kwargs):
        print("this is deco01")
        startTime = time.time()
        func(*args, **kwargs)
        endTime = time.time()
        msecs = (endTime - startTime)*1000
        print("time is %d ms" %msecs)
        print("deco01 end here")
    return wrapper

def deco02(func):
    def wrapper(*args, **kwargs):
        print("this is deco02")
        func(*args, **kwargs)

        print("deco02 end here")
    return wrapper

@deco01
@deco02
def func(a,b):
    print("hello，here is a func for add :")
    time.sleep(1)
    print("result is %d" %(a+b))



if __name__ == '__main__':
    f = func
    f(3,4)

结果：
this is deco01
this is deco02
hello，here is a func for add :
result is 7
deco02 end here
time is 1007 ms
deco01 end here

Process finished with exit code 0

```

```
*args 表示任何多个无名参数， 他本质上是一个 tuple** kwargs 表示关键字参数， 它本质上是一个 dict同时使用时必须要求 *args 参数列要在** kwargs 前面【因为位置参数在关键字参数的前面。】

```

***args**：

- *args 和 ** args 主要用于函数定义，你可以将不定数量的参数传递给一个函数。
- 这里不定的意思是： 预先并不知道，函数使用者会传递多少个参数给你，所在在这个场景下使用这两个关键字。 * args 是用来发送一个 非键值 的可变数量的参数列表给一个函数。

***kwargs**

- `**kwargs`允许你将不定长度的 【键值对 key-value 】，作为参数传递给一个函数。如果你想要在一个函数里处理带名字的参数，你应该使用`**kwargs` 

#### 模块

- 容器---->数据的封装
- 函数---->语句的封装
- 类------>方法和属性的封装
- 模块----->模块就是程序

搜索模块路径：

模块查找顺序：

1.内存中已经加载的模块-------- >内置模块-------- >sys.path路径中包含的模块

sys.path的第一个路径是当前执行文件的路径

>>> import sys
>>> sys.path
>>> ['', 'C:\\Users\\dell\\AppData\\Local\\Programs\\Python\\Python38\\Lib\\idlelib', 'C:\\Users\\dell\\AppData\\Local\\Programs\\Python\\Python38\\python38.zip', 'C:\\Users\\dell\\AppData\\Local\\Programs\\Python\\Python38\\DLLs', 'C:\\Users\\dell\\AppData\\Local\\Programs\\Python\\Python38\\lib', 'C:\\Users\\dell\\AppData\\Local\\Programs\\Python\\Python38', 'C:\\Users\\dell\\AppData\\Local\\Programs\\Python\\Python38\\lib\\site-packages']

导入其他包下的模块

import 包.模块名

#### Python数据模型

**特殊方法**

特殊方法又称为双下方法（魔术方法）。 特殊方法主要应用于类中，方便了类的一些操作操作。

 <img src="https://img-blog.csdn.net/20171026180704114?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM3NzIwMTcy/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="这里写图片描述" style="zoom: 67%;" /> 

特殊方法来实现数据模型有两大好处：

- 作为类的用户，不必记住标准操作各式的名称
- 更加方便的使用了Python的标准库

```Python
#coding:gbk
import collections
from random import choice
#首先利用模块创建一个命名元组card代表名字纸牌，spot代表纸牌的点数，suit代表纸牌类型花色
Cards=collections.namedtuple('Card',['spot','suit'])
class Getcard:
    #先规定纸牌的点数与花色
    spot=[str(n) for n in range(2,11)]+list('JQKA')
    suit='黑桃 方块 梅花 红桃'.split()
    def __init__(self):
        #对一摞纸牌进行初始化
        self.cards=[Cards(spot,suit) for spot in self.spot
                    for suit in self.suit]
    def __len__(self):
        #获取一摞纸牌的数量
        return len(self.cards)
    def __getitem__(self, item):
        #进行纸牌索引，查找第几张纸牌或第几张到第几张纸牌是什么
        return self.cards[item]
beer_card=Cards('7','梅花')
print(beer_card)
deck=Getcard()
print(len(deck))
#获取这一摞中第25张纸牌
print(deck[25])
#随机从中抽取纸牌
print(choice(deck))
#抽取前三张纸牌
print(deck[:3])
#从第12张纸牌开始，每隔13张纸牌抽取一次
print(deck[12::13])
结果：
Card(spot='7', suit='梅花')
52
Card(spot='8', suit='方块')
Card(spot='2', suit='方块')
[Card(spot='2', suit='黑桃'), Card(spot='2', suit='方块'), Card(spot='2', suit='梅花')]
[Card(spot='5', suit='黑桃'), Card(spot='8', suit='方块'), Card(spot='J', suit='梅花'), Card(spot='A', suit='红桃')]

Process finished with exit code 0


```

##### repr

python中有一个内置的函数叫做repr，它能把一个对象用字符串的形式表达出来以便辨认。repr就是通过__repr__这个特殊方法来得到一个字符串表达形式的。

__repr__和__str__的区别在于，后者是在str()函数被使用，或者是在print()函数打印一个对象的时候才被调用，并且他返回的字符串对终端更为友好。





### 数据结构

#### 序列构成的数组

- **列表推倒和生成器表达式**	
  - ​	列表推倒式

列表推倒是构建列表的快捷方式，可以使得所写的代码拥有更好的可读性。

```python
a=[i for i in range(30) if i%3 == 0]# 完整的列表推导式
结果：
[0, 3, 6, 9, 12, 15, 18, 21, 24, 27]

```

字典推倒式

```python
#字典推倒式，笛卡尔积应用
colors=['black','white']
sizes=['S','M','l']
dicts=[(color,size)for color in colors for size in sizes]
print(dicts)
结果：
[('black', 'S'), ('black', 'M'), ('black', 'l'), ('white', 'S'), ('white', 'M'), ('white', 'l')]

```

集合推倒式

```python
squared = {x**2 for x in [1,-1,2]}
print(squared)
结果
{1, 4}      

```



- 生成器表达式

  生成器表达式背后遵循了迭代器协议，这样可以逐个的产生元素，而不是先创建一个完整的元素。显然这样更节省内存。

  ```python
  gen_L = (x * x for x in range(10))
  for i in gen_L:
      print(i)
  结果：
  0
  1
  4
  9
  
  ```

#### 元组

元组其实是对数据进行记录

- Python中的元组tuple和列表list类似，不同之处在于：元组的元素不能修改，所以被称为不可变列表；在形式上，元组用小括号()表示，而列表用中括号[]表示；在计算过程中，元组的处理将比列表要快。 

- 元组不能更改，如果要修改元组，我们只能通过变量进行重新赋值，不能进行元素的增删，否则会报错。

  - **元组的拆包**

    - 元组的拆包就是将元组内部的每个元素按照位置，对应的赋值给不同变量。 

    - **不仅是元组，** 在python中任何序列或可迭代对象（如：列表、元组、字符串、文件对象、迭代器和生成器等），皆可通过类似这样的简单赋值语句拆包给多个变量。  唯一的要求就是**变量必须跟序列元素的数量一致**，否则会抛出ValueError的异常 

      ```Python
      lax_coordinates=(33.9425,-118.4080056)
      latitude,longitude=lax_coordinates
      print(latitude)
      print(longitude)
      结果：
      33.9425
      -118.4080056
      
      ```

      

  - **占位符的使用**

    - **一般使用" _ "来代表一个占位符** 。

    - **一般使用 \* 来代表多个占位符** 

    - *前缀只能用于一个变量名， 但是这个变量可以出现在赋值表达式的任意位置。 \* 占位符拆出来的变量永远是list列表类型。 

    - ```python
      a,b,*rest=range(5)
      print(a,b,rest)
      结果：
      0 1 [2, 3, 4]
      
      ```

  - **具名元组**

    - 创建具名元组有两个参数：一个是类名，另一个是各个字段的名字。各个字段的名字可以是由数个字符串组成的可迭代对象，或者是由空格分隔开的字段名组成的字符串。

#### 用bisect来管理已经排序的序列

bisect模块主要包含两个主要函数

- bisect

- insort

  两个函数都是利用二分查找算法来在有序序列中查找或插入元素

```python
import bisect
import sys
HAYSTACK=[1,4,5,6,8,12,15,20,21,23,26,29,30]
NEEDELS=[0,1,2,5,8,10,22,23,29,30,31]
ROW_FMT='{0:2d} @ {1:2d}    {2}{0:<2d}'
def demo(bisect_fn):
    for needle in reversed(NEEDELS):
        position=bisect_fn(HAYSTACK,needle)
        offset=position *'  |'
        print(ROW_FMT.format(needle,position,offset))
if __name__ == '__main__':
    if sys.argv[-1]=='left':
        bisect_fn=bisect.bisect_left
    else:
        bisect_fn=bisect.bisect
    print('DEMO',bisect_fn.__name__)
    print('haystack ->',' '.join('%2d'%n for n in HAYSTACK))
    demo(bisect_fn)

结果：
DEMO bisect_right
haystack ->  1  4  5  6  8 12 15 20 21 23 26 29 30
31 @ 13      |  |  |  |  |  |  |  |  |  |  |  |  |31
30 @ 13      |  |  |  |  |  |  |  |  |  |  |  |  |30
29 @ 12      |  |  |  |  |  |  |  |  |  |  |  |29
23 @ 10      |  |  |  |  |  |  |  |  |  |23
22 @  9      |  |  |  |  |  |  |  |  |22
10 @  5      |  |  |  |  |10
 8 @  5      |  |  |  |  |8 
 5 @  3      |  |  |5 
 2 @  1      |2 
 1 @  1      |1 
 0 @  0    0 

Process finished with exit code 0

```

#### 数组

我们需要一个只包含数字的列表，那么数组就比列表更加高效。

python不允许在数组存放除指定类型以外的数据。

数组支持所有跟可变序列有关的操作包括.pop,.insert和.extend。另外数组还提供从文件读取和存入文件更快的方法。如.frombytes和.tofile.

 数组是一个固定长度的存储相同数据类型的数据结构，数组中的元素被存储在一段连续的内存空间中。它是最简单的数据结构之一，大多数现代编程语言都内置数组支持。 

#### 字典和集合

##### **哈希表（散列表）**

  哈希表（Hash table，也叫散列表），是根据关键码值(Key value)而直接进行访问的数据结构。也就是说，它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度。\*\*这个映射函数叫做\*\*散列函数\*\*，存放记录的数组叫做散列表。

当时用hash表进行查询的时候，就是再次使用哈希函数将key转化为对应的数组下标，并定位到该空间获取对应的value值，这样就能充分的利用数组的定位性进行数据定位。

**数组的特点是：寻址容易，插入和删除困难；**

**而链表的特点是：寻址困难，插入和删除容易。**

 ***\*Hash就是找到一种数据内容和数据存放地址之间的映射关系\**\**。\**** 

**散列表的查找步骤** 

当存储记录时，通过散列函数计算出记录的散列地址

当查找记录时，我们通过同样的是散列函数计算记录的散列地址，并按此散列地址访问该记录

##### 泛映射类型

collections.abc模块中有Mapping和MutableMapping两个抽象基类。它的作用是为dict和其他的类型定义形式接口。这些抽象基类的主要作用是作为形式化的文档，他们定义了构建一个映射类型所需要的最基本的接口。

可散列的数据类型

 如果一个对象是可散列的数据类型的话，那它应是不可变的。 

```Python
test = (1,2,(3,4))
hash(test)
-2725224101759650258
test1 = (1,2,[3,4])
hash(test1)
Traceback (most recent call last):
  File "<input>", line 1, in <module>
TypeError: unhashable type: 'list'

```

 list等可变对象是不可散列的，因为随着数据的改变他们的哈希值会变化导致进入错误的哈希表。 

##### **鸭子类型**

“当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。”

我们并不关心对象是什么类型，到底是不是鸭子，只关心行为。

比如在python中，有很多file-like的东西，比如StringIO,GzipFile,socket。它们有很多相同的方法，我们把它们当作文件使用。

又比如list.extend()方法中,我们并不关心它的参数是不是list,只要它是可迭代的,所以它的参数可以是list/tuple/dict/字符串/生成器等.
鸭子类型在动态语言中经常使用，非常灵活，使得python不想java那样专门去弄一大堆的设计模式。下面例子用duck typing来实现多态

```python
#coding=utf-8
class Duck:
    def quack(self):
        print "Quaaaaaack!"
 
class Bird:
    def quack(self):
        print "bird imitate duck."
 
class Doge:
    def quack(self):
        print "doge imitate duck."
 
def in_the_forest(duck):
    duck.quack()
 
duck = Duck()
bird = Bird()
doge = Doge()
for x in [duck, bird, doge]:
    in_the_forest(x)

```

### 文本和字节序列

#### 字符

字符串：一个字符串是一个字符序列

- 字符的标识：码位。码位： 字符在字符集中的位置 .
- 字符的具体表述取决于所用的编码。编码是在码位与字节序列之间转化时使用的算法。
  - 把码位转化为字节序列的过程就是编码。把码位转化为字节序列的过程就是解码。
  - 把字节序列变成人类可读的文本字符串就是解码，而把字符串变成用于存储或传输的字节序列就是编码。



各个字节的值可会使用下列三个不同的方式显示。

- 可打印的ASCII范围内的字节（从空格到~）,使用ASCII字符本身。
- 制表符，换行符，回车符，和\对应的字节,使用转义序列\t,\n,\r和\\
- 其他字节的值使用十六进制转义序列（例如,\x00是空字节）

### 文件I/O

linux文件目录结构

 <img src="https://img-blog.csdn.net/2018080620324833?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25hbl9sZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" alt="img" style="zoom:67%;" /> 

##### 系统调用与用编程接口

**系统调用**（System Call）是由操作系统实现提供的所有系统调用所构成的程序接口的集合。是**应用程序与操作系统间的接口与纽带**。 

操作系统的主要功能是为管理硬件资源和为应用程序开发人员提供良好的环境来使应用程序具有良好的兼容性。为了达到这个目的，内核提供一系列具备预定功能的函数，通过系统调用的接口呈现给用户。当用户访问系统调用，系统调用把应用程序的请求传递给内核，调用相应的内核函数完成所需处理，将处理结果返回给应用程序。
  **应用程序编程接口**（API，Application Programming Interface）是一些**预定义的函数**，目的是**提供****应用程序**与开发人员基于软件/硬件得以访问一组例程的能力，而又无需访问源码或理解内部工作原理机制。 

##### 标准IO与文件IO的区别

- linux环境下既可以使用标准I/O，也可以使用文件I/O
  -  文件编程I/O又称为低级磁盘I/O，任何兼容POSI标准的操作系统都支持文件I/O。
  -  标准编程I/O又称为高级磁盘I/O，只要开发环境有标准C库，标准I/O就可以使用。

- 通过文件I/O读写文件时，每次操作都会执行相关**系统调用**。这样的好处是直接读写实际文件，坏处是频繁的系统调用会增加系统开销。标准I/O在文件I/O的基础上封装了缓冲机制，每次先**操作缓冲区**，必要时再访问文件，从而**减少了系统调用的次数**。 
- 文件I/O使用文件描述符打开操作一个文件，可以**访问不同类型的文件**（例如普通文件、设备文件和管道文件等）。而标准I/O使用FILE指针来表示一个打开的文件，通常**只能访问普通文件**。 

##### 文件的读取与操作

open()读取文件：

```python
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)

```

 其中，`mode='r'`表示只读；`mode='w'`表示只写；`mode='a'`表示追加。`mode='r+'`表示可读写，但是文件必须存在，否则报错。 

##### 指针

python**中的不可变对象与可变对象**

- python 中一切皆对象，每个对象至少包含三个数据：引用计数、类型和值。 	

可变对象与不可变对象

-  **不可变对象：int(整形)、str(字符串)、float(浮点型)、tuple(元组)** 
-  **可变对象：dict(字典)、list(列表)、 set(集合）** 

不可变对象

```python
>>> x=1
>>> id(x)
140724658034336
>>> x+=1
>>> x
2
>>> id(x)
140724658034368

```

不可变对象

```Python
>>> l=['a','b']
>>> l
['a', 'b']
>>> id(l)
2198504679104
>>> l[0]='c'
>>> l
['c', 'b']
>>> id(l)
2198504679104

```

 **这意味着在C语言中定义变量时, x 它代表的是一个内存位置**，可以理解为一个空盒子，而关键字 int 就确定了这个盒子的大小，我们可以将值2337放进这个盒子，也可以将2338放进这个盒子，因为它们是 int 型的值。 

 定义一个变量 x：**x = 2337** 

分解为5步：

**1. 创建一个PyObject**

**2. 将PyObject的类型设置为整数型**

**3. 将PyObject的值设置为2337**

**4.创建一个变量（名称）x**

**5.将 x 指向新建的PyObject**

**6.将该PyObject的引用计数加 1**

 <img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9maWxlcy5yZWFscHl0aG9uLmNvbS9tZWRpYS9weV9tZW1vcnkxLjJiNmU1ZjhlNWJjOS5wbmc?x-oss-process=image/format,png" alt="Python In-Memory representation of X (2337)" style="zoom:50%;" /> 

 将x重新赋值：**x = 2338** 

**1. 创建一个新的PyObject**

**2. 将PyObject的类型设置为整数型**

**3. 将PyObject的值设置为2338**

**4.将 x 指向新的PyObject**

**5.将新的PyObject的引用计数加 1**

**6.将旧的PyObject的引用计数减 1**

 <img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9maWxlcy5yZWFscHl0aG9uLmNvbS9tZWRpYS9weV9tZW1vcnkyLjk5YmI0MzJjMzQzMi5wbmc?x-oss-process=image/format,png" alt="Python Name Pointing to new object (2338)" style="zoom:50%;" /> 

 这说明 x 它不是一个空盒子。  我们在Python中不是新建变量，而是新建名称并绑定到变量，所以说Python中的变量和C中的变量的意义不是等价的。  ，如果此处的指针是指C语言中的指针，那么答案是没有，如果这里的指针指的是C语言中的指针思想，那么答案是有。 

##### 数据存储

- ###### **pickle模块**

  - pickle提供了一个简单的持久化功能。可以将对象以文件的形式存放在磁盘上。 

  - 序列化对象，并将结果数据流写入到文件对象中。参数protocol是序列化模式，默认值为0，表示以文本的形式序列化。protocol的值还可以是1或2，表示以二进制的形式序列化。

  - ```python
    pickle.dump(obj, file[, protocol])
    
    ```

    反序列化对象。将文件中的数据解析为一个Python对象 

    ```
    pickle.load(file)
    
    ```

 存储机制都有一个共同点：存储的数据是独立于对这些数据进行操作的对象和程序。这样做的好处是，数据可以作为共享的资源，供其它应用程序使用。缺点是，用这种方式，可以允许其它程序访问对象的数据，这违背了面向对象的封装性原则 — 即对象的数据只能通过这个对象自身的公共（public）接口来访问。 

```python
>>> a1 = 'apple'  
>>> b1 = {1: 'One', 2: 'Two', 3: 'Three'}  
>>> c1 = ['fee', 'fie', 'foe', 'fum']  
>>> f1 = file('temp.pkl', 'wb')  
>>> pickle.dump(a1, f1, True)  
>>> pickle.dump(b1, f1, True)  
>>> pickle.dump(c1, f1, True)  
>>> f1.close()  
>>> f2 = file('temp.pkl', 'rb')  
>>> a2 = pickle.load(f2)  
>>> a2  
'apple'  
>>> b2 = pickle.load(f2)  
>>> b2  
{1: 'One', 2: 'Two', 3: 'Three'}  
>>> c2 = pickle.load(f2)  
>>> c2  
['fee', 'fie', 'foe', 'fum']  
>>> f2.close()  

```

- ###### json模块

  - **json模块的主要功能是将序列化数据从文件里读取出来或者存入文件。**

    -  dump（）是将数据存入文件中 
    -  load（）是用于读取文件 

  - dumps()和loads()是对python对象进行操作 

    -  dumps()是将python对象编码成json字符串
    -  loads()是将json字符串解码成python对象 

  - **json.dumps()和json.dump()的区别** 

    - json.dumps() 是把python对象转换成json对象的一个过程，生成的是字符串。 

    - json.dump() 是把python对象转换成json对象生成一个fp的文件流，和文件相关 

    - ```python
      #coding:gbk
      import json
      
      
      data_dict = {"xioazhang": 18, "xiaoli": 20, "dazhao": 19}
      #    默认转换的json数据是无序的。如果将参数sort_keys改为True,
      #    则会根据key值将数据进行排序。
      json1 = json.dumps(data_dict, sort_keys=True)
      # 默认无序
      json2 = json.dumps(data_dict)
      print(json1)
      print(json2)
      data_str = '{"小张": 18, "小李": 20, "小赵": 19}'
      data_dict = json.loads(data_str)
      print(data_dict)
      data = '{"小张": 18, "小李": 20, "小赵": 19}'
      with open(' data.json', 'w', encoding='utf-8') as f:
          json.dump(data, f)
      # 等同于f.write(json.dumps (data))
      
      with open(' data.json', 'r') as f:
          infos = json.load(f)
          print(infos)
      # infos = json.loads (f.read())#和上面的效果一样
      结果：
      {"dazhao": 19, "xiaoli": 20, "xioazhang": 18}
      {"xioazhang": 18, "xiaoli": 20, "dazhao": 19}
      {'小张': 18, '小李': 20, '小赵': 19}
      {"小张": 18, "小李": 20, "小赵": 19}
      
      
      ```

### Redis

##### NOSQL概述

**单机mysql时代**

- 数据量太大，一个机器放不下
- 数据的索引，一个机器内存也放不下
- 访问量（读写混合），一个服务器受不了

**Memcached(缓存)+mysql+垂直拆分**（读写分离）

网站80%的数据都在读，每次都进行数据库查询的化就很麻烦，为了减轻数据的压力就采用缓存技术来保证数据的效率。
![1660890025452](https://github.com/zxingq/down/raw/main/img/1660890025452.png)

 **分库分表+水平拆分+mysql集群**


本质===数据的读写

早些年的MyISAM:表锁，十分的影响效率！高并发下会出现严重的锁问题

转战Innodb:行锁（相对于表锁就更加的方便）

将不同的业务进行分表形成微服务

**如今最近的年代**

![1660891270479](https://github.com/zxingq/down/raw/main/img/1660891270479.png)



用户的个人信息，社交网络，地理信息。自己产生的数据，日志数据爆发式生长。

nosql这时候就能很好的处理以上情况。

```
NOSQL的特点：

```

解耦：

1.方便扩展（数据之间没有关系，很好扩展）

2.大数据量高性能

数据类型是多样型的（不需要事先设计数据库！随取随用）

传统关系型数据库（RDBMS）和Nosql的区别：

- RDBMS：
  - 结构化组织
  - SQL
  - 数据和关系都存在单独的表中
  - 数据定义语言
  - 严格的一致性
  - 基础的事务

- NOSQL
  - 不仅仅是数据
  - 没有固定的查询语言
  - 键值对存储，列存储，文档存储，图形数据库（社交关系）
  - 最終一致性
  - CAP定理和BASE
  - 高性能，高可用，高扩展

3v和3高

海量，多样，实时

高可用，高并发，高性能

使用：nosql+RDBMS一起提升

演进分析

```python
#1.商品的基本信息
名称，价格，商品信息：关系型数据库解决！（mysql/oracle）
#2.商品的描述，评论（文字比较多）
文档型数据库中（MongguoDB）
#3.图片
分布式文件系统:FastDFS
    -淘吧  TFS
    Gooale GFS
    Hadoop HDFS
    -阿里云 oss
#4.商品的关键字
-搜索引擎  solr elasticsearch
#5.商品热门的波段信息
-内存数据库
redis  Tair,Memache...
#6.商品的交易，外部的支付网站
---三方应用

```

##### NOSQL四大分类

**kv键值对**

- 新浪：redis
- 美团：redis+tair
- 阿里，百度：redis+memechche

**文档型数据库**（bson格式和json格式一样）

- MonggoDB是一个基于分布式文件存储的数据库，C++编写。它是非关系型数据库中功能最丰富，最像关系型数据库的

**列存储数据库**

- Hbase
- 分布式文件系统

**图关系数据库**

比如朋友圈社交网络，广告推荐

对比：

![1660895244207](https://github.com/zxingq/down/raw/main/img/1660895244207.png)

##### Redis概述

 Redis（Remote Dictionary Server )，即远程字典服务 

-  是一个开源的使用ANSI c语言编写、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。 

Redis能干嘛？

- 内存存储，持久化，内存中是断电即失。使用持久化很重要（rdb,aof）
- 效率高，可以用于高速缓存
- 分布订阅系统
- 地图信息分析
- 计时器，计数器



特征

- 持久化
- 集群
- 事务



Redis推荐在linux上面学习

windows上安装

- 默认端口：6379


- 下载连接 https://github.com/tporadowski/redis/releases

  - 解压

  - 双击redis-server.exe启动服务端

  - 双击redis-cli.exe启动客户端连接服务端

  - 在客户端输入 “ping”，出现“PONG”，即证明连接成功
    ————————————————

     <img src="https://img-blog.csdnimg.cn/img_convert/d33f3bf2fbf84a89bd82e3f7edd5d004.png" alt="图片描述" style="zoom:50%;" /> 

**测试性能**

redis-benchmark测试工具

![1660993751684](https://github.com/zxingq/down/raw/main/img/1660993751684.png)

基础知识：

清空当前数据库:flushdb

清空全部数据库的内容：flushall

选择数据库：select 

```python
#Redis是单线程的

```

Redis是基于内存操作，CPU不是Redis的性能瓶颈。

Redis的瓶颈是根据机器的内存于网络带宽，既然可以使用单线程来实现就使用单线程了。

```python
#Redis单线程为什么还这么快？

```

**核心**：Redis是将全部的数据放在内存中的所以说用单线程去操作单线程效率就是最高的。多线程（CPU上下文切换是耗时的操作），对系统内存来说，没有上下文切换效率就是最高的！多次读写都是在一个CPU上，在内存情况下这个就是最佳方案。

##### **Redis的五大基本数据类型**

- Redis可以用作数据库，缓存，消息中间件（MQ）

###### **String**(字符串)

- ```bash
  set key1 v1 #设置值
  get key1 #获得值
  keys *  #获的所有的值
  exists key1 #判断某个key知否存在
  append key1 "hello" #追加字符串，当key1值不存在时，相当于set key
  strlen key1 #获取字符串的长度
  ####################################################################
  
  i++
  set views 0 #设置出事浏览量为0
  get views  #获取当前浏览量
  incr views #自增1 浏览量变为1
  decr views #自减1 浏览量变为0
  incrby views 10 #设置步数为10 即每次浏览量增加10
  decrby views 10 #设置步数为10 即每次浏览量减少10
  ####################################################################
  获取字符串范围
  getrange key1 0 3
  getrange key1 0 -1 #回去全部字符串
  #####################################################################
  替换
  127.0.0.1:6379[1]> set key2 abcdefg
  OK
  127.0.0.1:6379[1]> get key2
  "abcdefg"
  127.0.0.1:6379[1]> setrange key2 1 xx  #替换制定位置开始的字符串
  (integer) 7
  127.0.0.1:6379[1]> get key2
  "axxdefg"
  #####################################################################
  127.0.0.1:6379[1]> setex key3 30 "hello"#设置值30秒后消失
  OK
  127.0.0.1:6379[1]> ttl key3#查询剩余秒数
  (integer) 20
  127.0.0.1:6379[1]> get key3
  "hello"
  127.0.0.1:6379[1]> setnx mykey "redix"#如果不存在值redis则创建值redis
  (integer) 1
  127.0.0.1:6379[1]> keys *#获取值
  1) "key2"
  2) "key1"
  3) "mykey"
  127.0.0.1:6379[1]> ttl key3
  (integer) -2
  127.0.0.1:6379[1]> get mykey
  "redix"
  ####################################################################
  127.0.0.1:6379[1]> mset k1 v1 k2 v2 k3 v3#同时设置多个值
  OK
  127.0.0.1:6379[1]> keys *
  1) "k3"
  2) "k2"
  3) "k1"
  127.0.0.1:6379[1]> mget k1 k2 k3#同时获取多个值
  1) "v1"
  2) "v2"
  3) "v3"
  127.0.0.1:6379[1]> msetnx k1 v1 k4 v4#msetnx 是一个原子性操作，要么一起成功，要么一起失败
  (integer) 0
  127.0.0.1:6379[1]> get key4
  (nil)
  
  ####################################################################
  #这里的key是一个巧妙的设计：user{id}:{filed}
  127.0.0.1:6379[1]> mset user:1:name zhangsan user:1:age 2
  OK
  127.0.0.1:6379[1]> mget user:1:name user:1:age
  1) "zhangsan"
  2) "2"
  127.0.0.1:6379[1]> getset db redis#如果不存在值，则返回nil
  (nil)
  127.0.0.1:6379[1]> get db
  "redis"
  127.0.0.1:6379[1]> getset db mongodb#如果存在值，获取原来的值，并设置新的值
  "redis"
  127.0.0.1:6379[1]> get db
  "mongodb"
  
  
  ```

String类型的使用场景

value除了是我们的字符串还可以是我们的数字！

- 计数器

- 统计多单位的数量

- 粉丝数


###### list（列表）

在redis里面，我们把list玩成，栈队列，阻塞队列

所有的list命令都是用L开头

```python
#lpush 加入
#lpop  删除
#lrem 移除	
127.0.0.1:6379[1]> lpush  list one#将一个值或多个值插入列表的首部（头部--左）
(integer) 1
127.0.0.1:6379[1]> lpush  list two
(integer) 2
127.0.0.1:6379[1]> lpush  list three
(integer) 3
127.0.0.1:6379[1]> lrange list 0 -1
1) "three"
2) "two"
3) "one"
127.0.0.1:6379[1]> lrange list 0 1
1) "three"
2) "two"

127.0.0.1:6379[1]> rpush list right#将一个值或多个值插入到列表的右部
(integer) 4
127.0.0.1:6379[1]> lrange list 0 -1
1) "three"
2) "two"
3) "one"
4) "right"

127.0.0.1:6379[1]> lrem list 2 three
(integer) 1
#############################################################################
#trim将列表进行截断截取指定的长度
127.0.0.1:6379[1]> lrange list 0 -1
1) "one"
2) "right"
#############################################################################
#將具体某个value值插入到指定元素的前面或后面
127.0.0.1:6379> Rpush mylist "hello"
(integer) 1
127.0.0.1:6379> rpush mylist "world"
(integer) 2
127.0.0.1:6379> linsert mylist before "world" "other"
(integer) 3
127.0.0.1:6379> lrange mylist 0 -1
1) "hello"
2) "other"
3) "world"

```

小结：

- list实际上是一个链表，before Node aftre ,lef right 都可以插入值
- key不存在则创建新的链表
- 如果key存在，则新增内容
- 如果移除了所有值，空链表也代表不存在！
- 在两边插入值或改动值，效率最高！中间元素相对来说效率相对要低一些

消息排队！消息队列（Lpush Rpop）,栈（Lpush Lpop）!

###### **set**（集合）

- ```python
  127.0.0.1:6379> sadd myset "hello"#向set集合中添加元素
  (integer) 1
  127.0.0.1:6379> sadd myset "xiaojiu"
  (integer) 1
  127.0.0.1:6379> smembers myset#查询集合中的元素
  1) "hello"
  2) "xiaojiu"
  127.0.0.1:6379> sismember myset hello#判断某个元素知否在集合中
  (integer) 1
  127.0.0.1:6379> scard myset#获取集合中元素的个数
  (integer) 2
  127.0.0.1:6379> srem myset hello#从集合中移除元素hello
  (integer) 1
  127.0.0.1:6379> smembers myset	
  1) "xiaojiu"
  ###########################################################################
  删除指定的key或是随机的key
  127.0.0.1:6379> spop myset#随机删除指定的key 
  "xiaojiu"
  127.0.0.1:6379> smembers myset
  (empty list or set)
  ###########################################################################
  微博，B站共同关注
  数字集合类
  -差集   sdiff
  -交集   sinter  
  -并集   sunion
  127.0.0.1:6379> sadd set1 a
  (integer) 1
  127.0.0.1:6379> sadd set1 b
  (integer) 1
  127.0.0.1:6379> sadd set2 b
  (integer) 1
  127.0.0.1:6379> sdiff set1 set2
  1) "a"
  127.0.0.1:6379> sinter set1 set2#交集  共同好友就可以实现
  1) "b"
  127.0.0.1:6379> sunion set1 set2
  1) "a"
  2) "b"
  
  ```

  

###### Hash(哈希)

Map集合，key-map!这里的值是一个map集合，本质和hash没有太大的区别，本质还是一个很简单的key-value

- ```python
  127.0.0.1:6379> hmset myhash field hello field world #向哈希表中添加元素field代表键 set多个key-value
  OK
  127.0.0.1:6379> hmget myhash field field#获取值
  1) "world"
  2) "world"
  127.0.0.1:6379> hdel myhash field	#删除指定的键对应的值
  (integer) 1
  127.0.0.1:6379>  hlen myhash  	#获取hash的字段长度
  (integer) 2
  127.0.0.1:6379> hkeys myhash	#获取哈希的所有键
  1) "filed"
  2) "filed1"
  127.0.0.1:6379> hvals myhash	#获取哈希所有的值
  1) "hello"
  2) "world"
  ##########################################################################################
  127.0.0.1:6379> hset myhash field3 1#指定增量
  (integer) 1
  127.0.0.1:6379> hset myhash field3 5
  (integer) 0
  127.0.0.1:6379> hset myhash field3 -1
  (integer) 0
  127.0.0.1:6379> hset myhash field4 hello#如果不存在则可以设置
  (integer) 1
  127.0.0.1:6379> hset myhash field4 world#如果存在则不可以设置
  (integer) 0
  
  ```

  



hash应用于做变更数据，尤其是经常变更的数据

String更适合用于字符串的存储

###### Zset(有序集合)

在set的基础上，添加了一个值zset k1 v1  zset score1 v1

- ```python
  127.0.0.1:6379> zadd myset 1 one#添加一个有序元素
  (integer) 1
  127.0.0.1:6379> zadd myset 2 two 3 three
  (integer) 2
  127.0.0.1:6379> zrange myset 0 -1#获取所有的元素
  1) "one"
  2) "two"
  3) "three"
  #############################################################################
  薪资排序
  127.0.0.1:6379> zadd salary 1500 zhangsan#添加用户
  (integer) 0
  127.0.0.1:6379> zadd salary 1700 lisi
  (integer) 1
  127.0.0.1:6379> zadd salary 1300 wangwu
  (integer) 1
  127.0.0.1:6379> ZRANGEBYSCORE salary -inf 1500 withscores#根据薪水将用户从小到大排序
  1) "kuangshen"
  2) "500"
  3) "wangwu"
  4) "1300"
  5) "zhangsan"
  6) "1500"
  ####zrem移出集合中的元素
  127.0.0.1:6379> zrem salary kuangshen
  (integer) 1
  127.0.0.1:6379> zcard salary#获取集合中的元素个数
  (integer) 4
  
  ```

  场景：

  常用于统计班级成绩排行，工资排行

  怕行榜应用实现

  **许多的东西斗依赖于官方文档**

##### 三种特殊数据类型

###### geospatial 地理位置

场景：

- 朋友的定位
- 附近的人
- 打车距离的计算

拥有六个相关的命令

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\1661219377305.png" alt="1661219377305" style="zoom:50%;" />

- ```python
  #geoadd 添加地理位置
  #规则：两级无法直接添加，我们一般会直接下载城市数据直接通过程序一次性导入
  ############################################################################
  有效的经度从-180度到180度，有效的纬度从-85.05112878到85.05112878，当坐标超出范围将返回错误
  #参数key 值()
  127.0.0.1:6379> geoadd chian:city 116.40 39.90 beijing#添加北京的经纬度
  (integer) 1
  127.0.0.1:6379> geoadd chian:city 121.47 31.23 shanghai
  (integer) 1
  127.0.0.1:6379> geoadd chian:city 106.50 29.53 chongqi 114.05 22.52 shenzhen#同时添加重庆的经纬度
  (integer) 2
  127.0.0.1:6379> geoadd chian:city 120.16 30.24 hangzhou 108.96 34.26 xian
  (integer) 2
  127.0.0.1:6379> GEOPOS chian:city beijing
  1) 1) "116.39999896287918091"
     2) "39.90000009167092543"
  127.0.0.1:6379> GEOPOS chian:city beijing chongqi#同时查询北京和重庆的经纬度
  1) 1) "116.39999896287918091"
     2) "39.90000009167092543"
  2) 1) "106.49999767541885376"
     2) "29.52999957900659211"
  ######################################################################
  GEODIST 两人之间的距离
  127.0.0.1:6379> GEODIST chian:city beijing shanghai km
  "1067.3788"    #查询指定两个城市的直线距离
  ######################################################################
  以给定的经纬度，查出指定半径内的元素
  127.0.0.1:6379> GEORADIUS chian:city 110 30 500 km withcoord #查询出经纬度为110 30为中心的500km的城市以及经纬度
  1) 1) "chongqi"
     2) 1) "106.49999767541885376"
        2) "29.52999957900659211"
  2) 1) "xian"
     2) 1) "108.96000176668167114"
        2) "34.25999964418929977"
  ###########################################################################
  GEORADIUSBYMEMBER  #找出定位于指定元素周围的其他元素
  127.0.0.1:6379> GEORADIUSBYMEMBER chian:city beijing 1000 km
  1) "beijing"
  2) "xian"
  
  
  ```

###### Hyperloglog

```bash
什么是基数

```

j基数(不存在的元素)，可以接受误差

网页的UV（一个人访问多次网站，但是还是算作一个人）

传统的方式：set保护用户id，然后就统计set中的元素数量作为判断标准 。      这个方式如果保存大量的用户id，就会比较的麻烦我们的目的是为了计数而不是保护用户id

**优点：**

- 占用的内存是固定的，2^64种不同的元素的技术只需要费12KB的内存。
- 如果从内存角度，Hyperloglog是首选

```bash
127.0.0.1:6379> PFADD mykey1 a b c d e f g h i j k l
(integer) 1
127.0.0.1:6379> PFADD mykey2 v c d s w q a z j
(integer) 1
127.0.0.1:6379> PFCOUNT mykey2
(integer) 9
127.0.0.1:6379> PFMERGE mykey3 mykey1 mykey2  #将mykey1mykey2的数据进行合并，相同的元素计数一次
OK
127.0.0.1:6379> PFCOUNT mykey3#查看并集的数量
(integer) 17

```

**Bitmaps**

```
位存储

```

应用场景：

统计用户信息，活跃，不活跃！登录，未登录！打卡，未打卡！

- ```bash
  127.0.0.1:6379> setbit sign 1 1
  (integer) 0
  127.0.0.1:6379> setbit sign 2 1
  (integer) 0
  127.0.0.1:6379> setbit sign 3 0
  (integer) 0
  127.0.0.1:6379> setbit sign 4 0
  (integer) 0
  127.0.0.1:6379> setbit sign 5 0
  (integer) 0
  127.0.0.1:6379> setbit sign 6 1
  (integer) 0
  127.0.0.1:6379> setbit sign 7 1#添加某天是否打卡
  (integer) 0
  127.0.0.1:6379> GETBIT sign 3 #获取星期三是否打卡
  (integer) 0
  127.0.0.1:6379> GETBIT sign 7
  (integer) 1
  127.0.0.1:6379> bitcount sign#查询一个星期总共的打卡天数
  (integer) 4
  
  ```

##### 事务

Redis事务的本质：一组命令的集合！一个事务中的所有命令都会被序列化！在事务执行过程中会按顺序执行！~

- 一次性，顺序性，拍他性

Redis事务没有隔离级别的概念！

所有命令在事务中，并没有直接被执行！只有发起执行命令的时候才会执行

redis的事务：

- 开启事务（multi）
- 命令入队（）
- 执行事务（）

```bash
执行事务

```

```bash
127.0.0.1:6379> multi#开启事务
OK
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> set k3 v3
QUEUED
127.0.0.1:6379> exec#执行事务
1) OK
2) OK
3) OK

```

```
放弃事务

```

```bash
127.0.0.1:6379> multi
OK
127.0.0.1:6379> set k1 v1
QUEUED
127.0.0.1:6379> set k2 v2
QUEUED
127.0.0.1:6379> set k4 v4
QUEUED
127.0.0.1:6379> DISCARD   #放弃事务
OK
127.0.0.1:6379> get k4
(nil)

```

**异常**：

- 编译型异常（代码有问题！命令有错！）事务中的所有命令都不会执行

  - ```bash
    127.0.0.1:6379> getset key3
    (error) ERR wrong number of arguments for 'getset' command
    
    ```

- 运行时错误（I/O），如果事务队列中存在语法性,那么执行命令的时候，其他命令是可以正常执行的，错误命令抛出异常！

  - ```bash
    127.0.0.1:6379> set k1 "v1"
    OK
    127.0.0.1:6379> multi   #开启事务
    OK
    127.0.0.1:6379> incr k1 #k1代表的值自增1
    QUEUED
    127.0.0.1:6379> set k2 v2
    QUEUED
    127.0.0.1:6379> set k3 v3
    QUEUED
    127.0.0.1:6379> get k3
    QUEUED
    127.0.0.1:6379> exec
    1) (error) ERR value is not an integer or out of range
    2) OK
    3) OK
    4) "v3"
    
    ```

###### 监控

**悲观锁：**

- 很悲观，认为什么时候都会出现问题，无论做什么都会加锁！

**乐观锁：**

- 认为什么时候都不会出现问题，所以不会上锁！更新数据的时候去判断一下，在此期间是否有人修改过这个数据。
- 获取version
- 更新的时候比较version

Redis监听测试

正常执行成功：

- ```bash
  127.0.0.1:6379> set money 100
  OK
  127.0.0.1:6379> set out 0
  OK
  127.0.0.1:6379> watch money#监视money对象
  OK
  127.0.0.1:6379> multi#事务正常结束，数据期间没有发生变动，这个时候就正常执行成功！
  OK
  127.0.0.1:6379> decrby money 20
  QUEUED
  127.0.0.1:6379> incrby out 20
  QUEUED
  127.0.0.1:6379> exec
  1) (integer) 80
  2) (integer) 20
  
  ```



```bash
 我们还要知道当我们的事务正常执行成功之后，我们的这个watch监视就会自动取消掉 
 ##3watch命令 ，可以当做redis的乐观锁操作！

它这个底层原理就是当我们使用watch命令之后，它就会获取这个key的值，然后监视，当我们去执行事务的时候，就会去更新这个值，更新的时候，首先它会去比较现在要更新的这个key值是否和之前获取到的值是一样的，如果一样，则没有任何问题，如果不一样，则代表有问题，执行事务时会失败！


```

##### Jedis





**单条命令保证原子性，但是事务不保证原子性**

## 操作系统

操作系统：（OS）管理和控制计算机硬件和软件资源的计算机程序，任何其他软件都必须在操作系统的支持下才能运行。

<img src="C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220327214410697.png" alt="image-20220327214410697" style="zoom:50%;" />

操作系统作用：

对下控制硬件运行，对上提供软件支持

操作系统的分类

- 桌面(Windows)

- 服务器(Linux)
- 嵌入式(Linux)
- 移动设备操作系统(OS/Android)

操作系统

windows系统：用户群体多

macOS：适合于开发人员

Linux：应用软件少

虚拟机：软件模拟的方式模拟了一个操作系统

![image-20220327220550542](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20220327220550542.png)

Linux内核版本

内核：是系统的心脏，提供操作系统最基本的功能，他负责管理系统的内存，进程，设备驱动程序，文件和网络系统，决定系统的性能和稳定性。

分为：

- 稳定版
- 开发版

### 终端

终端通常是一个软件控制台，在终端中输入指令可以控制电脑的执行内容

快捷键：ctrl+alt+t

终端指令格式   命令 【选项|参数】

（1）man命令：man   ls

- 回车 一行

- 空格 一页

  f  下一屏

  b  上一屏

  q  退出

##### 常用命令--显示文件和目录

1.显示当前路径（目录）：**pwd**

![1649853560928](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\1649853560928.png)

2、以树状形式显示文件内容：tree

3.查看目录下面的文件（以列表的方式）：ls

ls -a：显示当前目录下的所有文件，包括隐藏文件

##### 常用命令--查看文件详细信息

命令：**ls -l**

![1649854782594](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\1649854782594.png)



##### 常用命令--切换工作目录

- **cd ..****返回上一路径**

- **cd**:直接回到家目录(主目录)

- **cd ~**:回到家目录

- **cd  -**:进入上次所在的目录
- **cd .**:当前目录





##### 常见命令--创建文件和文件夹

- mkdir:创建目录，递归创建 添加 -p选项
- touch:创建一个文件名：touch 文件名  创建多个文件 touch 文件1 文件2 .....
- gedit:用来打开一个文件用于在线编译，相当于ConstOS的vim



##### 常见命令---删除文件和文件夹

rm ---->remove

删除文件：rm 文件名

​				-i    以交互模式删除

​				-f 强制删除不提

删除文件夹

- rm -r +文件夹名字（递归删除文件名）

##### 常见命令---拷贝copy

1.拷贝

![1650176913744](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\1650176913744.png)



##### 常用命令---移动

mv-->move

1.移动文件或者文件夹

- mv 源路径   目标路径
  - -i	交互方式进行文件的移动
  - -f 强制覆盖不提示
  - -v 显示移动的过程
- 注意：移动文件夹不需要加 -r 选项

2.重命名文件或文件夹

重命名：在一个目录中进行移动才能进行重命名

mv  旧文件名   新文件名

##### 常用命令---->文件查看

cat 查看或连接文件

1.查看文件

-n   查看文件的时候对每一行进行编号

-b   非空行进行编号

-s 两个以上的空行 ，只显示一行

2.连接文件，把两个文件连接到一起输出



##### 文件和目录

/bin  二进制文件
/home   用户目录
/home/xxx  用户家目录
/etc   系统配置文件目录
/root  超级管理员目录



##### 常用命令-日期指令

cal 查看日历

-3 上月，当前月，下一月

-y 显示一年的日历

-j 以一年中的第xxx天的格式来显示日历



### 网络编程

###### 使用网络的目的

- 能够使用网络能够把多方连接在一起，然后进行数据传输。
- 网络编程：让不同电脑上的软件能够进行数据传输

###### socket网络编程

![1658480881556](https://github.com/zxingq/down/raw/main/img/1658480881556.png)



对于TCP协议传输一定要指定消息的边界（如FFFFF）作为消息的结尾

UPD传输的是完整的数据报，不需要指定边界。

socket是任何一种计算机网络通讯中最基础的内容

**socket**:  Socket是应用层与TCP/IP协议族通信的中间软件抽象层，它是一组接口。在设计模式中，Socket其实就是一个门面模式，它把复杂的TCP/IP协议族隐藏在Socket接口后面，对用户来说，一组简单的接口就是全部，让Socket去组织数据，以符合指定的协议。 

 ![img](https://images.cnblogs.com/cnblogs_com/goodcandle/socket3.jpg) 

 socket模块是针对 服务器端 和 客户端Socket 进行【打开】【读写】【关闭】 

-  先从服务器端说起。服务器端先初始化Socket，然后与端口绑定(bind)，对端口进行监听(listen)，调用accept阻塞，等待客户端连接。在这时如果有个客户端初始化一个Socket，然后连接服务器(connect)，如果连接成功，这时客户端与服务器端的连接就建立了。客户端发送数据请求，服务器端接收请求并处理请求，然后把回应数据发送给客户端，客户端读取数据，最后关闭连接，一次交互结束。 

 网络层的“**ip地址**”可以唯一标识网络中的主机，而传输层的“**协议+端口**”可以唯一标识主机中的应用程序（进程）。这样利用三元组（ip地址，协议，端口）就可以标识网络的进程了 

 **s.bind(address)** ：将套接字绑定到地址。 

 **sk.listen(backlog)** ： 开始监听传入连接。backlog指定在拒绝连接之前，可以挂起的最大连接数量。 

 **sk.setblocking(bool)** ： 是否阻塞（默认True） 

 **sk.accept()** ： 接受连接并返回（conn,address）,其中conn是新的套接字对象，可以用来接收和发送数据。address是连接客户端的地址。 

 **sk.connect(address)** ： 连接到address处的套接字。 

###### 架构

B/S架构:通过浏览器，只需要写网站来实现交互

C/S架构：服务，客户架构。需要编写软件来实现交互。

###### IO多路复用

IO多路复用：io多路复用分为磁盘io和网络io，这里指代网络io。

 I/O多路复用指：通过一种机制，可以监视多个描述符(socket)，一旦某个描述符就绪（一般是读就绪或者写就绪），能够通知程序进行相应的读写操作。 

### 并发编程

一个程序，至少有一个进程，一个进程中至少有一个线程，最终是线程在工作。

###### **GIL锁**

全局解释锁

###### 多线程与多进程

计算密集型：需要警醒计算，大量数据的计算时候-----**多进程** import multiprocessing

io密集型：文件读写，网络文件传输-----**多线程**=》主线程等待子线程

- t.setDaemon:守护线程，必须放在start前面。

 在现实当中，我们有很多办法来提升程序的运行速度，比如说：我可以对某个算法进行优化，但是，这种优化往往比较有限。因此，我们可以采用多线程，多CPU，以及多机器并行等方式。 

```python
import threading
from threading import Lock,Thread
import time,os


'''
                                      python多线程详解
      什么是线程？
      线程也叫轻量级进程，是操作系统能够进行运算调度的最小单位，它被包涵在进程之中，是进程中的实际运作单位。
      线程自己不拥有系统资源，只拥有一点儿在运行中必不可少的资源，但它可与同属一个进程的其他线程共享进程所
      拥有的全部资源。一个线程可以创建和撤销另一个线程，同一个进程中的多个线程之间可以并发执行
'''

'''
    为什么要使用多线程？
    线程在程序中是独立的、并发的执行流。与分隔的进程相比，进程中线程之间的隔离程度要小，它们共享内存、文件句柄
    和其他进程应有的状态。
    因为线程的划分尺度小于进程，使得多线程程序的并发性高。进程在执行过程之中拥有独立的内存单元，而多个线程共享
    内存，从而极大的提升了程序的运行效率。
    线程比进程具有更高的性能，这是由于同一个进程中的线程都有共性，多个线程共享一个进程的虚拟空间。线程的共享环境
    包括进程代码段、进程的共有数据等，利用这些共享的数据，线程之间很容易实现通信。
    操作系统在创建进程时，必须为改进程分配独立的内存空间，并分配大量的相关资源，但创建线程则简单得多。因此，使用多线程
    来实现并发比使用多进程的性能高得要多。
'''

'''
    总结起来，使用多线程编程具有如下几个优点：
    进程之间不能共享内存，但线程之间共享内存非常容易。
    操作系统在创建进程时，需要为该进程重新分配系统资源，但创建线程的代价则小得多。因此使用多线程来实现多任务并发执行比使用多进程的效率高
    python语言内置了多线程功能支持，而不是单纯地作为底层操作系统的调度方式，从而简化了python的多线程编程。
'''


'''
    普通创建方式
'''
# def run(n):
#     print('task',n)
#     time.sleep(1)
#     print('2s')
#     time.sleep(1)
#     print('1s')
#     time.sleep(1)
#     print('0s')
#     time.sleep(1)
#
# if __name__ == '__main__':
#     t1 = threading.Thread(target=run,args=('t1',))     # target是要执行的函数名（不是函数），args是函数对应的参数，以元组的形式存在
#     t2 = threading.Thread(target=run,args=('t2',))
#     t1.start()
#     t2.start()


'''
    自定义线程：继承threading.Thread来定义线程类，其本质是重构Thread类中的run方法
'''
# class MyThread(threading.Thread):
#     def __init__(self,n):
#         super(MyThread,self).__init__()   #重构run函数必须写
#         self.n = n
#
#     def run(self):
#         print('task',self.n)
#         time.sleep(1)
#         print('2s')
#         time.sleep(1)
#         print('1s')
#         time.sleep(1)
#         print('0s')
#         time.sleep(1)
#
# if __name__ == '__main__':
#     t1 = MyThread('t1')
#     t2 = MyThread('t2')
#     t1.start()
#     t2.start()


'''
    守护线程
    下面这个例子，这里使用setDaemon(True)把所有的子线程都变成了主线程的守护线程，
    因此当主线程结束后，子线程也会随之结束，所以当主线程结束后，整个程序就退出了。
    所谓’线程守护’，就是主线程不管该线程的执行情况，只要是其他子线程结束且主线程执行完毕，主线程都会关闭。也就是说:主线程不等待该守护线程的执行完再去关闭。
'''
# def run(n):
#     print('task',n)
#     time.sleep(1)
#     print('3s')
#     time.sleep(1)
#     print('2s')
#     time.sleep(1)
#     print('1s')
#
# if __name__ == '__main__':
#     t=threading.Thread(target=run,args=('t1',))
#     t.setDaemon(True)
#     t.start()
#     print('end')
'''
    通过执行结果可以看出，设置守护线程之后，当主线程结束时，子线程也将立即结束，不再执行
'''

'''
    主线程等待子线程结束
    为了让守护线程执行结束之后，主线程再结束，我们可以使用join方法，让主线程等待子线程执行
'''
# def run(n):
#     print('task',n)
#     time.sleep(2)
#     print('5s')
#     time.sleep(2)
#     print('3s')
#     time.sleep(2)
#     print('1s')
# if __name__ == '__main__':
#     t=threading.Thread(target=run,args=('t1',))
#     t.setDaemon(True)    #把子线程设置为守护线程，必须在start()之前设置
#     t.start()
#     t.join()     #设置主线程等待子线程结束
#     print('end')


'''
    多线程共享全局变量
    线程时进程的执行单元，进程时系统分配资源的最小执行单位，所以在同一个进程中的多线程是共享资源的
'''
# g_num = 100
# def work1():
#     global  g_num
#     for i in range(3):
#         g_num+=1
#     print('in work1 g_num is : %d' % g_num)
#
# def work2():
#     global g_num
#     print('in work2 g_num is : %d' % g_num)
#
# if __name__ == '__main__':
#     t1 = threading.Thread(target=work1)
#     t1.start()
#     time.sleep(1)
#     t2=threading.Thread(target=work2)
#     t2.start()


'''
        由于线程之间是进行随机调度，并且每个线程可能只执行n条执行之后，当多个线程同时修改同一条数据时可能会出现脏数据，
    所以出现了线程锁，即同一时刻允许一个线程执行操作。线程锁用于锁定资源，可以定义多个锁，像下面的代码，当需要独占
    某一个资源时，任何一个锁都可以锁定这个资源，就好比你用不同的锁都可以把这个相同的门锁住一样。
        由于线程之间是进行随机调度的，如果有多个线程同时操作一个对象，如果没有很好地保护该对象，会造成程序结果的不可预期，
    我们因此也称为“线程不安全”。
        为了防止上面情况的发生，就出现了互斥锁（Lock）
'''
# def work():
#     global n
#     lock.acquire()
#     temp = n
#     time.sleep(0.1)
#     n = temp-1
#     lock.release()
#
#
# if __name__ == '__main__':
#     lock = Lock()
#     n = 100
#     l = []
#     for i in range(100):
#         p = Thread(target=work)
#         l.append(p)
#         p.start()
#     for p in l:
#         p.join()


'''
    递归锁：RLcok类的用法和Lock类一模一样，但它支持嵌套，在多个锁没有释放的时候一般会使用RLock类
'''
# def func(lock):
#     global gl_num
#     lock.acquire()
#     gl_num += 1
#     time.sleep(1)
#     print(gl_num)
#     lock.release()
#
#
# if __name__ == '__main__':
#     gl_num = 0
#     lock = threading.RLock()
#     for i in range(10):
#         t = threading.Thread(target=func,args=(lock,))
#         t.start()


'''
    信号量（BoundedSemaphore类）
    互斥锁同时只允许一个线程更改数据，而Semaphore是同时允许一定数量的线程更改数据，比如厕所有3个坑，
    那最多只允许3个人上厕所，后面的人只能等里面有人出来了才能再进去
'''
# def run(n,semaphore):
#     semaphore.acquire()   #加锁
#     time.sleep(3)
#     print('run the thread:%s\n' % n)
#     semaphore.release()    #释放
#
#
# if __name__== '__main__':
#     num=0
#     semaphore = threading.BoundedSemaphore(5)   #最多允许5个线程同时运行
#     for i in range(22):
#         t = threading.Thread(target=run,args=('t-%s' % i,semaphore))
#         t.start()
#     while threading.active_count() !=1:
#         pass
#     else:
#         print('----------all threads done-----------')

'''
    python线程的事件用于主线程控制其他线程的执行，事件是一个简单的线程同步对象，其主要提供以下的几个方法：
        clear将flag设置为 False
        set将flag设置为 True
        is_set判断是否设置了flag
        wait会一直监听flag，如果没有检测到flag就一直处于阻塞状态
    事件处理的机制：全局定义了一个Flag，当Flag的值为False，那么event.wait()就会阻塞，当flag值为True，
    那么event.wait()便不再阻塞
'''
event = threading.Event()
def lighter():
    count = 0
    event.set()         #初始者为绿灯
    while True:
        if 5 < count <=10:
            event.clear()  #红灯，清除标志位
            print("\33[41;lmred light is on...\033[0m]")
        elif count > 10:
            event.set()    #绿灯，设置标志位
            count = 0
        else:
            print('\33[42;lmgreen light is on...\033[0m')

        time.sleep(1)
        count += 1


def car(name):
    while True:
        if event.is_set():     #判断是否设置了标志位
            print('[%s] running.....'%name)
            time.sleep(1)
        else:
            print('[%s] sees red light,waiting...'%name)
            event.wait()
            print('[%s] green light is on,start going...'%name)


# startTime = time.time()
light = threading.Thread(target=lighter,)
light.start()

car = threading.Thread(target=car,args=('MINT',))
car.start()
endTime = time.time()
# print('用时：',endTime-startTime)

'''
                           GIL  全局解释器
        在非python环境中，单核情况下，同时只能有一个任务执行。多核时可以支持多个线程同时执行。但是在python中，无论有多少个核
        同时只能执行一个线程。究其原因，这就是由于GIL的存在导致的。
        GIL的全程是全局解释器，来源是python设计之初的考虑，为了数据安全所做的决定。某个线程想要执行，必须先拿到GIL，我们可以
        把GIL看做是“通行证”，并且在一个python进程之中，GIL只有一个。拿不到线程的通行证，并且在一个python进程中，GIL只有一个，
        拿不到通行证的线程，就不允许进入CPU执行。GIL只在cpython中才有，因为cpython调用的是c语言的原生线程，所以他不能直接操
        作cpu，而只能利用GIL保证同一时间只能有一个线程拿到数据。而在pypy和jpython中是没有GIL的
        python在使用多线程的时候，调用的是c语言的原生过程。
'''
'''
                            python针对不同类型的代码执行效率也是不同的
        1、CPU密集型代码（各种循环处理、计算等），在这种情况下，由于计算工作多，ticks技术很快就会达到阀值，然后出发GIL的
        释放与再竞争（多个线程来回切换当然是需要消耗资源的），所以python下的多线程对CPU密集型代码并不友好。
        2、IO密集型代码（文件处理、网络爬虫等设计文件读写操作），多线程能够有效提升效率（单线程下有IO操作会进行IO等待，
        造成不必要的时间浪费，而开启多线程能在线程A等待时，自动切换到线程B，可以不浪费CPU的资源，从而能提升程序的执行
        效率）。所以python的多线程对IO密集型代码比较友好。
'''
'''
    主要要看任务的类型，我们把任务分为I/O密集型和计算密集型，而多线程在切换中又分为I/O切换和时间切换。如果任务属于是I/O密集型，
    若不采用多线程，我们在进行I/O操作时，势必要等待前面一个I/O任务完成后面的I/O任务才能进行，在这个等待的过程中，CPU处于等待
    状态，这时如果采用多线程的话，刚好可以切换到进行另一个I/O任务。这样就刚好可以充分利用CPU避免CPU处于闲置状态，提高效率。但是
    如果多线程任务都是计算型，CPU会一直在进行工作，直到一定的时间后采取多线程时间切换的方式进行切换线程，此时CPU一直处于工作状态，
    此种情况下并不能提高性能，相反在切换多线程任务时，可能还会造成时间和资源的浪费，导致效能下降。这就是造成上面两种多线程结果不能的解释。
结论:I/O密集型任务，建议采取多线程，还可以采用多进程+协程的方式(例如:爬虫多采用多线程处理爬取的数据)；对于计算密集型任务，python此时就不适用了。
'''



```

### 正则表达式

正则表达式推荐使用网站

- http://regex101.com

最基础的语法

**限定符**

![](https://github.com/zxingq/down/raw/main/img/image-20220325220057299.png)

**\d:匹配数字**

**\w:匹配字母，数字，下划线**

**\s：匹配空白**

**\b；匹配单词的边界**

\D:匹配所有的非数字

\w:匹配所有的非字母，数字，下划线

\S:匹配所有非空白

^:匹配开始

$:匹配结束

.  :匹配任意字符，除了换行符

| *    | 匹配前面的子表达式零次或多次。要匹配 * 字符，请使用 \*。  |
| ---- | --------------------------------------------------------- |
| .    | 匹配除换行符 \n 之外的任何单字符。要匹配 . ，请使用 \. 。 |

？:可选字符，可以出现也可以不出现，

| ?    | 匹配前面的子表达式零次或一次，或指明一个非贪婪限定符。要匹配 ? 字符，请使用 \?。 |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

{}：表示数字的个数

()：用于分组

### 匿名函数

什么是匿名函数：定义函数时，不指定函数名的函数
为什么要使用匿名函数：节约内存；避免产生全局变量，造成全局污染。
匿名函数两种情况：
（1）绝大多数回调函数，都使用匿名函数（节约内存）
1）原因：匿名函数用完之后，就会自动释放
（2）匿名函数自调（避免产生全局变量，造成全局污染）
1）什么是匿名函数自调：定义一个匿名函数后，立刻调用该函数执行，调用后立刻释放

```python
def sum_func(a, b, c):
    return a + b + c
 
 
sum_lambda = lambda a, b, c: a + b + c
 
print(sum_func(1, 100, 10000))
print(sum_lambda(1, 100, 10000))
结果：
10101
10101

# 无参数
lambda_a = lambda: 100
print(lambda_a())
 
# 一个参数
lambda_b = lambda num: num * 10
print(lambda_b(5))
 
# 多个参数
lambda_c = lambda a, b, c, d: a + b + c + d
print(lambda_c(1, 2, 3, 4))
 
# 表达式分支
lambda_d = lambda x: x if x % 2 == 0 else x + 1
print(lambda_d(6))
print(lambda_d(7))
结果：
100
50
10
6
8

def sub_func(a, b, func):
    print('a =', a)
    print('b =', b)
    print('a - b =', func(a, b))
 
 
sub_func(100, 1, lambda a, b: a - b)

结果：
a = 100
b = 1
a - b = 99

member_list = [
    {"name": "风清扬", "age": 99, "power": 10000},
    {"name": "无崖子", "age": 89, "power": 9000},
    {"name": "王重阳", "age": 120, "power": 8000}
]
new_list = sorted(member_list, key=lambda dict_: dict_["power"])
print(new_list)
ber_list))
print(num_sum)

结果：
[{'name': '王重阳', 'age': 120, 'power': 8000}, {'name': '无崖子', 'age': 89, 'power': 9000}, {'name': '风清扬', 'age': 99, 'power': 10000}]

```

