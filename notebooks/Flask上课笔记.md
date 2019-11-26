# 安装加载第三方库

```
1、pip install Flask
2、pip install Flask-Script
3、pip install Flask-blueprint
4、pip install Flask-Session
5、pip install Flask-SQLAlchemy
6、pip install Flask-Migrate
7、pip install Flask-Bootstrap
8、pip install Flask-DebugToolbar
9、pip install Flask-Cache
10、pip install Flask-RESTful
11、pip install Flask-Mail

虚拟环境的迁移：
pip freeze > requirements.txt   #迁移脚本requirements.txt保存的位置为当前目录
pip install -r requirements.txt
```



# 安装虚拟环境

```
虚拟环境
  安装pip
      CentOS yum install pip
      Ubuntu apt install python-pip
      记得前面添加sudo
      注意：如果没有apt 那么解决办法 sudo apt update 更新源中的软件包管理工具

      apt update 更新源中的软件包
      apt install xxx  安装指定的软件xxx
      apt remove xxx 卸载软件（仅仅卸载软件）
      apt autoremove xxx 卸载软件（会卸载软件和没有用的依赖包）

  安装virtualenv
     sudo apt install virtualenv

  统一管理虚拟环境virtualenvwrapper
       sudo pip install virtualenvwrapper

  virtualenvwrapper.sh安装路径
       /usr/local/bin/
       
  修改环境变量
       sudo vim ~/.bashrc
       打开bashrc之后 编辑
       #python
       export WORKON_HOME = /home/xxx(用户名字)/.virtualenvs
       注意需要创建.virtualenv的文件夹  mkdir .virtualenv
       source xxx virtualenvwrapper.sh 激活路径

  激活更新后的环境变量
       source .bashrc

  创建虚拟环境
       mkvirtualenv ENV_NAME名字

  退出虚拟环境 
       deactivate

  进入虚拟环境 
       workon ENV_NAME
       
  查看虚拟环境
  		workon
  		
创建3.x的虚拟环境
       mkvirtualenv xxx -p /usr/bin/python3
  
pip python专用的包管理工具
       pip install xxx 安装某一个软件
       pip uninstall xxx 卸载某一个软件
       pip list 列出所有的依赖包
       pip freeze 列出自己安装的所有的依赖包
       
虚拟环境迁移
	pip freeze > requirements.txt   #迁移脚本requirements.txt保存的位置为当前目录
	pip install -r requirements.txt
	
	
	
	
深度系统创建虚拟环境
安装：pip install virtualenv

创建虚拟环境：
    cd ~/你的项目文件夹
    # 创建虚拟环境
    # 虚拟环境可以创建到任何位置,但一般与项目文件夹放到一起
    virtualenv .venv
    
加载虚拟环境：
	source ~/项目文件夹/.venv/bin/activate
	# 激活虚拟环境
	
退出虚拟环境：
	deactivate
# 当开发完成后,可以退出当前虚拟环境
```

# 常用的状态码

```
状态码：
    服务器向用户返回的状态码和提示信息，常见的有以下一些地方
    200 OK - [GET]：服务器成功返回用户请求的数据
    201 CREATED -[POST/PUT/PATCH]：用户新建或修改数据成功
    202 Accepted - [*] ：表示一个请求已经进入后台排队（异步任务）
    204 NO CONTENT - [DELETE]：表示数据删除成功
    400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误
    401 Unauthorized - [*] ：表示用户没有权限（令牌，用户名，密码错误）
    403 Forbidden - [*]：表示用户得到授权，但是访问是被禁止的
    404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录
    405 请求方式错误
    406 Not Acceptable - [*]：用户请求格式不可得
    410 Gone - [GET] ：用户请求的资源被永久移除，且不会再得到的
    422 Unprocesable entity -[POST/PUT/PATCH]：当创建一个对象时，发生一个验证错误，登陆的时候 如果没有获取到用户名 或者 密码
    500 INTERNAL SERVER EROR - [*] ：服务器内部发生错误
推荐使用json数据传输
```



# 一、框架简介

## １、基于python的web(微)框架

```
重量级框架　django
	为了方便业务程序的开发，提供了丰富的工具及其组件
轻量级框架　flask
	只提供web核心功能，自由灵活，高度定制，Ｆlask也被称为“microfrmework”,因为它使用简单的核心，用　extension　增加其他功能
```

## ２、官方文档

```
http://flask.pocoo.org/docs/0.12/      英文
http://docs.jinkan.org/docs/flask/     中文
```

## ３、flask依赖库

```
flask依赖三个库
 jinja2         模板引擎
 Werkzeug  WSGI 工具集
 Itsdangerous   基于Django的签名模块
 现在不仅仅是三个  但是依然前两个有用
 安装时候会出现6个 看看就可以了
```

## ４、flask流行的主要原因

```
 1 有非常齐全的官方文档，上手非常方便
 2 有非常好的扩展机制和第三方扩展环境，工作中常见的软件都会有   对应的扩展，动手实现扩展也很容易
 3 社区活跃度非常高 flask的热度已经超过django好几百了
 4 微型框架的形式给了开发者更大的选择空间
```

## ５、配置static和templates路径

static和templates默认是与app = Flask(__name__）在同一文件夹下查找：

```
#核心代码
#settings.py
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
#BASE_DIR=E:\python_django\Flask_Project\Debugtoolber_flask（也就是工程根目录）

#__init__.py
templates_folder = os.path.join(settings.BASE_DIR, 'templates')
static_folder = os.path.join(settings.BASE_DIR,'static')
app = Flask(__name__,template_folder=templates_folder,static_folder=static_folder)
```

# 二、BS/CS

概念：

```
BS:B browser 浏览器   S server  服务器   主流
CS:C client  客户端   S server  服务器
B/S结构是WEB兴起后的一种网络结构模式，WEB浏览器是客户端最主要的应用软件。这种模式统一了客户端，将系统功能实现的核心部分集中到服务器上，简化了系统的开发、维护和使用。
```

**CS/BS的区别：**

![BS-CS区别](/home/shenyang/Desktop/每日资料/Falsk资料/day01/doc/BS-CS区别.png)

# 三、MVC/MTV

## **MVC**

**Model：**数据的封装，数据的抽象，用来操作数据的入口
**View**：视图，主要用来呈现给用户的
**Controller**：控制器，主要用来接收用户请求（输入），并且协调模型和视图

**核心理念**：解耦
**实现结果：**将数据操作，页面展示，逻辑处理进行了拆分

```
MVC：软件架构思想
	简介：
		MVC开始是存在于桌面程序中的，M是指业务模型 model，V是指用户界面 view，C则是控制器 controler，使用MVC的目的是将M和V的实现代码分离，从而使同一个程序可以使用不同的表现形式。比如一批统计数据可以分别用柱状图、饼图来表示。C存在的目的则是确保M和V的同步，一旦M改变，V应该同步更新
实现了模型层的复用
	核心思想: 
		解耦合
	面向对象语言：高内聚  低耦合
	Model
		模型
		封装数据的交互操作
			CRUD
	View
		视图
		是用来将数据呈现给用户的
	Controller
		控制器
		接受用户输入输出
		用来协调Model和View的关系，并对数据进行操作，筛选
	流程
		控制器接受用户请求
		调用模型，获取数据
		控制器将数据展示到视图中
```

![](/home/shenyang/Pictures/31.jpg)

## MTV也叫MVT

**Models：**封装数据操作、数据库的表和字段的定义
**Template：**模板、用来展示数据
**Views**:视图函数、相当于controller、接收请求，协调模型和模板

```
MTV
	也叫做MVT
	本质上就是MVC，变种
	Model
		同MVC中Model
	Template
		模板
		只是一个html，充当的是MVC中View的角色，用来做数据展示
	Views
		视图函数
		相当于MVC中Controller
```

# 四、Flask的基本使用

## １、虚拟环境的创建

```
1.创建flask的虚拟环境
	mkvirtualenv Flaskpython1905 -p /usr/bin/python3
2.查看虚拟环境
	pip freeze
	pip list

3.虚拟环境迁移
	pip freeze > requirements.txt
		迁出
	pip install -r requirements.txt
		迁入
```

## ２、Flask项目的创建

```
1.安装
	国外源  pip install flask
	国内源  pip install flask -i https://pypi.douban.com/simple
2.创建项目
	mkdir python1905 mkdir Flaskday01  mkdir FirstFlask  vim HelloFlask.py
	代码结构
		from flask import Flask
         app = Flask(__name__)

        @app.route("/")
        def index():
            return "Hello"
        app.run()
3.启动服务器  python  文件名字.py
	默认端口号  5000  只允许本机连接
```

## ３、启动服务器参数修改 

```
run方法中添加参数
	在启动的时候可以添加参数在　run中
	debug
		是否开启调试模式，开启后修改过python代码自动重启
		如果修改的是html/js/css 那么不会自动重启
	host
		主机，默认的是127.0.0.1 指定为0.0.0.0代表本机的ip 
	port
		指定服务器端口号
	threaded
		是否开启多线程
		
```

扩展：ＰＩＮ码 

```
全称Personal Identification Number.就是SIM卡的个人识别密码。手机的PIN码是保护SIM卡的一种安全措施，防止别人盗用SIM卡，如果启用了开机PIN码，那么每次开机后就要输入4到8位数PIN码。
在输入三次PIN码错误时，手机便会自动锁卡，并提示输入PUK码解锁，需要使用服务密码拨打运营商客服热线，客服会告知初始的PUK码，输入PUK码之后就会解锁PIN码。
```

## ４、命令行参数

```
	1.安装
		pip install flask-script
		作用
			启动命令行参数
	2.初始化
		修改  文件.py为manager.py
		manager = Manager(app=app)
		修改 文件.run()为manager.run()
	3.运行
		python manager.py runserver -p xxx -h xxxx -d -r
          参数
          - p  端口 port
          - h  主机  host
          - d  调试模式  debug
          - r  重启（重新加载） reload（restart）
```

# 五、视图函数返回值

```
	（1）index返回字符串
		@app.route('/index/')
         def index():
            return 'index'
	（2）模板first.html
		@app.route('/first/')
         def hello():
            return render_template("test.html")
      静态文件css
           注意
           <link rel="stylesheet" href="/static/css/hello.css">
```

# 六、Flask基础结构

```
App
	templates
		模板
		默认也需要和项目保持一致
	static
		静态资源
		默认需要和我们的项目保持一致，在一个路径中，指的Flask对象创建的路径
	views
	models
	坑点
		执行过程中manager.py和其他的文件的路径问题
	第二个坑--封装__init__文件--
```

# 七、蓝图

## １、概念：

**什么是蓝图：**一个蓝图定义了可用于单个应用的视图，模板，静态文件等等的集合

**什么时候会用到蓝图：**蓝图是将你的应用组织成不同的组件

**通常情况下的组织结构**：

![](/home/shenyang/Pictures/33.png)



**使用蓝图后的项目组织结构：**

![](/home/shenyang/Pictures/32.png)



## ２、蓝图的安装与使用

```

	1. 宏伟蓝图（宏观规划）
	2. 蓝图也是一种规划，主要用来规划urls（路由）
	3. 蓝图基本使用
  	- 安装
     - pip install flask-blueprint
     - 初始化蓝图   blue = Blueprint('first',__name__)
     - 调用蓝图进行路由注册  app.register_blueprint(blueprint=blue)
```

## ３、核心代码

```
#views.py
from flask import Blueprint

blue=Blueprint('blue',__name__)
                                                                                  
def init_blue(app):
    app.register_blueprint(blueprint=blue)
    
@blue.route('/')
def index():
    return '欢迎来到召唤师峡谷'
```

# 八、Flask请求流程

```
Flask请求流程
	请求到路由   app.route()
	视图函数   
	视图函数和models交互
	模型返回数据到视图函数
	视图函数渲染模板
	模板返回给用户
```

![34](/home/shenyang/Pictures/34)

# 九、Flask路由参数

```
# 路由参数

# 路由参数的基本结构 /资源路径/<变量>/
# 路由参数的访问路径 http://127.0.0.1:5000/testRoute/1/
# 路由参数的名字一定要和视图函数的参数一致
# 路由参数的传到视图函数 是字符串类型
@blue.route('/testRoute/<id>/')
def test(id):
    print(type(id))
    return 'testRoute'


# 路由参数的类型 默认情况下是字符串
# string  path  int  float  uuid any

# string
接收的时候也是str， 匹配到 / 的时候是匹配结束
@blue.route('/testRoute1/<string:name>/')
def testRoute1(name):
    print(name)
    print(type(name))
    return 'testRoute1'

# path
接收的时候也是str， / 只会当作字符串中的一个字符处理
@blue.route('/testRoute2/<path:name>/')
def testRoute2(name):
    print(name)
    print(type(name))
    return 'testRoute2'
# 总结
# string和path的区别？
# string遇到/ 会当作结束标签
# path遇到/ 会当作一个字符串


# int
@blue.route('/testRoute3/<int:money>/')
def testRoute3(money):
    print(money)
    print(type(money))
    return 'testRoute3'


# float
@blue.route('/testRoute4/<float:price>/')
def testRoute4(price):
    print(price)
    print(type(price))
    return 'testRoute3'


# uuid
@blue.route('/testuuid/')
def testuuid():

    uid = uuid.uuid4()
    print(uid)

    return 'testuuid'

@blue.route('/testRoute5/<uuid:uid>/')
def testRoute5(uid):
    print(uid)
    print(type(uid))
    return 'testRoute5'

# any
任意一个
已提供选项的任意一个 而不能写参数外的内容  注意的是/
@blue.route('/testRoute6/<any(a,b):p>/')
def testRoute6(p):
    print(p)
    print(type(p))
    return 'testRoute6'
```

# 十、postman

```
请求方式又叫做http方法
# get（获取） post（添加） delete （删除）  put(修改全部属性) patch（修改的是部分属性）

# 需求：执行一个视图函数 然后跳转到一个模板 login.html
# 在模板中输入用户名字  然后点击登录
# 点击之后 显示欢迎光临红浪漫

@blue.route('/toLogin/')
def toLogin():
    return render_template('login.html')

# 路由默认只支持  get  head  options请求方式 不支持post  delete
# 如果想让路由支持post delete put patch怎么办 可以在route方法中添加一个参数
# 这个参数是methods=[]
# methods列表的元素的大小写都可以
@blue.route('/login/',methods=['post','delete'])
def login():
    return '欢迎光临红浪漫,拖鞋手牌拿好,楼上二楼左转,男宾3位'

# 状态码
# 200 成功
# 301 重定向
# 302 永久重定向
# 403 防跨站攻击 forbidden
# 404 路径
# 405 请求方式错误
# 500 服务器 业务逻辑错误


# postman 请求模拟工具
@blue.route('/testPostman/',methods=['post','get','put'])
def testPostman():
    return '你的梦想是否只是说说而已'
```

# 十一、反向解析

```
反向解析
@blue.route('/testReverse/')
def testReverse():
    return 'testReverse'


@blue.route('/testReverse1/')
def testReverse1():

    # 反向解析的语法  url_for(蓝图的名字.方法的名字)
    # 反向解析获取的是请求资源路径
    # 获取testReverse的请求资源路径
    s = url_for('blue.testReverse')
    print(s)

    s1 = url_for('blue.testPostman')
    print(s1)

    # 应用场景:
    #       (1)  redirect('/index/') 重定向到index请求
    #            尽量不要使用硬编码 redirect(url_for('blue.index'))
    #       (2)  页面中 不要写硬编码  form action='/login/'
    #            form action = url_for('blue.login')

    return 'testReverse1'
```

# 十二、Request

```
request是一个内置对象
内置对象：不需要创建就可以直接使用的对象
属性
	method  **
	获取的是请求方式/http方法
	
	base_url
	去掉请求参数的路径
	http://127.0.0.1:5000/testRequest/
	去掉get参数的url
	
	host_url
	http://127.0.0.1:5000/
	主机的路径不带请求资源路径
	只有主机和端口号的url
		
	url
	 http://127.0.0.1:5000/testRequest/?name=zs
	  完整的请求地址（请求资源路径，请求参数）
	  
	remote_addr **
	请求的客户端地址  应用场景  反爬虫
	
	 应用场景 文件上传
    print(request.files)

    # 请求头
    print(request.headers)

    # 请求资源路径   应用场景：购物车
    print(request.path)

    # 获取请求的cookies
    print(request.cookies)
    
    #session	
		与request类似  也是一个内置对象  可以直接打印 print（session）


	 获取get请求方式的参数的方式：
	request.args.get('name')
	args  **
		1. args
         - get请求参数的包装，args是一个ImmutableMultiDict对象，类字典结构对象
         - 数据存储也是key-value
         - 外层是大列表，列表中的元素是元组，元组中左边是key，右边是value
     一般情况下 post请求方式都是通过表单形式使用的
     eg：
     	<form action='xxx' method='post'>
     		<input type='text' name='name'>
     获取post请求方式的参数的方式
     request.form.get('name')
     
	form   **
		2. form
         - 存储结构个args一致
         - 默认是接收post参数
         - 还可以接收 PUT，PATCH参数
   
```

# 十三、Response

## response 视图函数的返回值类型

```

# 视图函数返回字符串
@blue.route('/testResponse/')
def testResponse():
    return '窗前明月光'


# 视图函数返回一个模板
@blue.route('/testResponse2/')
def testResponse2():
    s = render_template('testResponse2.html')
    print(type(s))
    return s


# 视图函数返回一个make_response()
@blue.route('/testResponse3/')
def testResponse3():
    r = make_response('<h1>举头望明月</h1>')
    print(type(r))
    return r

# 视图函数返回redirect
@blue.route('/index/')
def index():
    return 'welcome to 东北'

@blue.route('/testResponse4/')
def testResponse4():
    # r = redirect('/index/')
    r = redirect(url_for('blue.index'))
    print(type(r))
    return r

# 视图函数返回Response对象
@blue.route('/testResponse5/')
def testResponse5():
    r = Response('低头思故乡')
    print(type(r))
    return r


# 总结：视图函数的返回值有2大类 1 字符串   (1)普通字符串  (2)render_template
2 response    (1)make_response  (2)redirect  (3)Response
```

## 异常

```
abort
	直接抛出 显示错误状态码  终止程序运行
	abort(404)
	eg:
		@blue.route('/makeabort/')
         def make_abort():
              abort(404)
              return '天还行'
```

```
捕获
	@blue.errorhandler()
		- 异常捕获
		- 可以根据状态或 Exception进行捕获
		- 函数中要包含一个参数，参数用来接收异常信息
	eg:
	@blue.errorhandler(502)
    def handler502(exception):
        return '不能让你看到状态码'
```

# 十四、会话技术

```
1.请求过程Request开始，到Response结束
2.连接都是短连接
3.延长交互的生命周期
4.将关键数据记录下来
5.Cookie是保存在浏览器端/客户端的状态管理技术
6.Session是服务器端的状态管理技术
```

![](/home/shenyang/Desktop/每日资料/Falsk资料/day02/img/cookie和session.png)

## １、cookie

```
Cookie
	1.客户端会话技术
	2.所有数据存储在客户端
	3.以key-value进行数据存储层
	4.服务器不做任何存储
	5.特性
		支持过期时间
			max_age
			expries
		根据域名进行cookie存储
		不能跨网站（域名）
		不能跨浏览器
		自动携带本网站的所有cookie
	6.cookie是服务器操作客户端的数据
	7.通过Response进行操作
```

```
cookie登陆使用
	设置cookie    response.set_cookie('username',username)
		response
	获取cookie    username = request.cookies.get('username','游客')
		request
	删除cookie     response.delete_cookie('username')
		response
```

## ２、session

```
Session
	1.服务端会话技术
	2.所有数据存储在服务器中
	3.默认存在服务器的内存中
		- django默认做了数据持久化（存在了数据库中）
	4.存储结构也是key-value形势，键值对
	【注】单纯的使用session是会报错的，需要使用在__init__方法中配置app.config['SECRET_KEY']=‘110’
```

```
session登陆使用
	设置    session['username'] = username
	获取    session.get('username')
	删除
		   resp.delete_cookie('session')
		   session.pop('username')
```

## ３、session持久化问题

**Seeion**

```
--diango中对session做了持久化，储存在数据库中

--可以修改到redis中，flask中没有对默认session（服务端会话技术）进行任何处理

--flask-session 可以实现session的数据持久化

--Session需要持久化到redis中

--缓存在磁盘上的时候，管理磁盘文件用lru，最近最少使用原则

```

**实现方案：**

```
安装插件：flask-session    pip install flask-session
在国内源安装：pip install flask-sessin -i 			　　　　　　　https://pipy.douban.com/simple

配置init中app.config['SESSION_TYPE]='redis'
初始化：1 Session(app=app)
	　 2 session = Session()  session.init_app(app = app)
安装redis: pip install redis
需要配置SECRET_KEY : app.config['SECRET_KEY'] = '123' 
#解决密钥问题

其他配置--视情况而定 : 
app.config['SESSION_KEY_PREFIX']='flask'
					app.config['SESSION_COOKIE_SECURE']=True
```

查看redis内容

```
redis-cli
keys *
get key

flask的session的生存时间是３１天
django的session生存时间是1４天
```

# 十五、Template

简介：

```
MVC中的View，MTV中的Template
主要用来做数据展示的
模板处理过程分为2个阶段
 1 加载
 2 渲染
```

## １、jinja2模板引擎

```
jinja2模板引擎
            1.本质上是html
            2.支持特定的模板语法
            3.flask作者开发的   一个现代化设计和友好的python模板语言  模仿的django的模板引擎
            4.优点
                    速度快，被广泛使用
                    HTML设计和后端Python分离
                    减少Python复杂度
                    非常灵活，快速和安全
                    提供了控制，继承等高级功能
```

## ２、结构标签

```
#base.html
结构标签
block
	首次出现挖坑操作
	第二次出现填坑操作
	第N次出现，填坑操作，会覆盖前面填的坑
	不想被覆盖，需要添加 {{ super() }}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{ title }}</title>
    <script src="http://libs.baidu.com/jquery/1.9.1/jquery.min.js"></script>
    {% block extCSS %}

    {% endblock %}
</head>
<body>
    {% block header %}

    {% endblock %}
    {% block content %}

    {% endblock %}
    {% block footer %}

    {% endblock %}
    {% block extJS %}

    {% endblock %}
</body>
</html>
```

## ３、extends继承

```
#base_main.html

{% extends 'base.html' %}

{% block extCSS %}
{#在Django中加载静态资源{% static '' %}   url_for("static", filename=xxx) #}
    <link rel="stylesheet" href="{{ url_for('static', filename='css/main.css') }}">
{% endblock %}

{% block header %}
    <h3>小伙子你又睡着了!</h3>
{% endblock %}
```

## ４、include加载

包含，将一个指定的模板包含进来

```
index.html

{% extends 'base_main.html' %}

{% block header %}
    {{ super() }}
    <h6>销量已超200w，国产神车,哈佛H6!</h6>
{% endblock %}

{% block content %}
    {% include 'index_content.html' %}
{% endblock %}
```

## ５、宏定义

可以在模板中定义，调用函数、函数还是用来生成html的、外文件中的宏定义调用需要导入include

```
{#调用函数 同页面调用函数#}
{% macro create_item(goods_id, goods_name) %}
    <h3>商品id{{ goods_id }}</h3>
    <h4>商品名字{{ goods_name }}</h4>
{% endmacro %}

{% block content %}
    {{ create_item("110", "手铐") }}
{% endblock %}


{#外文件导入函数#}
{% macro create_user(name) %}
    <h3>不小心创建了一个用户：{{ name }}</h3>
{% endmacro %}

{% from 'mmm.html' import create_user %}
    {{ create_user("翠花") }}
```

## ６、过滤器

形式：{{ var|xxx|yyy|zzz }}（没有个数限制）

```
{# 字符串操作 #}
{# 当变量未定义时，显示默认字符串，可以缩写为d #}
<p>{{ name | default('No name', true) }}</p>
 
{# 单词首字母大写 #}
<p>{{ 'hello' | capitalize }}</p>
 
{# 单词全小写 #}
<p>{{ 'XML' | lower }}</p>
 
{# 去除字符串前后的空白字符 #}
<p>{{ '  hello  ' | trim }}</p>
 
{# 字符串反转，返回"olleh" #}
<p>{{ 'hello' | reverse }}</p>
 
{# 格式化输出，返回"Number is 2" #}
<p>{{ '%s is %d' | format("Number", 2) }}</p>
 
{# 关闭HTML自动转义 #}
<p>{{ '<em>name</em>' | safe }}</p>
 
{% autoescape false %}
{# HTML转义，即使autoescape关了也转义，可以缩写为e #}
<p>{{ '<em>name</em>' | escape }}</p>
{% endautoescape %}


{# 数值操作 #}
{# 四舍五入取整，返回13.0 #}
<p>{{ 12.8888 | round }}</p>
 
{# 向下截取到小数点后2位，返回12.88 #}
<p>{{ 12.8888 | round(2, 'floor') }}</p>
 
{# 绝对值，返回12 #}
<p>{{ -12 | abs }}</p>



{# 列表操作 #}
{# 取第一个元素 #}
<p>{{ [1,2,3,4,5] | first }}</p>
 
{# 取最后一个元素 #}
<p>{{ [1,2,3,4,5] | last }}</p>
 
{# 返回列表长度，可以写为count #}
<p>{{ [1,2,3,4,5] | length }}</p>
 
{# 列表求和 #}
<p>{{ [1,2,3,4,5] | sum }}</p>
 
{# 列表排序，默认为升序 #}
<p>{{ [3,2,1,5,4] | sort }}</p>
 
{# 合并为字符串，返回"1 | 2 | 3 | 4 | 5" #}
<p>{{ [1,2,3,4,5] | join(' | ') }}</p>
 
{# 列表中所有元素都全大写。这里可以用upper,lower，但capitalize无效 #}
<p>{{ ['tom','bob','ada'] | upper }}</p>




{# 字典列表操作 #}
{% set users=[{'name':'Tom','gender':'M','age':20},
              {'name':'John','gender':'M','age':18},
              {'name':'Mary','gender':'F','age':24},
              {'name':'Bob','gender':'M','age':31},
              {'name':'Lisa','gender':'F','age':19}]
%}
{# 按指定字段排序，这里设reverse为true使其按降序排 #}
<ul>
{% for user in users | sort(attribute='age', reverse=true) %}
     <li>{{ user.name }}, {{ user.age }}</li>
{% endfor %}
</ul>
 
{# 列表分组，每组是一个子列表，组名就是分组项的值 #}
<ul>
{% for group in users|groupby('gender') %}
    <li>{{ group.grouper }}<ul>
    {% for user in group.list %}
        <li>{{ user.name }}</li>
    {% endfor %}</ul></li>
{% endfor %}
</ul>
 
{# 取字典中的某一项组成列表，再将其连接起来 #}
<p>{{ users | map(attribute='name') | join(', ') }}</p>
```

# 十六、models

数据交换封装

Flask默认并没有提供任何数据库操作的API，Flask中可以自己的选择数据，用**原生语句实现功能**：

```
原生SQL缺点
	代码利用率低，条件复杂代码语句越过长，有很多相似语句
    一些SQL是在业务逻辑中拼出来的，修改需要了解业务逻辑
    直接写SQL容易忽视SQL问题
```

Flask中并没有提供默认ORM,可以选择第三方扩展库，**ORM**(ORM 对象关系映射,通过操作对象对数据的操作)

```
SQLAlchemy
	MongoEngine
	将对对象的操作转换为原生SQL
	优点
	易用性，可以有效减少重复SQL
		性能损耗少
		设计灵活，可以轻松实现复杂查询
		移植性好
```

## １、安装以及配置

```
安装sqlalchemy：pip install flask-sqlalchemy

使用app创建SQLALCHEMY对象：（一般选第二种）
	１、直接传入app：db=SQLAlchemy(app=app)
	２、先创建对象，在使用的时候再进行init_app：
		db=SQLAlchemy()  上面这句话一般会放到models中  因为需要db来调用属性 		 		 	db.init_app(app=app)
	３、config中配置  SQLALCHEMY_DATABASE_URI
	（1）pymysql:
mysql+pymysql://username:password@host:port/database
	-数据库+驱动://用户:密码@主机:端口/数据库
	（2）sqlite:
		轻量级数据库，配置简单
        sqlite:///xxxx（sqlite3.db）执行
```

## ２、使用

```
 使用：
	定义模型
			继承Sqlalchemy对象中的model
	定义字段
              主键
                  一定要添加
              所需要字段
              语法
                  db.Column( db.类型（）,约束 )
     创建
	db.create_all()
	删除
	db.drop_all()
	修改表名
	__tablename__ = "Worker"
    数据操作
        创建对象
        添加 
            db.session.add(对象)
            db.session.commit()
        查询
            模型.query.all()
```

# 十七、项目拆分

```
#models.py
from flask_sqlalchemy import SQLAlchemy
db=SQLAlchemy()#创建models.db对象
class User_info(db.Model):
    pass

#init.py
# 选择开发环境以及数据库的选择和配置
app.config.from_object(settings.env.get(ENV_NAME))
# 第三方库的整合
init_ext(app=app)
```

**开发环境：**

​		开发环境
                测试环境
                演示环境-类似线上环境也叫做预生产环境
                线上环境 也叫做 生产环境

Flask轻量级框架，在一个setting.py中实现所有功能

```
def get_database_uri(DATABASE):
    dialect = DATABASE.get('dialect')
    driver = DATABASE.get('driver')
    username = DATABASE.get('username')
    password = DATABASE.get('password')
    host = DATABASE.get('host')
    port = DATABASE.get('port')
    database = DATABASE.get('database')
    return '{}+{}://{}:{}@{}:{}/{}'.format(dialect,driver,username,password,host,port,database)


class Config():
    Test = False
    Debug = False

    SQLALCHEMY_TRACK_MODIFICATIONS = False


class DevelopConfig(Config):
    Debug = True

    DATABASE={
        'dialect':'mysql',
        'driver':'pymysql',
        'username':'root',
        'password':'1234',
        'host':'localhost',
        'port':'3306',
        'database':'day041905'
    }

    SQLALCHEMY_DATABASE_URI = get_database_uri(DATABASE)


class TestConfig(Config):

    Test = True

    DATABASE = {
        'dialect': 'mysql',
        'driver': 'pymysql',
        'username': 'root',
        'password': '1234',
        'host': 'localhost',
        'port': '3306',
        'database': 'day041905'
    }

    SQLALCHEMY_DATABASE_URI = get_database_uri(DATABASE)

class ShowConfig(Config):

    Debug = True

    DATABASE = {
        'dialect': 'mysql',
        'driver': 'pymysql',
        'username': 'root',
        'password': '1234',
        'host': 'localhost',
        'port': '3306',
        'database': 'day041905'
    }

    SQLALCHEMY_DATABASE_URI = get_database_uri(DATABASE)

class ProductConfig(Config):

    Debug = True

    DATABASE = {
        'dialect': 'mysql',
        'driver': 'pymysql',
        'username': 'root',
        'password': '1234',
        'host': 'localhost',
        'port': '3306',
        'database': 'day041905'
    }

    SQLALCHEMY_DATABASE_URI = get_database_uri(DATABASE)


ENV_NAME = {
    'develop':DevelopConfig,
    'test':TestConfig,
    'show':ShowConfig,
    'product':ProductConfig,
}
```

# 十八、flask-mirgrate

数据模型迁移

使用步骤

```
安装：pip install flask-migrate

初始化：
	１、创建migrate对象:
	migrate = Migrate()
	需要在ext.py中使用app和db初始化:migrate.init_app(app=app, db=db)
	２、懒加载初始化：
	结合flask-script使用
	在manager.py中：manager.add_command("db", MigrateCommand)
```

```
如果之前没有migrations的文件夹 那么必须先init，但是如果有这个文件夹 那么就不需要init了
python manager.py db xxx（命令行操作）：
	python manager.py db init #第一次使用，初始化
	python manager.py db migrate #生成迁移文件
	python manager.py db upgrade #将模型映射到数据库表（也就是建表以及完成映射过程）升级
	python manager.py db downgrade #删除数据库中与models映射的模型对应的表　　降级
	
	python manager.py db migrate 无法生成迁移文件有一下两种情况：
	１、模型定义完成从未调用（在视图文件中调用）
	２、数据库已经有模型记录（数据库存在表，尤其是迁移产生的非映射表）
	
	创建用户文件：
	python manager.py db migrate  --message ‘创建用户’
```

**核心代码**

```
#ext.py(创建migtare对象，由于没有其他地方调用，所以放在函数内部，在db初始化的上面)
def init_ext(app):
    # 创建迁移对象以及迁移数据的初始化
    migrate=Migrate()
    migrate.init_app(app=app,db=db)
    
#manager.py
manager.add_command("db", MigrateCommand)
```

# 十九、数据操作DML

   DDL  数据定义语言
        针对表操作    create  alter  drop

   DML  数据操纵语言
        针对数据的操作 insert delete update

   DQL  数据查询语言   select

   TCL  事务         commit rollback

## １、增加

步骤：创建对象、放到数据连接的session进行commit

**db.session.add:**单个添加

```
@blue.route("/addperson/")
def add_person():
    p = Person()
    p.p_name = "小明"
    p.p_age = 15
    db.session.add(p)
    db.session.commit()
    return "添加成功"
```

**db.session.add_all：**添加多个

```
@blue.route("/addpersons/")
def app_persons():
    persons = []
    for i in range(5):
        p = Person()
        p.p_name = "猴子请来的救兵%d" % random.randrange(100)
        p.p_age = random.randrange(70)
        persons.append(p)

    db.session.add_all(persons)
    db.session.commit()
    
    return "添加成功"
```

## ２、删除

```
@blue.route("/deleteperson/")
def delete_person():
    # 查询操作
    person = Person.query.get(3)

    db.session.delete(person)
    db.session.commit()

    return "删除成功
```

## ３、修改

```
@blue.route("/addperson/")
def add_person():
    p = Person()
    p.p_name = "小明"
    p.p_age = 15

    db.session.add(p)
    db.session.commit()

    return "添加成功"
```

## ４、查询DQL

通过过滤器进行查询

**获取单个数据**

```
（1）get
            主键值
            获取不到不会抛错
            person = Person.query.get(3)
            db.session.delete(person)
            db.session.commit()
（2）first
		   person = Person.query.first()
```

**获取结果集**

```
（1）xxx.query.all   
			persons = Person.query.all()
			返回的列表的类型
（2）xxx.query.filter_by
			persons = Person.query.filter_by(p_age=15)
			返回的是BaseQuery对象
 （3）xxx.query.filter
			persons = Person.query.filter(Person.p_age < 18)
			persons = Person.query.filter(Person.p_age.__le__(15))
			persons = Person.query.filter(Person.p_name.startswith("小"))
			persons = Person.query.filter(Person.p_name.endswith("1"))
			persons = Person.query.filter(Person.p_name.contains("1"))
			persons = Person.query.filter(Person.p_age.in_([15, 11]))
			返回的是BaseQuery对象
```

**数据筛选**

```
	（1）order_by
			升序：
				persons = Person.query.order_by("p_age")
			降序：
				persons = Person.query.order_by(db.desc('p_age'))
	（2）limit
			persons = Person.query.limit(5)#取数据前五条
	（3）offset
			persons = Person.query.offset(5).order_by("id")取数据丢弃前5条数据后的所有数据
	（4）offset和limit不区分顺序，offset先生效
			persons = Person.query.order_by("id").limit(5).offset(5)
			persons = Person.query.order_by("_id").limit(5)
		 	persons = Person.query.order_by("id").offset(17).limit(5)
	（5）order_by 需要先调用执行(order_by无论在语法还是执行顺序都是先执行)
		 	persons = Person.query.order_by("id").offset(17).limit(5)
```

# 二十、分页操作

### (1)pagination  

```
（1）简介：分页器
              需要想要的页码
              每一页显示多少数据
（2）原生：
		 persons = Person.query.offset((page_num - 1) * page_per).limit(page_per)
（3）封装：
        参数（page，page_per,False(是否抛异常）
        persons = Person.query.paginate(page_num, page_per, False).items
```

### (2)paginate参数以及属性

```
pagination = Movie.query.paginate(page,per_page,False)
	#用法
	page：当前页数
	per_page：每页多少条数据
	error_out=False是否打印错误信息
	#属性
    items：pagination对象转化为可迭代对象
    total 数据总条数
	pages：获取总页数
    prev_num：上一页的页码
    has_prev：是否有上一页，返回布尔值
    next_num：下一个页码
    has_next：是否有下一页，返回布尔值
    iter_pages：所有页码，返回列表
    paginate(page, per_page,error_out).items
	返回当前页的所有数据
```

### (3)核心的代码实现

```
"""
创建分页函数对象pagination，传递pagination，使用pagination对象其中分页函数、参数实现分页操作
"""

```

**实例：**查询所有学生信息，每页显示2条数据，可以通过页码和上一页、下一页跳转页面。

**视图：**

```
@stu.route('/stupage/')
def stu_page():
	page是要查询的页码   page从哪里获得???
    page = int(request.args.get('page', 1))
    per_page = int(request.args.get('per_page', 2))
	思考该方法的返回值类型 然后观察该类有什么方法
    paginate = Student.query.order_by('-s_id').paginate(page, per_page, error_out=False)

    stus = paginate.items

    return render_template('stupage.html', paginate=paginate, stus=stus)
    
```

##### **html页面解析数据**

```

{% extends 'base_main.html' %}

{% block title %}
    分页显示学生信息
{% endblock %}

{% block content %}
    <h2>学生信息</h2>
    {% for stu in stus %}
        学生编号：{{ stu.s_id }}<br>
        学生姓名：{{ stu.s_name }}<br>
        学生年龄：{{ stu.s_age }}<br>
        <br>
    {% endfor %}

    当前页数：{{ paginate.page }}
    总页数：{{ paginate.pages }}
    一共有{{ paginate.total }}条数据
    <br>

    {% if paginate.has_prev %}
        <a href="/stu/stupage/?page={{ paginate.prev_num }}">上一页</a>
    {% endif %}
    页码：
    {% for i in paginate.iter_pages() %}
        <a href="/stu/stupage/?page={{ i }}">{{ i }}</a>
    {% endfor %}

    {% if paginate.has_next %}
        <a href="/stu/stupage/?page={{ paginate.next_num }}">下一页</a>
    {% endif %}
{% endblock %}
```

![](/home/shenyang/Pictures/35.webp)

>**注意**页面中a链接的地址，需要传入参数

##### **访问请求**

!!!首次访问，每页page参数，自动给page赋值1，且当前页数每页上一页

![](/home/shenyang/Pictures/36.png)

!!!点击下一页

![](/home/shenyang/Pictures/37.png)

！！！当跳转到最后一页时，不会显示下一页的链接

![](/home/shenyang/Pictures/38.png)

# 二十一、逻辑运算

```
5.逻辑运算
	（1）与
		    and_     filter(and_(条件))
			huochelist = kaihuoche.query.filter(and_(kaihuoche.id == 1,kaihuoche.name == 'lc'))

	（2）或
			or_          filter(or_(条件))
			huochelist = kaihuoche.query.filter(or_(kaihuoche.id == 1,kaihuoche.name =='lc'))

	（3）非
			not_         filter(not_(条件))  注意条件只能有一个,导包注意是sqlalchemy的包
			huochelist = kaihuoche.query.filter(not_(kaihuoche.id == 1))

	（4）in
		    huochelist = kaihuoche.query.filter(kaihuoche.id.in_([1,2,4]))
```

# 二十二、数据定义

## １、字段类型

```
Integer、String、Text、Unicode、Date、Boolean
```

## ２、约束

```
primary_key：主键
autoincrement：主键自增长
unique：唯一
default：默认
index：索引
not null：非空
ForeignKey：外键、用来约束级联数据
		db.Column( db.Integer, db.ForeignKey(xxx.id) )
		使用relationship实现级联数据获取、声明级联数据、backref="表名"、lazy=True
```

# 二十二、模型关系

## １、一对一

```
class Parent(Base):
    id =db.Column(db.Integer, primary_key=True)
    child_id = db.Column(db.Integer, ForeignKey('child.id'))
    child = relationship("Child", backref=backref("parent", uselist=False)) 

class Child(Base):
    id = db.Column(db.Integer, primary_key=True)
    parent_id = db.Column(db.Integer, ForeignKey('parent.id'))
```

**一对一需要设置relationship中的uselist=Flase，其他数据库操作一样。**

## ２、一对多

```
模型定义
          class Parent(db.Model):
              id=db.Column(db.Integer,primary_key=True,autoincrement=True)
              name=db.Column(db.String(30),unique=True)
              children=db.relationship("Child",backref="parent",lazy=True)
              def __init__(self):
                  name=self.name

          class Child(db.Model):
              id = db.Column(db.Integer, primary_key=True)
              name = db.Column(db.String(30), unique=True)
              parent_id = db.Column(db.Integer, db.ForeignKey('parent.id'))
              def __init__(self):
                  name = self.name
```

```
参数介绍:
 		 1.relationship函数
                    sqlalchemy对关系之间提供的一种便利的调用方式，关联不同的表；
          2.backref参数
                    对关系提供反向引用的声明，在Parent类上声明新属性的简单方法，之后可以在Child.person来获取这个对象的person；
          3.lazy参数
                    （1）'select'（默认值）
                        SQLAlchemy 会在使用一个标准 select 语句时一次性加载数据；
                    （2）'joined'
                        让 SQLAlchemy 当父级使用 JOIN 语句是，在相同的查询中加载关系；
                    （3）'subquery'
                        类似 'joined' ，但是 SQLAlchemy 会使用子查询；
                    （4）'dynamic'：
                        SQLAlchemy 会返回一个查询对象，在加载这些条目时才进行加载数据，大批量数据查询处理时推荐使用。
          4.ForeignKey参数
                    代表一种关联字段，将两张表进行关联的方式，表示一个person的外键，设定上必须要能在父表中找到对应的id值
```

```
（3）模型的应用
            添加
                eg：@blue.route('/add/')
                    def add():
                        p = Parent()
                        p.name = '张三'
                        c = Child()
                        c.name = '张四'
                        c1 = Child()
                        c1.name = '王五'
                        p.children = [c,c1]

                        db.session.add(p)
                        db.session.commit()

                        return 'add success'
            查
                  eg:
                  主查从 --》 Parent--》Child
                  @blue.route('/getChild/')
                  def getChild():
                      clist = Child.query.filter(Parent.id == 1)
                      for c in clist:
                          print(c.name)
                      return 'welcome to red remonce'
                  从查主
                  @blue.route('/getParent/')
                  def getParent():
                      p = Parent.query.filter(Child.id == 2)
                      print(type(p))
                      print(p[0].name)
                      return '开洗'
```

## ３、多对多

```
模型定义
          class User(db.Model):
              id = db.Column(db.Integer,primary_key=True,autoincrement=True)
              name = db.Column(db.String(32))
              age = db.Column(db.Integer,default=18)

          class Movie(db.Model):
              id = db.Column(db.Integer,primary_key=True,autoincrement=True)
              name = db.Column(db.String(32))

          class Collection(db.Model):
              id = db.Column(db.Integer,primary_key=True,autoincrement=True)
              u_id = db.Column(db.Integer,db.ForeignKey(User.id))
              m_id = db.Column(db.Integer,db.ForeignKey(Movie.id))
              num = db.Column(db.Integer,default=1)
```

```
（2）应用场景
          购物车添加
              @blue.route('/getcollection/')
              def getcollection():
                    u_id = int(request.args.get('u_id'))
                    m_id = int(request.args.get('m_id'))
                    c = Collection.query.filter(Collection.u_id == u_id).filter_by(m_id = m_id)

                    if c.count() > 0:
                        print(c.first().u_id,c.first().m_id)
                        # print(c)
                        # print(type(c))
                        # print('i am if')
                        return '已经添加到了购物车中'
                    else:
                        c1 = Collection()
                        c1.u_id = u_id
                        c1.m_id = m_id
                        db.session.add(c1)
                        db.session.commit()
                        return 'ok'
```

# 二十三、flask-bootstrap

```
插件安装
	pip install  flask-bootstrap
ext中初始化
	Bootstrap（app=app）
	
bootstrap案例--bootstrap模板   {% extends ‘bootstrap/base.html’%}
```

# 二十四、flask-debugtoolbar

```
辅助调试插件
安装
	pip install flask-debugtoolbar
初始化  ext 
    app.debug = True (最新版本需要添加)
	debugtoolbar = DebugToolBarExtension()
	debugtoolbar.init_app(app=app)
```

# 二十五、缓存flask-cache

```
缓存目的:缓存优化加载
		减少数据库的ＩＯ操作
实现方案：数据库
		文件
		内存
		内存中的数据库Redis
实现流程：
		（1）从路由函数进入程序
        （2）路由函数到视图函数
        （3）视图函数去缓存中查找
        （4）缓存中找到，直接进行数据返回
        （5）如果没找到，去数据库中查找
        （6）查找到之后，添加到缓存中
        （7）返回到页面上
```

## 安装以及配置

````
(1)安装：pip install flask-cache

(2)初始化：
	cache = Cache(config='CACHE_TYPE':默认是simple)
	#指定使用的缓存方案
	使用：在路由的下面添加＠cache.cached(timeout=30)
	要配置config:TYPE、还可以配置各种缓存的配置信息
	cache = Cache(config={'CACHE_TYPE':默认是simple/'redis'})
    cache.init_app(app=app)	
		
(3)用法：
	    ①：装饰器
                      @cache.cached(timeout=xxx)
                      注意：装饰器必须放在视图函数路由的下面
                      eg：
                      	@blue.route('/helloCache/')
                        @cache.cached(timeout=30)
                        def helloCache():
                            print('这么多年总算看到了秋天')
                            return 'helloCache'
         ②：原生
               get
               set
	

````

# 二十六、钩子

## １、钩子介绍

```
before_first_request：在处理app第一个请求前运行。

before_request：在每次请求前运行。

after_request：如果处理逻辑没有异常抛出，在每次请求后运行。

teardown_request：在每次请求后运行，即使处理发生了错误。

teardown_appcontext：在应用上下文从栈中弹出之前运行
```

## ２、在app对象中的作用

```
#__init__.py（在封装中可以这么使用）
#views.py中的init_blue（）函数中使用
#两个作用范围是所有的蓝图之前或者之后

# 钩子函数 before_first_request
@app.before_first_request
def before_first():
    print("app.before_first")

# 钩子函数 before_request
@app.before_request
def before():
    print("app.before")

# 钩子函数 after_request
@app.after_request
def after(response):
    print("app.after")
    return response

# 钩子函数 teardown_request
@app.teardown_request
def teardown(e):
    print("app.teardown")

        
#在视图函数中通过蓝图对象实现以上功能

# 钩子函数 before_app_first_request（只执行第一次请求，以后的请求不再执行）
@blue.before_app_first_request
def before_first2():
    print("app.before_app_first_request")

# 钩子函数 before_app_request
@blue.before_app_request
def before_first1():
    print("app.before_app_request")

# 钩子函数 after_app_request
@blue.after_app_request
def before_first3(response):
    print("app.after_app_request")
    #response=redirect(url_for('blue.dage'))
    return response

# 钩子函数 teardown_app_request
@blue.teardown_app_request
def before_first4(e):
    print("app.teardown_app_request")
```

## ３、在蓝图对象中使用

```
"""
实现现在当其他蓝图对象的路由接收到用户请求时候，不会执行钩子
只有blue蓝图对象的路由接收到用户请求时候，执行钩子
"""

# 钩子函数 before_first_request
@blue.before_request
def before_first1():
   print("app.before_app_request")

# 钩子函数 before_first_request
@blue.after_request
def before_first3(response):
    print("app.after_app_request")
    #response=redirect(url_for('blue.dage'))
    return response

# 钩子函数 teardown_request
@blue.teardown_request
def before_first4(e):
   print("app.teardown_request")
```

# 二十七、四大内置对象

```
	(1)request
			 请求的所有信息
	(2)session
			 服务端会话技术的接口
	(3)config
              概念：当前项目的配置信息
              (1)模板中可以直接使用
                  config
                    eg:
                    {% for c in config %}
                      <li>{{ c|lower }}</li>
                    {% endfor %}
    		
              (2)在python代码中
                  current_app.config
              	  eg:
                  for c in current_app.config:
                      print(c)
	(4)g
              global  全局
              可以帮助开发者实现跨函数传递数据
              eg:
                  @blue.route('/g/')
                  def g():
                      g.ip = request.remote_addr
                      return 'ok'

                  @blue.route('/testg1/')
                  def testg1():
                      print(g.ip)
                      return 'ok1'
```

# 二十八、路径

````
	BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
	init中app = Flask（__name__,static_folder=static_folder）
		 static_folder=os.path.join(settings.BASE_DIR,'static')
````

# 二十九、flask-restful

```
整合网络和软件的一种架构模式
理解
	Representtational
		表现层
	State Transfer
		状态转换
	表现层状态转换
		资源（Resource）
	每一个URI代表一类资源
		对整个数据的操作
		增删改查
```

## １、前后端分离

```
根据请求提交方式的不同 然后执行对应的方法
http://127.0.0.1/user/1 GET  根据用户id查询用户数据
http://127.0.0.1/user  POST 新增用户
http://127.0.0.1/user  PUT 修改用户信息
http://127.0.0.1/user  DELETE 删除用户信息

推荐使用json数据传输
```

## ２、前后端分离-原生实现

### 概念：

```
概念：就是判断不同的请求方式，实现请求方法
高内聚，低耦合
	高内聚
	相同的数据操作封装在一起
	低耦合
MVC 没有模板--前后端分离
```

```
#视图函数中的借助蓝图，用原生代码实现前后端分离的思想
@blue.route('/user/',methods=['GET','POST','PUT','DELETE'])
def user():
    if request.method == 'GET':
        #一般返回的变量的名字都是data
        data = {
            'message':'ok',
            'status':'200',
        }
        return jsonify(data)
    elif request.method == 'POST':
        data = {
            'message': 'ok',
            'status': '200',
        }
        return jsonify(data),500
    elif request.method == 'PUT':
        data = {
            'message': 'ok',
            'status': '200',
        }
        return jsonify(data)
    elif request.method == 'DELETE':
        data = {
            'message': 'ok',
            'status': '200',
        }
        return jsonify(data)
    else:
        abort(405)
```

### Get:

```
get
		坑---注意：判断请求方式的时候，请求方式必须大写
		eg：
		@blue.route("/users/<int:id>/", methods=["GET", "POST", "PUT", "DELETE", "PATCH"])
        def users(id):
            if request.method == "GET":
                page = int(request.args.get("page", default=1))
                per_page = int(request.args.get("per_page", default=3))

                users = User.query.paginate(page=page, per_page=per_page, error_out=False).items
                users_dict = []
                for user in users:
                    users_dict.append(user.to_dict())

                data = {
                    "message": "ok",
                    "status": "200",
                    "data": users_dict
                }

                return jsonify(data)
```

### Post:

```
post
		eg:
            elif request.method == "POST":
                  # 更新或创建
                  username = request.form.get("username")
                  password = request.form.get("password")

                  data = {
                      "message": "ok",
                      "status": "422"
                  }

                  if not username or not password:
                      data["message"] = "参数不正确"
                      return jsonify(data), 422

                  user = User()
                  user.u_name = username
                  user.u_password = generate_password(password=password)

                  try:

                      db.session.add(user)
                      db.session.commit()
                      data["status"] = "201"
                  except Exception as e:
                      data["status"] = "901"
                      data["message"] = str(e)
                      return jsonify(data), 422

                  return jsonify(data), 201
```

### Put:

```
put
		eg:
			elif request.method == "PUT":
                      username = request.form.get("username")
                      password = request.form.get("password")
                      user = User.query.get(id)

                      user.u_name = username
                      user.u_password = generate_password(password)

                      db.session.add(user)
                      db.session.commit()

                      data = {
                          "message": "update success",
                      }

                      return jsonify(data), 201
```

### delete:

```
delete
		eg:
		    elif request.method == "DELETE":
                    user = User.query.get(id)

                    data = {
                        "message": "delete success"
                    }

                    if user:
                        db.session.delete(user)
                        db.session.commit()
                        return jsonify(data), 204
                    else:
                        data["message"] = "指定数据不存在"
                        return jsonify(data)
```

### Patch:

```

	patch
			eg:
			   elif request.method == "PATCH":
                        password = request.form.get("password")
                        user = User.query.get(id)
                        user.u_password = generate_password(password)

                        data = {
                            "messgage": "update success"
                        }

                        db.session.add(user)
                        db.session.commit()

                        return jsonify(data), 201
```

## ３、restful简介

````
整合网络和软件的一种架构模式、
理解：
    Representtational：表现层
    State Transfer：状态转换
    表现层状态转换：资源（Resource）
    每一个URI代表一类资源：对整个数据的操作、增删改查
RESTful中更推荐使用HTTP的请求谓词（动词）来作为动作标识（GET、POST、PUT、PATCH、DELETE）

http（s）协议
	应该有自己专属域名：在应用上添加一个api前缀
	都是名词，复数形式
	可以将版本号设计进去：增量操作
	/collection/id/：? id=xxx
````

## ４、安装以及使用

```
	（1）安装 
			 pip install flask-restful
	
	（2）初始化 
              创建urls文件
                    1.api = Api()

                    2.def init_urls(app):
                           api.init_app(app=app)
                           注意：在init中调用init_urls

                    3.api.add_resource(Hello, "/hello/")
      注意：Hello是一个类的名字  hello是路由
              
	（3）apis--基本用法
			创建apis文件夹
                    1.继承自Resource
                          class Hello(Resource):
                    2.实现请求方法对应函数
                          def get(self):
                              return {"msg": "ok"}

                          def post(self):
                              return {"msg": "create success"}
                
     （4）乱码问题：init中app.config['JSON_AS_ASCII'] = False
```

## ５、定制输入输出

### (1)结构化输出：按照指定的格式输出数据

```
1.@marshal_with()基本使用1
 案例：
                  r1fields={
                      'msg':fields.String(),
                      'resultCode':fields.Integer
                      'resultValue':fields.String(default='dddd'),
                      'status':fields.String(attribute='xxx')
                  }
             
                  @marshal_with(r1fields)
                  def get(self):
                      data = {
                          'msg':'ok',
                          'status':'200',
                          'xxx':'xxx',
                      }
                      return data
 总结：(1)默认返回的数据如果在预定义结构中不存在，数据会被自动过滤
	  (2)如果返回的数据在预定义的结构中存在，数据会正常返回
	  (3)如果返回的数据比预定义结构中的字段少，预定义的字段会呈现一个默认值
                       如果类型是Integer  那么默认值是  0
                       如果类型是String  那么默认值是null
 	 （4）fields后面的类型 可以加（） 可以不加（）
```

说明：

1. fields中的类型约束

   ​	（1）String

   ​	（2）Integer

   ​	（3）Nested    嵌套

   ​	（4）List

2. fields的约束

   ​         （1）attribute(指定连接对应名字)

   ​				attribute=名字

   ​         （2）default(设置默认值)

   ​				default=404

```
2.@marshal_with()基本使用2
案例：
				r1fields = {
                      'msg': fields.String(),
                      'resultCode': fields.Integer,
                  }

                  class Cat4Resource(Resource):

                      def get(self):
                          data = {
                              'msg':'ok',
                              'status':'200'
                          }
                          return marshal(data=data,fields=r1fields)
```

```
3.@marshal_with返回一个类对象
案例：
				catfields = {
                      'id':fields.Integer,
                      'name':fields.String,
                      'color':fields.String
                  }

                  r1fields = {
                      'msg':fields.String,
                      'cat':fields.Nested(catfields)
                  }

                  class CatResource(Resource):
                      @marshal_with(r1fields)
                      def get(self):
                          cat = Cat.query.first()
                          data = {
                              'msg':'ok',
                              'cat':cat
                          }
                          return data
```

```
4.@marshal_with返回一个列表
案例：			
				catfields = {
                      'id':fields.Integer,
                      'name':fields.String,
                      'color':fields.String,
                  }

                  r1fields = {
                      'msg':fields.String,
                      'cats':fields.List(fields.Nested(catfields))
                  }

                  class CatResource(Resource):
                      def get(self):
                          cats = Cat.query.all()
                          data = {
                              'msg':'ok',
                              'cats':cats
                          }

                          return marshal(data=data,fields=r1fields)
```

### **(2)结构化输入**

```
 使用步骤：  
 		（1）parser=reqparse.RequestParser()
				
	    （2）parser.add_argument("c_name", type=str,required=True, help="c_name必须填写"）	
             parser.add_argument(name="id", type=int, required=True, help="id必须填写")
        		 	 
		（3）parse = parser.parse_args()
				
		（4）cat_name = parse.get("c_name")
        	 id = parse.get("id")
         	 print(id)
         	 
  总结: 
  		name 		获取请求的参数名字
  		type 		请求参数的类型
  		required     必须填写
  		help         如果没有填写报错  
```

