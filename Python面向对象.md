* [1.面向对象](#1面向对象)
* [2.什么是类和类变量?](#2什么是类和类变量)
* [3.实例和实例化以及实例变量](#3实例和实例化以及实例变量)
* [4.数据成员](#4数据成员)
* [5.方法和静态方法以及类方法](#5方法和静态方法以及类方法)
* [6.什么是方法重写](#6什么是方法重写)
* [7. _ _ <strong>init</strong> _ _](#7-_-_-init-_-_)
* [8.self](#8self)
* [9.类的初始化：new() 和 init()](#9类的初始化new-和-init)
* [10.<strong>@classmethon</strong>](#10classmethon)
* [11.<strong>@staticmethod</strong>](#11staticmethod)
* [12.设计的一个面向对象程序设计的完整示例。](#12设计的一个面向对象程序设计的完整示例)
* [13.私有属性](#13私有属性)
* [14.类的继承](#14类的继承)
* [15.多继承](#15多继承)


#### 1.面向对象

**抽象**：提取现实世界中某事物的关键特性，为该事物构建模型的过程。对同一事物在不同的需求下，需要提取的特性可能不一样。得到的抽象模型中一般包含：属性（数据）和操作（行为）。这个抽象模型我们称之为类。对类进行实例化得到对象。

**封装**：封装可以使类具有独立性和隔离性；保证类的高内聚。只暴露给类外部或者子类必须的属性和操作。类封装的实现依赖类的修饰符（public、protected和private等）

**继承**：对现有类的一种复用机制。一个类如果继承现有的类，则这个类将拥有被继承类的所有非私有特性（属性和操作）。这里指的继承包含：类的继承和接口的实现。

**多态**：多态是在继承的基础上实现的。多态的三个要素：继承、重写和父类引用指向子类对象。父类引用指向不同的子类对象时，调用相同的方法，呈现出不同的行为；就是类多态特性。多态可以分成编译时多态和运行时多态。

#### 2.什么是类和类变量?

用来描述具有相同属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。其中的对象被称作类的实例。

类变量：类变量是所有实例公有的变量。类变量定义在类中，但在方法体之外。

#### 3.实例和实例化以及实例变量

实例：也称对象。通过类定义的初始化方法，赋予具体的值，成为一个”有血有肉的实体”。

实例化：创建类的实例的过程或操作。

实例变量：定义在实例中的变量，只作用于当前实例。

#### 4.数据成员

类变量、实例变量、方法、类方法、静态方法和属性等的统称。

#### 5.方法和静态方法以及类方法

方法：类中定义的函数。

静态方法：不需要实例化就可以由类执行的方法

类方法：类方法是将类本身作为对象进行操作的方法。

#### 6.什么是方法重写

如果从父类继承的方法不能满足子类的需求，可以对父类的方法进行改写，这个过程也称override。

#### 7. _ _ __init__ _ _

可以成为类的实例对象的构造函数，每次通过类创建一个该类的对象是调用此函数，所以其下的以sefl.前缀的变量是每个创建好了的实例(化)对象的所独有的。换句话说，有多少个类的对象内存里就有多少份这个实例对象变量存在。就像生产了多少小汽车就有多少个方向盘似的。

#### 8.self

代表运行时的类的实例对象本身，一般在类的内部设计时出现，在程序里使用对象编程时不用self。在实例对象的成员函数里以self.前缀的变量是实例对象的成员变量，没有self.的变量是本方法函数的局部变量。

#### 9.类的初始化：new() 和 init()

new()方法用来实例化最终的类对象，在类创建之前被调用，它在类的主体被执行完后开始执行。

init()方法是在类被创建之后被调用，用来执行其他的一些输出化工作

当我们构造元类的时候，通常只需要定一个init()或new()方法，但不是两个都定义。但是，如果需要接受其他的关键词参数的话，这两个方法就要同时提供，并且都要提供对应的参数签名。

#### 10.**@classmethon**

这个关键字是修饰器，修饰也是说下面的函数是类的方法函数而不是类的对象的方法函数。

#### 11.**@staticmethod** 

这个也是修饰器，说明接下来的函数是一个静态函数，和实例对象的成员函数、类函数的区别主要在第一个形参，既无self又无cls。可以被类或对象直接调用。 差不多解释完了，下面来看一个具体的类的实例程序。

#### 12.设计的一个面向对象程序设计的完整示例。

```
# coding:utf-8
class Horse(object):
    variety = "大宛马"
    def __init__(self, name = "green", height = 0.5, length = 1.3, sex = "male"):       
        # self.name是成员变量，name是形参、局部变量
        self.name = name 
        self.height = height
        self.length = length
        self.sex = sex
        print "A baby horse is born called", self.name

    def print_info(self):
        print self.name, self.height, self.length, self.sex, Horse.variety#,Horse.address
        Horse.print_variety() # 在对象方法里通过类调用类方法，避免
        Horse().print_ci(200, 100)# 对象调用静态方法
        Horse.print_ci(200, 100) # 类调用静态方法

    @staticmethod
    def print_ci(x, y):
        print x, y

    @classmethod
    def pp(cls):
        # 类使用类变量
        print cls.variety, Horse.variety, cls.address
        #cls.print_variety()    
        print Horse().name  # 对象使用对象的成员变量
    @classmethod
    def print_variety(cls):
        cls.address = "xi'an"
        print "type", type(cls.address)
        print cls.variety, Horse.variety, cls.address 
        Horse.pp()# 类调用类方法
        Horse().print_ci(100, 100)# 对象调用静态方法

a = Horse("xiaoxuanfeng")
b = Horse("pilihuo", sex = "female")
a.print_info()
b.print_info()
Horse.print_variety()
print "*" * 20
Horse.pp() # 类调用类方法
Horse.print_ci(12, 23)# 类外类调用静态方法
a.print_ci(23, 31) # 类外对象调用静态方法
```

#### 13.私有属性

变量和函数

- 定义私有变量

```
class aa(object):
    def __init__(self, w, v):
        self.x = w
        self.__y = v
    def p(self):
        print "  x", self.x
        print "__y", self.__y
ai = aa(12, 13)
ai.p()
```

程序的执行结果：

```
  x 12
__y 13
```

- 定义私有函数,不能在类的外部调用。

```
class aa(object):
    def __init__(self, w, v):
        self.x = w
        self.__y = v
    def p(self):
        print "  x", self.x
        print "__y", self.__y
        self.__q()
    def __q(self):
        print "private method of class aa"
ai = aa(12, 13)
ai.p()
#aa.__q()
#ai.__q()
#ai._aa__q()
```

程序的执行结果：

```
  x 12
__y 13
private method of class aa
```

`__q`函数是类aa的私有函数，可以在类内部使用，但不能在类之外使用。

#### 14.类的继承

假如已经有几个类，而类与类之间有共同的变量属性和函数属性，那就可以把这几个变量属性和函数属性提取出来作为基类的属性。而特殊的变量属性和函数属性，则在本类中定义，这样只需要继承这个基类，就可以访问基类的变量属性和函数属性。可以提高代码的可扩展性。通过继承可以快速扩展和实现函数的多样性

举例:

```
class aa(object):
    def __init__(self, v):
        self.x = v
        self.__pa = 10
    def p(self):
        print "class aa's instance method"
    def info(self):
        print "info of aa instance"
class cc(aa):
    def __init__(self, v):
        self.z = v
        self__pc = 10
    def p(self):
        print "class cc's instance method"
a = aa(10)
c = cc(30)
a.p()
a.info()
c.p()
c.info()
```

程序执行结果：

```
class aa's instance method
info of aa instance
class cc's instance method
info of aa instance
```

#### 15.多继承

Python的类允许可以有多个父类，从左至右有顺序要求，这和后续搜索查找数据和函数有关系。

```
  class 子类(父类1， 父类2， ...)
```

多继承时子类的父类间和子类要满足人类的**伦理规则**。

举例:

```
class aa(object):
    def __init__(self, v):
        self.x = v
    def px(self):
        print self.x

class bb(object):
    def __init__(self, v):
        self.y = v
    def py(self):
        print self.y

class cc(aa, bb):
    def __init__(self, v, v1 = 100):
        print "cc"
        super(cc, self).__init__(v1)
        #aa.__init__(self, v1)
        #bb.__init__(self, v1)
        print "ccx"
        self.z = v
    def pz(self):
        print self.z

a = aa(12)
a.px()
b = bb(13)
b.py()
c = cc(14)
print dir(c)
c.pz()
```

程序的执行结果：

```
12
13
cc
ccx
['__class__', ..., '__weakref__', 'px', 'py', 'pz', 'x', 'z']
14
```

#### 参考链接

https://blog.csdn.net/weixin_39628063/article/details/111455821

http://liao.cpython.org/27classobject/

https://blog.csdn.net/weixin_35390379/article/details/112022047

