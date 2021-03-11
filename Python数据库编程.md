
* [1.什么是MySQLdb?](#1什么是mysqldb)
* [2.如何连接数据库？](#2如何连接数据库)
* [3.如何创建数据库表？](#3如何创建数据库表)
* [4.如何执行数据插入？](#4如何执行数据插入)
* [5.如何执行数据库查询操作？](#5如何执行数据库查询操作)
* [6.如何更新数据库数据？](#6如何更新数据库数据)
* [7.如何删除数据库数据？](#7如何删除数据库数据)
* [8.如何使用数据库事务？](#8如何使用数据库事务)
* [9.python如何操作redis？](#9python如何操作redis)
* [10.如果redis中的某个列表中的数据量非常大，如何实现循环显示每一个值？](#10如果redis中的某个列表中的数据量非常大如何实现循环显示每一个值)
* [11.什么是一致性哈希？Python中是否有相应模块？](#11什么是一致性哈希python中是否有相应模块)


## 数据库编程


#### 1.什么是MySQLdb?

MySQLdb 是用于Python链接Mysql数据库的接口，它实现了 Python 数据库 API 规范 V2.0，基于 MySQL C API 上建立的。

#### 2.如何连接数据库？

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost", "testuser", "test123", "TESTDB", charset='utf8' )

# 使用cursor()方法获取操作游标 
cursor = db.cursor()

# 使用execute方法执行SQL语句
cursor.execute("SELECT VERSION()")

# 使用 fetchone() 方法获取一条数据
data = cursor.fetchone()

print "Database version : %s " % data

# 关闭数据库连接
db.close()
```

#### 3.如何创建数据库表？

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost", "testuser", "test123", "TESTDB", charset='utf8' )

# 使用cursor()方法获取操作游标 
cursor = db.cursor()

# 如果数据表已经存在使用 execute() 方法删除表。
cursor.execute("DROP TABLE IF EXISTS EMPLOYEE")

# 创建数据表SQL语句
sql = """CREATE TABLE EMPLOYEE (
         FIRST_NAME  CHAR(20) NOT NULL,
         LAST_NAME  CHAR(20),
         AGE INT,  
         SEX CHAR(1),
         INCOME FLOAT )"""

cursor.execute(sql)

# 关闭数据库连接
db.close()

```

#### 4.如何执行数据插入？

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost", "testuser", "test123", "TESTDB", charset='utf8' )

# 使用cursor()方法获取操作游标 
cursor = db.cursor()

# SQL 插入语句
sql = """INSERT INTO EMPLOYEE(FIRST_NAME,
         LAST_NAME, AGE, SEX, INCOME)
         VALUES ('Mac', 'Mohan', 20, 'M', 2000)"""
try:
   # 执行sql语句
   cursor.execute(sql)
   # 提交到数据库执行
   db.commit()
except:
   # Rollback in case there is any error
   db.rollback()

# 关闭数据库连接
db.close()
```

#### 5.如何执行数据库查询操作？

Python查询Mysql使用 fetchone() 方法获取单条数据, 使用fetchall() 方法获取多条数据。

fetchone(): 该方法获取下一个查询结果集。结果集是一个对象
fetchall():接收全部的返回结果行.
rowcount: 这是一个只读属性，并返回执行execute()方法后影响的行数。

#### 6.如何更新数据库数据？

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost", "testuser", "test123", "TESTDB", charset='utf8' )

# 使用cursor()方法获取操作游标 
cursor = db.cursor()

# SQL 更新语句
sql = "UPDATE EMPLOYEE SET AGE = AGE + 1 WHERE SEX = '%c'" % ('M')
try:
   # 执行SQL语句
   cursor.execute(sql)
   # 提交到数据库执行
   db.commit()
except:
   # 发生错误时回滚
   db.rollback()

# 关闭数据库连接
db.close()
```

#### 7.如何删除数据库数据？

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost", "testuser", "test123", "TESTDB", charset='utf8' )

# 使用cursor()方法获取操作游标 
cursor = db.cursor()

# SQL 删除语句
sql = "DELETE FROM EMPLOYEE WHERE AGE > %s" % (20)
try:
   # 执行SQL语句
   cursor.execute(sql)
   # 提交修改
   db.commit()
except:
   # 发生错误时回滚
   db.rollback()

# 关闭连接
db.close()

```

#### 8.如何使用数据库事务？

```
# SQL删除记录语句
sql = "DELETE FROM EMPLOYEE WHERE AGE > %s" % (20)
try:
   # 执行SQL语句
   cursor.execute(sql)
   # 向数据库提交
   db.commit()
except:
   # 发生错误时回滚
   db.rollback()
```

#### 9.python如何操作redis？

```
连接
- 直接连接：
    import redis 
    r = redis.Redis(host='10.211.55.4', port=6379)
    r.set('foo', 'Bar')　　　　# 这里的方法与Redis命令类似
    print r.get('foo')
- 连接池：
    import redis
    pool = redis.ConnectionPool(host='10.211.55.4', port=6379)
    r = redis.Redis(connection_pool=pool)
    r.set('foo', 'Bar')
    print r.get('foo')

```

#### 10.如果redis中的某个列表中的数据量非常大，如何实现循环显示每一个值？

```
　　　　 def list_iter(key, count=3):
            start = 0
            while True:
                result = conn.lrange(key, start, start+count-1)
                start += count
                if not result:
                    break
                for item in result:
                    yield item
　　　　# 调用
        for val in list_iter('num_list'):
            print(val)

```

#### 11.什么是一致性哈希？Python中是否有相应模块？

一致性hash算法（DHT）可以通过减少影响范围的方式，解决增减服务器导致的数据散列问题，从而解决了分布式环境下负载均衡问题；
如果存在热点数据，可以通过增添节点的方式，对热点区间进行划分，将压力分配至其他服务器，重新达到负载均衡的状态。

Python模块--hash_ring，即Python中的一致性hash。


#### 参考资料

https://www.runoob.com/python/python-mysql.html

https://www.cnblogs.com/wcwnina/p/10304641.html
