* [1.什么是时间元组？](#1什么是时间元组)
* [2.使用datetime获取今天日期及前N天日期](#2使用datetime获取今天日期及前n天日期)
* [3.获取以秒为单位的浮点时间time():](#3获取以秒为单位的浮点时间time)
* [4.获取人可以直观理解的时间ctime()：](#4获取人可以直观理解的时间ctime)
* [5.浮点时间转化为直观时间:](#5浮点时间转化为直观时间)
* [6.获取格林尼治时间UTC（Coordinated Universal Time，协调时间）格式：](#6获取格林尼治时间utccoordinated-universal-time协调时间格式)
* [7.将UTC格式的时间转化为浮点值的时间：](#7将utc格式的时间转化为浮点值的时间)
* [8.strptime 和 strftime 函数](#8strptime-和-strftime-函数)
* [9.返回本地区当前日期时间datetime对象](#9返回本地区当前日期时间datetime对象)
* [10.返回数组：（年、第多少周、星期几）](#10返回数组年第多少周星期几)
* [11.如何用Python删除一个文件？](#11如何用python删除一个文件)
* [12.python如何copy一个文件？](#12python如何copy一个文件)
* [13.python如何打开文件？](#13python如何打开文件)
* [14.python如何重命名文件？](#14python如何重命名文件)
* [15.python如何创建目录？](#15python如何创建目录)
* [16.python如何删除目录？](#16python如何删除目录)
* [17.python如何进行文件定位？](#17python如何进行文件定位)
* [18.python如何读取键盘输入？](#18python如何读取键盘输入)
* [19.python如何关闭文件？](#19python如何关闭文件)
* [20.python如何向文件写入数据？](#20python如何向文件写入数据)
* [21.python如何从文件读取数据？](#21python如何从文件读取数据)


## 常用类库

#### 1.什么是时间元组？

很多Python函数用一个元组装起来的9组数字处理时间:

| 序号 | 字段         | 值                                   |
| :--- | :----------- | :----------------------------------- |
| 0    | 4位数年      | 2008                                 |
| 1    | 月           | 1 到 12                              |
| 2    | 日           | 1到31                                |
| 3    | 小时         | 0到23                                |
| 4    | 分钟         | 0到59                                |
| 5    | 秒           | 0到61 (60或61 是闰秒)                |
| 6    | 一周的第几日 | 0到6 (0是周一)                       |
| 7    | 一年的第几日 | 1到366 (儒略历)                      |
| 8    | 夏令时       | -1, 0, 1, -1是决定是否为夏令时的旗帜 |

上述也就是struct_time元组。这种结构具有如下属性：

| 序号 | 属性     | 值                                   |
| :--- | :------- | :----------------------------------- |
| 0    | tm_year  | 2008                                 |
| 1    | tm_mon   | 1 到 12                              |
| 2    | tm_mday  | 1 到 31                              |
| 3    | tm_hour  | 0 到 23                              |
| 4    | tm_min   | 0 到 59                              |
| 5    | tm_sec   | 0 到 61 (60或61 是闰秒)              |
| 6    | tm_wday  | 0到6 (0是周一)                       |
| 7    | tm_yday  | 1 到 366(儒略历)                     |
| 8    | tm_isdst | -1, 0, 1, -1是决定是否为夏令时的旗帜 |

#### 2.使用datetime获取今天日期及前N天日期

问：在Python中如何获取今天的日期？如何获取前N天的日期？
答：使用datetime模块可以完成日期获取任务。
（1）获取当天日期

```
import datetime
# 获取当天日期
# strftime()函数是将time信息输出为想要的格式，如‘2020-08-03’
date_today = datetime.datetime.now().strftime('%Y-%m-%d')
# 输出带有小时分钟的日期
data_today2 = datetime.datetime.now().strftime('%Y-%m-%d %H-%M-%S')

```

（2）获取前N天日期

```
# 通过timedelta(N)函数完成
date_3today_ago = (datetime.datetime.now() - datetime.timedelta(3)).strftime('%Y-%m-%d')

```

#### 3.获取以秒为单位的浮点时间time():

```
>>> import time
>>> print time.time()#获取当前时间的浮点值，单位为秒
1369031293.33
>>> 
```

#### 4.获取人可以直观理解的时间ctime()：

```
print time.ctime()
Mon May 20 14:29:30 2013#获取人能理解的直观时间
```

#### 5.浮点时间转化为直观时间:

```
>>> t = time.time()#浮点时间
>>> print t
1369034676.69
>>> print time.ctime(t)#浮点时间转化为直观时间
Mon May 20 15:24:36 2013
```

#### 6.获取格林尼治时间UTC（Coordinated Universal Time，协调时间）格式：

```
>>> print time.gmtime()#获取UTC格式的当前时间
time.struct_time(tm_year=2013, tm_mon=5, tm_mday=20, tm_hour=6, tm_min=37, tm_sec=45, tm_wday=0, tm_yday=140, tm_isdst=0)
```



#### 7.将UTC格式的时间转化为浮点值的时间：

```
>>> gmt = time.gmtime()#UTC格式的时间
>>> print gmt
time.struct_time(tm_year=2013, tm_mon=5, tm_mday=20, tm_hour=6, tm_min=48, tm_sec=13, tm_wday=0, tm_yday=140, tm_isdst=0)
>>> print time.mktime(gmt)#将UTC格式的时间转化为浮点值的时间
1369003693.0

>>> lt = time.localtime()#将UTC格式当前时区当前时间
>>> print lt
time.struct_time(tm_year=2013, tm_mon=5, tm_mday=20, tm_hour=14, tm_min=49, tm_sec=25, tm_wday=0, tm_yday=140, tm_isdst=0)
>>> print time.mktime(lt)##将UTC格式的时间转化为浮点值的时间
1369032565.0
```



#### 8.strptime 和 strftime 函数

```
时间.strftime(时间格式)
datetime.strptime(字符串,时间格式)
  
示范:
datetime.strptime(str,'%Y-%m-%d')
datetime.now().strftime("%Y-%m-%d %H:%M:%S"）　
```

### 

#### 9.返回本地区当前日期时间`datetime`对象

```
datetime.today()
# 输出 : datetime.datetime(2019, 12, 9, 13, 27, 54, 693978)
```

#### 10.返回数组：（年、第多少周、星期几）

```
d = datetime(2019,12,6,13,30,50)
d.isocalendar()
# 输出 : (2019, 49, 5)
```

#### 11.如何用Python删除一个文件？

使用os.remove(filename)或者os.unlink(filename)

#### 12.python如何copy一个文件？

shutil模块有一个copyfile函数可以实现文件拷贝

#### 13.python如何打开文件？

open(file_name)

#### 14.python如何重命名文件？

os.rename(current_file_name, new_file_name)

#### 15.python如何创建目录？

os.mkdir("newdir")

#### 16.python如何删除目录？

os.rmdir('dirname')

#### 17.python如何进行文件定位？

tell()方法告诉你文件内的当前位置, 换句话说，下一次的读写会发生在文件开头这么多字节之后。

seek（offset [,from]）方法改变当前文件的位置。Offset变量表示要移动的字节数。From变量指定开始移动字节的参考位置。

如果from被设为0，这意味着将文件的开头作为移动字节的参考位置。如果设为1，则使用当前的位置作为参考位置。如果它被设为2，那么该文件的末尾将作为参考位置。

#### 18.python如何读取键盘输入？

raw_input函数
raw_input([prompt]) 函数从标准输入读取一个行，并返回一个字符串（去掉结尾的换行符）。

input函数
input([prompt]) 函数和 raw_input([prompt]) 函数基本类似，但是 input 可以接收一个Python表达式作为输入，并将运算结果返回。

#### 19.python如何关闭文件？

File 对象的 close（）方法刷新缓冲区里任何还没写入的信息，并关闭该文件，这之后便不能再进行写入。

当一个文件对象的引用被重新指定给另一个文件时，Python 会关闭之前的文件。用 close（）方法关闭文件是一个很好的习惯。

#### 20.python如何向文件写入数据？

File 对象的write()方法可将任何字符串写入一个打开的文件。需要重点注意的是，Python字符串可以是二进制数据，而不是仅仅是文字。

write()方法不会在字符串的结尾添加换行符('\n')：

#### 21.python如何从文件读取数据？

File 对象的read())方法从一个打开的文件中读取一个字符串。需要重点注意的是，Python字符串可以是二进制数据，而不是仅仅是文字。



#### 参考链接

https://blog.csdn.net/LI20132017/article/details/107769363

https://www.cnblogs.com/fengff/p/8674681.html

https://blog.csdn.net/weixin_33853794/article/details/86739039

https://www.runoob.com/python/python-tutorial.html
