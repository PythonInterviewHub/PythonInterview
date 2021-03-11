* [1.什么是Flask？有什么优点？](#1什么是flask有什么优点)
* [2.Django和Flask有什么区别？](#2django和flask有什么区别)
* [3.Flask-WTF是什么，有什么特点？](#3flask-wtf是什么有什么特点)
* [4.Flask脚本的常用方式是什么?](#4flask脚本的常用方式是什么)
* [5.如何在Flask中访问会话?](#5如何在flask中访问会话)
* [6.解释Python Flask中的数据库连接?](#6解释python-flask中的数据库连接)
* [7.Flask框架有哪些依赖组件?](#7flask框架有哪些依赖组件)
* [8.Flask蓝图的作用?](#8flask蓝图的作用)
* [9.列举使用过的Flask第三方组件?](#9列举使用过的flask第三方组件)
* [10. 简述Flask上下文管理流程?](#10-简述flask上下文管理流程)
* [11.Flask框架默认session处理机制?](#11flask框架默认session处理机制)
* [12.django请求的生命周期？](#12django请求的生命周期)
* [13.列举django中间件的5个方法？以及django中间件的应用场景？](#13列举django中间件的5个方法以及django中间件的应用场景)
* [14.django rest framework框架中都有那些组件？](#14django-rest-framework框架中都有那些组件)
* [15.django rest framework如何实现的用户访问频率控制？](#15django-rest-framework如何实现的用户访问频率控制)
* [16.django中如何实现单元测试？](#16django中如何实现单元测试)
* [17.django-debug-toolbar的作用？](#17django-debug-toolbar的作用)
* [18.什么是wsgi？](#18什么是wsgi)
* [19.简述什么是FBV和CBV？](#19简述什么是fbv和cbv)
* [20.django中csrf的实现机制](#20django中csrf的实现机制)
* [21.Django本身提供了runserver，为什么不能用来部署？(runserver与uWSGI的区别)](#21django本身提供了runserver为什么不能用来部署runserver与uwsgi的区别)
* [22.Django如何实现websocket？](#22django如何实现websocket)

#### 1.什么是Flask？有什么优点？

Flask是一个Web框架，就是提供一个工具，库和技术来允许你构建一个Web应用程序。这个Web应用程序可以是一些Web页面，博客，wiki，基于Web的日里应用或商业网站。

Flask属于微框架（micro-framework)这一类别，微架构通常是很小的不依赖外部库的框架。其优点如下：

- 框架很轻量
- 更新时依赖小
- 专注于安全方面的bug

#### 2.Django和Flask有什么区别？

Flask
轻量级web框架，默认依赖两个外部库：jinja2和Werkzeug WSGI工具
适用于做小型网站以及web服务的API，开发大型网站无压力，但架构需要自己设计
与关系型数据库的结合不弱于Django，而与非关系型数据库的结合远远优于Django

Django
重量级web框架，功能齐全，提供一站式解决的思路，能让开发者不用在选择上花费大量时间。
自带ORM(Object-Relational Mapping 对象关系映射)和模板引擎，支持jinja等非官方模板引擎。
自带ORM使Django和关系型数据库耦合度高，如果要使用非关系型数据库，需要使用第三方库
自带数据库管理app
成熟，稳定，开发效率高，相对于Flask，Django的整体封闭性比较好，适合做企业级网站的开发。
python web框架的先驱，第三方库丰富


#### 3.Flask-WTF是什么，有什么特点？

Flask-wtf是一个用于表单处理、校验并提供CSRF验证的功能的扩展库
Flask-wtf能把正表单免受CSRF<跨站请求伪造>的攻击

#### 4.Flask脚本的常用方式是什么?

在shell中运行脚本文件
在python编译器中run

#### 5.如何在Flask中访问会话?

会话（seesion）会话数据存储在服务器上。 会话是客户端登录到服务器并注销的时间间隔。 需要在此会话中进行的数据存储在服务器上的临时目录中。
from flask import session导入会话对象
session['name'] = 'admin'给会话添加变量
session.pop('username', None)删除会话的变量


#### 6.解释Python Flask中的数据库连接?

python中的数据库连接有2种方式
1）在脚本中以用第三方库正常连接，用sql语句正常操作数据库，如mysql关系型数据库的pymsql库
2）用ORM来进行数据库连接，flask中典型的flask_sqlalchemy，已面向对象的方式进行数据库的连接与操作

#### 7.Flask框架有哪些依赖组件?

Route(路由)
templates(模板)
Models(orm模型)
blueprint(蓝图)
Jinja2模板引擎

#### 8.Flask蓝图的作用?

蓝图Blueprint实现模块化的应用

- book_bp = Blueprint('book', __name__）创建蓝图对象
- 蓝图中使用路由@book_bp.route('url')
- 在另一.py文件里导入和注册蓝图from book import book_bp app.register_blueprint(book_bp)

作用
将不同的功能模块化
构建大型应用
优化项目结构
增强可读性,易于维护（跟Django的view功能相似）


#### 9.列举使用过的Flask第三方组件?

flask_bootstrap
flask-WTF
flask_sqlalchemy

#### 10. 简述Flask上下文管理流程?

每次有请求过来的时候，flask 会先创建当前线程或者进程需要处理的两个重要上下文对象，把它们保存到隔离的栈里面，这样视图函数进行处理的时候就能直接从栈上获取这些信息。

#### 11.Flask框架默认session处理机制?

Flask的默认session利用了Werkzeug的SecureCookie，把信息做序列化(pickle)后编码(base64)，放到cookie里了。

过期时间是通过cookie的过期时间实现的。

为了防止cookie内容被篡改，session会自动打上一个叫session的hash串，这个串是经过session内容、SECRET_KEY计算出来的，看得出，这种设计虽然不能保证session里的内容不泄露，但至少防止了不被篡改。

#### 12.django请求的生命周期？

1.wsgi,请求封装后交给web框架
2.中间件，对请求进行校验或者在请求对象中添加其他相关数据，
3.路由匹配，根据浏览器发送的不同url去匹配不同的视图函数
4.视图函数，在视图函数中进行业务逻辑的处理
5.中间件，对响应的数据进行处理
6.wsgi,将响应的内容发送给浏览器

#### 13.列举django中间件的5个方法？以及django中间件的应用场景？

1.process_request
接收到客户端信息后立即执行，视图函数之前
2.process_response
返回到客户端信息前最后执行，视图函数之后
3.process_view
拿到视图函数的名称，参数，执行process_view()方法
4.process_exception
视图函数出错时执行
5.process_template_response
在视图函数执行完后立即执行，前提是视图返回的对象中有一个render()方法

#### 14.django rest framework框架中都有那些组件？

1.序列化组件:serializers 对queryset序列化以及对请求数据格式校验
2.路由组件routers 进行路由分发
3.视图组件ModelViewSet 帮助开发者提供了一些类，并在类中提供了多个方法
4.认证组件 写一个类并注册到认证类(authentication_classes)，在类的的authticate方法中编写认证逻
5.权限组件 写一个类并注册到权限类(permission_classes)，在类的的has_permission方法中编写认证逻辑。
6.频率限制 写一个类并注册到频率类(throttle_classes)，在类的的allow_request/wait 方法中编写认证逻辑
7.解析器 选择对数据解析的类，在解析器类中注册(parser_classes)
8.渲染器 定义数据如何渲染到到页面上,在渲染器类中注册(renderer_classes)
9.分页 对获取到的数据进行分页处理, pagination_class
10.版本 版本控制用来在不同的客户端使用不同的行为
在url中设置version参数，用户请求时候传入参数。在request.version中获取版本，根据版本不同 做不同处理

#### 15.django rest framework如何实现的用户访问频率控制？

from rest_framework.throttling import SimpleRateThrottle

这里使用的节流类是继承了SimplePateThrottle类，而这个类利用了django内置的缓存来存储访问记录。通过全局节流设置，所有的视图类默认是使用UserThrottle类进行节流，如果不想使用默认的类就自定义给throttle_classes属性变量赋值，如：“throttle_classes = [VisitThrottle,]”。

#### 16.django中如何实现单元测试？

django的单元测试使用python的unittest模块，这个模块使用基于类的方法来定义测试。

#### 17.django-debug-toolbar的作用？

用来调试请求的接口

#### 18.什么是wsgi？

WSGI是Python在处理HTTP请求时，规定的一种处理方式。如一个HTTP Request过来了，那么就有一个相应的处理函数来进行处理和返回结果。WSGI就是规定这个处理函数的参数长啥样的，它的返回结果是长啥样的？至于该处理函数的名子和处理逻辑是啥样的，那无所谓。简单而言，WSGI就是规定了处理函数的输入和输出格式。

#### 19.简述什么是FBV和CBV？

FBV和CBV本质是一样的，基于函数的视图叫做FBV，基于类的视图叫做CBV。
在python中使用CBV的优点：
提高了代码的复用性，可以使用面向对象的技术，比如Mixin（多继承）。
可以用不同的函数针对不同的HTTP方法处理，而不是通过很多if判断，提高代码可读性。


#### 20.django中csrf的实现机制

第一步：django第一次响应来自某个客户端的请求时,后端随机产生一个token值，把这个token保存在SESSION状态中;同时,后端把这个token放到cookie中交给前端页面；
第二步：下次前端需要发起请求（比如发帖）的时候把这个token值加入到请求数据或者头信息中,一起传给后端；Cookies:{csrftoken:xxxxx}
第三步：后端校验前端请求带过来的token和SESSION里的token是否一致。

#### 21.Django本身提供了runserver，为什么不能用来部署？(runserver与uWSGI的区别)

1）runserver方法是调试 Django 时经常用到的运行方式，它使用Django自带的
WSGI Server 运行，主要在测试和开发中使用，并且 runserver 开启的方式也是单进程 。
2）uWSGI是一个Web服务器，它实现了WSGI协议、uwsgi、http 等协议。注意uwsgi是一种通信协议，而uWSGI是实现uwsgi协议和WSGI协议的 Web 服务器。uWSGI具有超快的性能、低内存占用和多app管理等优点，并且搭配着Nginx就是一个生产环境了，能够将用户访问请求与应用 app 隔离开，实现真正的部署 。相比来讲，支持的并发量更高，方便管理多进程，发挥多核的优势，提升性能。

#### 22.Django如何实现websocket？

django实现websocket官方推荐大家使用channels。channels通过升级http协议来升级到websocket协议。保证实时通讯。也就是说，我们完全可以用channels实现我们的即时通讯。而不是使用长轮询和计时器方式来保证伪实时通讯。他通过改造django框架，使django既支持http协议又支持websocket协议。



#### 参考资料

https://blog.csdn.net/wl_python/article/details/81131873

https://www.cnblogs.com/bk770466199/p/12696103.html

https://www.jianshu.com/p/724233387ba3
