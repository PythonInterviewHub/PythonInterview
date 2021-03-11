* [1.写函数，接收两个数字参数，返回最大值](#1写函数接收两个数字参数返回最大值)
* [2.写函数，获取传入列表的所有奇数位索引对应的元素，并将其作为新列表返回。](#2写函数获取传入列表的所有奇数位索引对应的元素并将其作为新列表返回)
* [3.写函数，检查传入的字符串是否含有空字符串，返回结果，包含空字符串返回True，不包含返回False](#3写函数检查传入的字符串是否含有空字符串返回结果包含空字符串返回true不包含返回false)
* [4.定义一个函数,实现两个数四则运算,要注意有3个参数,分别是运算符和两个运算的数字.](#4定义一个函数实现两个数四则运算要注意有3个参数分别是运算符和两个运算的数字)
* [5.filter、map、reduce 的作用?](#5filtermapreduce-的作用)
* [6.请实现一个装饰器,通过一次调用使函数重复执行5次。](#6请实现一个装饰器通过一次调用使函数重复执行5次)
* [7.如何判断一个值是函数还是方法?](#7如何判断一个值是函数还是方法)
* [8.可更改(mutable)与不可更改(immutable)对象](#8可更改mutable与不可更改immutable对象)
* [9.匿名函数](#9匿名函数)
* [10.变量作用域](#10变量作用域)
* [11.模块与包](#11模块与包)
* [12.模块的使用](#12模块的使用)
* [13.包的使用](#13包的使用)
* [14.File（文件)方法  python3](#14file文件方法--python3)
* [open() 方法](#open-方法)
* [15.异常处理的定义](#15异常处理的定义)
* [16.异常处理的意义](#16异常处理的意义)
* [17.常见的异常](#17常见的异常)
* [18.如何进行异常处理](#18如何进行异常处理)

#### 1.写函数，接收两个数字参数，返回最大值

```
def res_max(number1,number2):
    l1 = []
    l1.append(number1)
    l1.append(number2)
    return max(l1)
```

#### 2.写函数，获取传入列表的所有奇数位索引对应的元素，并将其作为新列表返回。

```
def getnewlist(mylist):
　　list1=[];
　　for i in range(0,len(mylist)):
　　　　if i%2!=0:
　　　　list1.append(mylist[i])
　　return list1
```

#### 3.写函数，检查传入的字符串是否含有空字符串，返回结果，包含空字符串返回True，不包含返回False

```
def str_spack(string):
    if string.find(' '):
        return True
    else:
        return False
```

#### 4.定义一个函数,实现两个数四则运算,要注意有3个参数,分别是运算符和两个运算的数字.

```
def arithmetic(number1, number2, symbol):
   
    if symbol == '+':
        s = number1 + number2
    elif symbol == '-':
        s = number1 - number2
    elif symbol == '*':
        s = number1 * number2
    elif symbol == '/':
        s = number1 / number2
    return s

方法二：
def getresult(num1,fh,num2):
    str1=str(num1)+fh+str(num2)
    return eval(str1)
print(getresult(10,'*',20))
```

#### 5.filter、map、reduce 的作用?

1. filter---过滤条件用的
2. map--将内容里的元素 逐个处理
3. reduce--用于做累计算的

#### 6.请实现一个装饰器,通过一次调用使函数重复执行5次。

```
import  time
def wrapper(func):
    def inner(*args,**kwargs):
        for i in range(5):
            time.sleep(0.5)
            func(*args,**kwargs)
    return inner
@wrapper
def func():
    print('a')

func()
```



#### 7.如何判断一个值是函数还是方法?

用type()来判断，如果是method为方法，如果是function则是函数。

括号中写入变量名,,不要有括号什么别的符号之类的

#### 8.可更改(mutable)与不可更改(immutable)对象

在 python 中，strings, tuples, 和 numbers 是不可更改的对象，而 list,dict 等则是可以修改的对象。

- **不可变类型：**变量赋值 **a=5** 后再赋值 **a=10**，这里实际是新生成一个 int 值对象 10，再让 a 指向它，而 5 被丢弃，不是改变a的值，相当于新生成了a。
- **可变类型：**变量赋值 **la=[1,2,3,4]** 后再赋值 **la[2]=5** 则是将 list la 的第三个元素值更改，本身la没有动，只是其内部的一部分值被修改了。

python 函数的参数传递：

- **不可变类型：**类似 c++ 的值传递，如 整数、字符串、元组。如fun（a），传递的只是a的值，没有影响a对象本身。比如在 fun（a）内部修改 a 的值，只是修改另一个复制的对象，不会影响 a 本身。
- **可变类型：**类似 c++ 的引用传递，如 列表，字典。如 fun（la），则是将 la 真正的传过去，修改后fun外部的la也会受影响

python 中一切都是对象，严格意义我们不能说值传递还是引用传递，我们应该说传不可变对象和传可变对象。

#### 9.匿名函数

python 使用 lambda 来创建匿名函数。

- lambda只是一个表达式，函数体比def简单很多。
- lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
- lambda函数拥有自己的命名空间，且不能访问自有参数列表之外或全局命名空间里的参数。
- 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

#### 10.变量作用域

一个程序的所有的变量并不是在哪个位置都可以访问的。访问权限决定于这个变量是在哪里赋值的。

变量的作用域决定了在哪一部分程序你可以访问哪个特定的变量名称。两种最基本的变量作用域如下：

- 全局变量
- 局部变量

#### 11.模块与包

模块首先是一个含有源代码的文件在Python里以.py结尾，文件里可以有函数的定义、变量的定义或者对象(类的实例化)的定义等等内容。如果一个项目的代码量较大，函数较多，最好把一个文件分为多个文件来管理，这样总程序脉络清晰易于维护和团队分工协作，这就是Python里存在模块的意义所在。模块名就是文件名(不含.py)，例如假设有一个模块：xopowo.py那么模块名为xopowo。

但当一个项目的模块文件不断的增多，为了更好地管理项目，通常将功能相近相关的模块放在同一个目录下，这就是包，故包从物理结构上看对应于一个目录，一个特殊要求，包目录下必有一个空的__init__.py文件，这是包区分普通目录的标签或者说是标志。包下可以又有包称为子包，子包也是一个目录，子包的目录下也得有一个空的__init__.py文件。这样就构成了分级或者说分层的项目管理体系。

#### 12.模块的使用

模块，可是Python自带的、而外安装的或者开发者自己写的，在一个文件里使用模块很简单用import即可，import有点像C语言的include。

以Python2的内建模块[datetime](https://docs.python.org/2.7/library/datetime.html)为例，讲解一下模块的基本使用。

在新程序里使用datetime模块可以有两种方式：方式一是把模块引入，而模块里的函数的使用需要用点运算的方式来来使用。

```
import datetime
birthday = datetime.date(2011,7,23)
print birthday
```

而文件引用模块里某函数还有另外一种方式就是用from import来直接引入某模块里的某函数，即方式二。

```
from datetime import date,time
birthday = date(2011,7,23)
print birthday
```

使用方式二文件只能用import后列出的函数，而模块datetime里的其他函数无法在本文件里使用，所以一种特殊的写法如下：

```
from datetime import *
```

也就是说datetime里的所有函数在本程序里均可使用。

#### 13.包的使用

包，实际是更大规模的以目录形式存在的模块集合，包可以含子包，包区别于目录是包的目录下有一个空的__init__.py文件。包和模块一样有Python自带的包，也可以通过工具安装一些包，例如numpy就是数据科学领域比较常用的一个包，需额外安装，当然也可以自己开发一些包。

以Python2自带的包[multiprocessing](https://docs.python.org/2.7/library/multiprocessing.html)为例，其下还有子包[dummy](https://docs.python.org/2.7/library/multiprocessing.html#module-multiprocessing.dummy)。

```
liao@liao:/usr/lib/python2.7/multiprocessing$ ls
connection.py   forking.py   heap.pyc      managers.py   pool.pyc     queues.py     reduction.pyc     synchronize.py 
connection.pyc  forking.pyc  __init__.py   managers.pyc  process.py   queues.pyc    sharedctypes.py   synchronize.pyc
dummy           heap.py      __init__.pyc  pool.py       process.pyc  reduction.py  sharedctypes.pyc  util.py
liao@liao:/usr/lib/python2.7/multiprocessing$ ls dummy/
connection.py  connection.pyc  __init__.py  __init__.pyc
liao@liao:/usr/lib/python2.7/multiprocessing$ 
```

multiprocess包下有很多的模块，例如process模块，那么可以在一个示例程序里使用包multiprocess里的process模块。

```
#coding:utf-8
from multiprocessing import Process
import os  
def test(name):
    print "Process ID： %s" % (os.getpid())  
    print "Parent Process ID： %s" % (os.getppid())  
if __name__ == "__main__": 
    proc = Process(target=test, args=('nmask',))  
    proc.start()  
    proc.join()
```

需要解释的是`from multiprocessing import Process`是从包multiprocess里引入Process， 但Process类定义在process.py文件里，包含Process类的process.py文件是在multiprocessing目录下的，故是multiprocessing包里的一个模块。通过Python交互环境可以查明这一点。

```
>>> from multiprocessing import Process
>>> help(Process)
Help on class Process in module multiprocessing.process:

class Process(__builtin__.object)
```

代码`from multiprocessing import Process`也可以这样去写`from multiprocessing.process import Process`这样写既写了包名又写了模块名即`包.模块`，其实在Python里一般还是直接用包名(偷懒)，而少有既写包又写模块的。

#### 14.File（文件)方法  python3

### open() 方法

Python open() 方法用于打开一个文件，并返回文件对象，在对文件进行处理过程都需要使用到这个函数，如果该文件无法被打开，会抛出 OSError。

**注意：**使用 open() 方法一定要保证关闭文件对象，即调用 close() 方法。

open() 函数常用形式是接收两个参数：文件名(file)和模式(mode)。

```
open(file, mode='r')
```

完整的语法格式为：

```
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
```

参数说明:

- file: 必需，文件路径（相对或者绝对路径）。
- mode: 可选，文件打开模式
- buffering: 设置缓冲
- encoding: 一般使用utf8
- errors: 报错级别
- newline: 区分换行符
- closefd: 传入的file参数类型
- opener: 设置自定义开启器，开启器的返回值必须是一个打开的文件描述符。

#### 15.异常处理的定义

python解释器检测到错误，触发异常（也允许程序员自己触发异常）

程序员编写特定的代码，专门用来捕捉这个异常（这段代码与程序逻辑无关，与异常处理有关）

如果捕捉成功则进入另外一个处理分支，执行你为其定制的逻辑，使程序不会崩溃，这就是异常处理

#### 16.异常处理的意义

python解析器去执行程序，检测到了一个错误时，触发异常，异常触发后且没被处理的情况下，程序就在当前异常处终止，后面的代码不会运行，所以你必须提供一种异常处理机制来增强你程序的健壮性与容错性 

#### 17.常见的异常

```
AttributeError 试图访问一个对象没有的属性，比如foo.x，但是foo没有属性x
IOError 输入/输出异常；基本上是无法打开文件
ImportError 无法引入模块或包；基本上是路径问题或名称错误
IndentationError 语法错误（的子类） ；代码没有正确对齐
IndexError 下标索引超出序列边界，比如当x只有三个元素，却试图访问x[5]
KeyError 试图访问字典里不存在的键
KeyboardInterrupt Ctrl+C被按下
NameError 尝试访问一个没有申明的变量
SyntaxError Python代码非法，代码不能编译(个人认为这是语法错误，写错了）
TypeError 传入对象类型与要求的不符合
UnboundLocalError 试图访问一个还未被设置的局部变量，基本上是由于另有一个同名的全局变量，导致你以为正在访问它
ValueError 传入一个调用者不期望的值，即使值的类型是正确的
```

#### 18.如何进行异常处理

- 使用if判断式

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
num1=input('>>: ') #输入一个字符串试试
if num1.isdigit():
    int(num1) #我们的正统程序放到了这里,其余的都属于异常处理范畴
elif num1.isspace():
    print('输入的是空格,就执行我这里的逻辑')
elif len(num1) == 0:
    print('输入的是空,就执行我这里的逻辑')
else:
    print('其他情情况,执行我这里的逻辑')

#第二段代码
# num2=input('>>: ') #输入一个字符串试试
# int(num2)

#第三段代码
# num3=input('>>: ') #输入一个字符串试试
# int(num3)
```

问题一：
使用if的方式我们只为第一段代码加上了异常处理，针对第二段代码，你得重新写一堆if，elif等
而这些if，跟你的代码逻辑并无关系,可读性差

问题二：
第一段代码和第二段代码实际上是同一种异常，都是ValueError,相同的错误按理说只处理一次就可以了，而用if，由于这二者if的条件不同，这只能逼着你重新写一个新的if来处理第二段代码的异常
第三段也一样

- try...except

语法：

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
try:
<语句>        #运行别的代码
except <异常类型>：
<语句>        #如果在try部份引发了'name'异常
except <异常类型> as <数据>:
<语句>        #如果引发了'name'异常，获得附加的数据
else:
<语句>        #如果没有异常发生
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

 

注：

python2 和 3 处理 except 子句的语法有点不同，需要注意；

　　　　　　　　Python2  

```
try:
    print (1/0)
except ZeroDivisionError, err:　　　　　　# , 加原因参数名称 
    print ('Exception: ', err)
```

　　　　　　　　Python3  

```
try:
    print (1/0)
except ZeroDivisionError as err:        # as 加原因参数名称
    print ('Exception: ', err)
```

 例

```
try:
    fh = open("testfile", "w")
    fh.write("这是一个测试文件，用于测试异常!!")
except IOError:
    print("Error: 没有找到文件或读取文件失败")
else:
    print("内容写入文件成功")
    fh.close()
```



输出

```
内容写入文件成功
```

注：

异常类只能用来处理指定的异常情况，如果非指定异常则无法处理。（**异常是由程序的错误引起的，语法上的错误跟异常处理无关，必须在程序运行前就修正）**

```
# 未捕获到异常，程序直接报错

s1 = 'hello'
try:
    int(s1)
except IndexError as e:
    print e
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

输出

```
  File "/Users/hexin/PycharmProjects/py3/day9/1.py", line 11
    print e
          ^
SyntaxError: Missing parentheses in call to 'print'
```

 

- 多分支

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
try:
    msg=input('>>:')
    int(msg) #ValueError
    #
    # print(x) #NameError
    # #
    # # l=[1,2]
    # # l[10] #IndexError
    #
    # 1+'asdfsadfasdf' #TypeError

except ValueError as e:
    print(e)
except NameError:
    print('NameError')
except KeyError as e:
    print(e)
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
>>:gg
invalid literal for int() with base 10: 'gg'
```

 

- 万能异常

在python的异常中，有一个万能异常：Exception，他可以捕获任意异常

```
s1 = 'hello'
try:
    int(s1)
except Exception as e:
    '丢弃或者执行其他逻辑'
    print(e)
```

输出

```
invalid literal for int() with base 10: 'hello'
```

 

- try-finally 语句

try-finally 语句无论是否发生异常都将执行最后的代码。

![复制代码](https://common.cnblogs.com/images/copycode.gif)

```
s1 = 'hello'
try:
    int(s1)
except IndexError as e:
    print(e)
except KeyError as e:
    print(e)
except ValueError as e:
    print(e)
#except Exception as e:
#    print(e)
else:
    print('try内代码块没有异常则执行我')
finally:
    print('无论异常与否,都会执行该模块,通常是进行清理工作')
```

![复制代码](https://common.cnblogs.com/images/copycode.gif)

输出

```
invalid literal for int() with base 10: 'hello'
无论异常与否,都会执行该模块,通常是进行清理工作
```

 

- raise主动触发异常

我们可以使用raise语句自己触发异常

raise语法格式如下：

```
raise [Exception [, args [, traceback]]]
```

语句中Exception是异常的类型（例如，NameError）参数是一个异常参数值。该参数是可选的，如果不提供，异常的参数是"None"。

最后一个参数是可选的（在实践中很少使用），如果存在，是跟踪异常对象。

```
try:
    raise TypeError('类型错误')
except Exception as e:
    print(e)
```

输出

```
类型错误
```

 

- 自定义异常

```
class hexinException(BaseException):
    def __init__(self,msg):
        self.msg=msg
    def __str__(self):
        return self.msg

try:
    raise hexinException('类型错误')
except hexinException as e:
    print(e)
```



输出

```
类型错误
```


 

#### 参考链接

https://www.cnblogs.com/puti306/p/12080526.html

https://www.cnblogs.com/jiazeng/articles/11299438.html

https://www.runoob.com/python/python-functions.html

https://www.runoob.com/python/python-files-io.html

https://www.cnblogs.com/zhangyingai/p/7097920.html
