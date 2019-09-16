# Web服务器与Tornado入门

## 一、ＨＴＴＰ服务器的真相

HTTP 协议是建立在 TCP 协议之上的短连接协议。

它利用了 TCP 协议的可靠性,用来传输超文本 (HTML),通信一次连接一次,通信完成后 TCP 连接关闭。

所以如果想创建一个 HTTP Server 需要通过 Socket 搭建一个 服务端程序。

### １、简单的HTTP Server

```
import socket

ADDR = ('0.0.0.0',80)

Response = b'''
HTTP/1.1 200 OK

<!DOCTYPE html>
<html>
	<head>
		<title>Hello</title>
	</head>
	<body>
		<h1 style="text-align: center;">hello word</h1>
	</body>
</html>
'''

listen_socket = socket.socket()   #建立ｓｏｃｋ连接
listen_socket.bind(ADDR) 	      #绑定　ＩＰ：端口
listen_socket.listen(100)    	  #开始监听
ssr
print('Serve is running: %s:%s...' % ADDR)

while True:
	client_socket, client_address = listen_socket.accept()     #接受客户端的连接
	print('client request from %s:%s' % client_addess)
	request = client_socket.recv(1024)   #接受客户端数据
	http_response = RESPONSE
	
	client_socket.sendall(http_response)
	client_socket.close()
```

### ２、对SimpleServer进行扩展

根据不同的URL显示不同页面

页面整体样式不变，根据不同参数，从数据库中取出不同学生的信息，并填充到页面中

## 二、Web框架概述

随着技术的发展，每天的信息量都在迅速增加，传统的静态页面已经跟不上时代的需求，所以催生了动态页面技术

所谓的动态页面，即在所有的页面用程序来生成，以细节实现上的不同，又可以分为“前段动态页面”和“后端动态页面”

我们在Ｗｅｂ前段中所学习到的就是Ａｊａｘ、Ｖｕｅ等技术，就是前端动态页面，而今后我们要学习的是后端动态页面技术和两者的结合

### １、Ｗｅｂ服务器原理

一个完整的ｗｅｂ系统如图所示

![](/home/shenyang/Pictures/20.png)

### ２、常见的ｗｅｂ框架

| web Framework | Description                                                  |
| :------------ | ------------------------------------------------------------ |
| **Django**    | **全能型的框架，大而全，插件丰富, 文档丰富, 社区活跃, 适合快速开发, 内部耦合比较紧** |
| **Flask**     | **微型框架, 适合新手学习, 极其灵活, 便便于二次开发和扩展, 生态环境好, 插件丰富** |
| **Tornado**   | **异步处理, 事件驱动 (epoll), 性能优异**                     |
| Bottle        | 单文件框架, 结构紧凑,适合初学者阅读源码,了解 Web 原理理      |
| web.py        | 代码优美, 适合学习源码                                       |
| Falcon        | 性能优异适合写 API 接口口                                    |
| Quixote       | 一个爷爷级别的框架,著名的豆瓣网用的便是这个                  |
| Sanic         | 后起之秀,性能秒杀以上所有前辈,但没有前辈们稳定。             |

## 三、Tornado入门

Tornado 是有 FriendFeed 公司开发的 Web 框架,该公司已经于 2009 年被 Facebook 收购,原本的
FriendFeed 已经成为了 Facebook 的一部分。
Tornado 最大的特点就是他实现了一个 “异步非阻塞” 的 HTTP Server,性能非常优异。

### １、安装

```
pip install tornado
```

### ２、Hello Word

```
import tornado.ioloop
import tornado.web

class MainHandler(tornado.web.RequestHandler):
    def get(self):
        self.write("Hello, world")
        
def make_app():
    return tornado.web.Application([
        (r"/", MainHandler),
    ])
if __name__ == "__main__":
    app = make_app()
    app.listen(8888)
    tornado.ioloop.IOLoop.current().start()
```

### ３、启动参数

```
from tornado.options import parse_command_line, define, options

define("host", default='0.0.0.0', help="主机地址", type=str)
define("port", default=8888, help="主机端口", type=int)

parse_command_line()
print('你传入的 host: %s' % options.host)
print('你传入的 port: %s' % options.port)
```

### ４、路由处理

```
import tornado.ioloop
from tornado.web import RequestHandler, Application

class HomeHandler(tornado.web.RequestHandler):
    def get(self):
        self.write("欢迎进入主页")
        
class BookHandler(tornado.web.RequestHandler):
    def get(self):
        self.write("你想看的书应有尽有")
        
app = Application([
    ('/', HomeHandler),
    ('/book/', BookHandler),
])

app.listen(8000)
tornado.ioloop.IOLoop.current().start()
```

### ５、处理GET和POST请求

```
class StoryHandler(tornado.web.RequestHandler):
stories = {1: '小红帽', 2: '皮诺曹', 3: '阿拉丁神灯'}

def get(self):
    story_id = self.get_argument('story_id')
    story = self.stories[story_id]
    self.write("你想看 %s 的故事" % story)
    
def post(self):
    pass
```

HTTP的请求方法

| Method  | Description                                                  |
| ------- | ------------------------------------------------------------ |
| POST    | 向指定的资源提交数据请求处理，数据被包含在请求体中           |
| GET     | 请求指定页面信息，并返回实体主体                             |
| PUT     | 从客户端向服务器传送的数据取代指定的文档内容                 |
| DELETE  | 请求服务器删除指定的页面                                     |
| HEAD    | 类似于GET请求，只不过返回的响应没有具体的内容。用于获取报头是 |
| PATVH   | 是对PUT方法的补充，用于对已知资源进行局部更新                |
| OPTIONS | 列举服务器支持的请求方法                                     |







# 数据库与模板系统

## 一、ORM:对象关系映射

### １、概述

ORM 全称是:Object Relational Mapping (对象关系映射)。其主要作用是在编程中把面向对象的概念跟数据库中表的概念对应起来。

举例来说就是,我定义一个类,那就对应着一张表,这个类的实例,就对应着表中的一条记录。

面向对象编程把所有实体看成对象(object),关系型数据库则是采用实体之间的关系(relation)连接数据。

很早就有人提出,关系也可以用用对象表达,这样的话,就能使用面向对象编程,来操作关系型数据库。

ORM 的优点:

- 数据模型都在一个地方定义，更加容易维护和更新，也利于重写代码
- ＯＲＭ有很多现成的工具，很多功能都可以自动完成，比如数据预处理、事务等
- 它迫使你使用ＭＶＣ架构，ＯＲＭ就是天然的ＭＯＤＥＬ,最终使代码更加清晰
- 基于ＯＲＭ的业务代码更加简单，代码量少，语义性好，更加容易理解
- 他不必编写性能不佳的ｓｑｌ

python下常用的ＯＲＭ有：Django-ORM、SALALchemy、Peewee等

### ２、实例

这里使用SQLALchemy来操作数据库

```
import datetime

from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from sqlalchemy import Column, String, Integer, Float, Date
from sqlalchemy.ext.declarative import declarative_base

# 建立连接与数据库的连接
engine = create_engine('mysql+pymysql://shen:123@localhost:3306/tornado')

Base = declarative_base(bind=engine)  # 创建模型的基础类
Session = sessionmaker(bind=engine)   # 创建会话类


class User(Base):
    '''类本身对应数据库里的表结构'''
    __tablename__ = 'user'

    id = Column(Integer, primary_key=True, autoincrement=True)
    name = Column(String(20), unique=True)
    birthday = Column(Date, default=datetime.date(1990, 1, 1))
    city = Column(String(10), default='上海')


Base.metadata.create_all()  # 创建表结构


# 定义的每一个对象，对应数据库里的一行数据
bob = User(name='bob', birthday=datetime.date(1990, 3, 21), city='上海')
tom = User(name='tom', birthday=datetime.date(1995, 9, 12))
lucy = User(name='lucy', birthday=datetime.date(1998, 5, 14), city='北京')
jam = User(name='jam', birthday=datetime.date(1994, 3, 9), city='深圳')
alex = User(name='alex', birthday=datetime.date(1992, 3, 17), city='北京')
eva = User(name='eva', birthday=datetime.date(1987, 7, 28), city='深圳')
rob = User(name='rob', birthday=datetime.date(1974, 2, 5), city='上海')
ella = User(name='ella', birthday=datetime.date(1999, 5, 26), city='北京')


```

**ORM的具体操作**

```
# 增加数据
session.add_all([bob, tom, lucy, jam]) # 在 Session 中记录操作
session.commit() # 提交到数据库中执行

# 删除数据
session.delete(jam) # 记录删除操作
session.commit() # 提交到数据库中执行

#修改数据
tom.money = 270 # 修改数据
session.commit() # 提交到数据库中执行

# 查询数据
u_query = session.query(User)
# 先定义表的查询对象

# 直接获取主键(ID)为 5 的数据
user = u_query.get(5)
print(user.id, user.name)

# 使用 filter_by 按条件查询
user = u_query.filter_by(id=7).one()
print(user.id, user.name, user.birthday)

# 使用 filter 进行范围查询,并对结果进行排序
users = u_query.filter(User.id>2).order_by('birthday')
for u in users:
print(u.name, u.birthday, u.money)

# 根据查询结果进行更新
users.update({'money': User.money - 1}, synchronize_session=False)
sessiom.commit()

# 按数量取出数据: limit / offset
users = u_query.limit(3).offset(4)
for u in users:
print(u.id, u.name)

# 计数
num = u_query.filter(User.money>200).count()
print(num)

# 检查是否存在
exists = q.filter_by(name='Seamile').exists()
result = session.query(exists).scalar()
print(result)
```





## 二、Tornado的模板系统

模板系统是为了更快速、更方便便的生产大量的页面而设计的一套程序。

借助模板系统,我们可以先写好⻚面大概的样子,然后预留好数据的位置,再然后将我们需要的数据,按照既定规则拼到模板中的指定位置,然后渲染出完整⻚面。

现代的模板系统已经相当成熟,甚至可以通过 if...else 、 for 等语句句在模板中写出简单的逻辑控制。

### １、模板与静态文件的路径配置

在定义ＡＰＰ时，在ａｐｐｌｉｃａｔｉｏｎ中定义，可以是相对路径，也可以是绝对路径

```
app = Application(
    template_path = 'templates',   # 模版路径
    static_path = 'statics'   # 静态文件路径
)
```

### ２、模板中的变量

模板中，变量和表达式使用｛｛......｝｝包围，可以写入任何的ｐｙｔｈｏｎ表达式或者变量

```
<!DOCTYPE html>
<html lang='en'>
    <head>
        <meta charset='UTF-8'>
        <title>Templates</title>
    </head>
    
    <body>
        <div>你好 {{ name }},欢迎回来!</div>
        <div>猜一猜,3 x 2 等于几?</div>
        <div>我就不不告诉你等于 {{ 3 * 2 }}</div>
    </body>
</html>
```

### ３、从python程序中传递参数

```
class MainHandler(tornado.web.RequestHandler):
    def get(self):
        name = 'Tom'
        say = "Hello, world"
        self.render('index.html', name=name, say=say)
```

### ４、模板中的if....else结构

**模板中的控制语句使用｛%......%｝包围**

```
<p>
    根据您的条件我们进行了筛选
    {% if 条件 %}
        <div>第 1 条数据</div>
        <div>第 2 条数据</div>
        <div>。。。</div>
    {% else %}
        <div>抱歉我们没有找到合适的内容</div>
    {% end %}
</p>
```

### ５、模板中的for循环

Ｐｙｔｈｏｎ程序中

```
class MainHandler(tornado.web.RequestHandler):
    def get(self):
        students = ["Lucy", "Tom", "Bob"]
        self.render("student.html", students=students)
```

页面中

```
<html>
    <head>
        <title>学生信息</title>
    </head>
    <body>
        <ul>
            {% for student in students %}
                <li>{{ student }}</li>
            {% end %}
        </ul>
    </body>
</html>
```

### ６、静态文件

⻚面中静态文件的路径需要以 '/static/' 开头, 后面跟文件路径

![](/home/shenyang/Pictures/21.png)

在模板中使用静态文件时，静态文件的路径格式如下

```
<img class="avatar" src="/static/img/coder.jpg" />
```

### ７、模板的继承

网站中,大多数⻚面都是同样的结构和风格,我们没有必要在所有⻚面中把相同的样式重复的写很多遍。

Tornado 为我们提供了模板的继承机制,只需要写好父模板,然后让其他模板继承一下即可

**父模板**文件名经常定义为 "base.html"

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %} 通用标题 {% end %}</title>
</head>
<body>
    {% block body %}{% end %}
</body>
</html>
```

**子模板**

```
{% extends "base.html" %}

{% block title %} 子⻚面的标题 {% end %}

{% block body %}
<div>
    子⻚面里的内容
    Bala Bala
</div>
{% end %}
```

# 虚拟环境与Git

## 一、MVC网站架构

![](/home/shenyang/Pictures/22.png)

MVC模式(Model–view–controller)是软件工程中的一种软件架构模式, 把软件系统分为三个基本部分:

- 模型 (Model), 它是程序需要操作的数据或信息。
- 视图 (View), 它提供给用户的操作界面, 是程序的外壳。
- 控制器 (Controller), 它负责根据用户从"视图层"输入的指令, 选取"数据层"中的数据, 然后对其进行相应的操作, 产生最终结果。

这种模式特点是构建简单，层次清晰，代码可复用性好，模块之间耦合度低

对应到我们的服务器程序，简单来说，就是一些模块只负责前段页面显示，另一些模块只负责数据模型的定义的数据操作，其他模块负责连接这两个部分，并进行必要的逻辑处理

对应到程序的细节

我们可以按照程序的功能不同，分为３个模块

![](/home/shenyang/Pictures/23.png)

## 二、虚拟环境

实际工作中,我们可能同时要维护若干个项目,每个项目使用的软件包、版本可能都不一样,比如项目A 使用 tornado 4.3,而项目 B 使用 tornado 6.0 版,这时如果将两个版本同时装到全局的 Python 环境下就会冲突。

所以我们要为不同的项目单独设置它运行所需的环境,这就需要借助虚拟环境管理。

- ### **安装**

  ```
  pip install virtualenv
  ```

- ### 创建虚拟环境

  ```
  cd ~/你的项目文件夹
  
  # 创建虚拟环境
  # 虚拟环境可以创建到任何位置,但一般与项目文件夹放到一一起
  virtualenv .venv
  ```

- ### 加载虚拟环境

  ```
  source ~/项目文件夹/.venv/bin/activate   # 激活虚拟环境
  ```

- ### 退出虚拟环境

  ```
  deactivate   # 当开发完成后,可以退出当前虚拟环境
  ```

## 三、版本控制工具与Git

### １、**版本控制工具的作用**

1. 能够追踪全部代码的状态
2. 能够进行版本之间的差异对比
3. 能够进行版本回滚
4. 能够协助多个开发者进行代码合并

### ２、常见的版本控制工具

- CVS:基本退出了历史的舞台
- svn：中心化的版本控制工具，需要有一台服务器

![](/home/shenyang/Pictures/24.png)



- git：分布式的版本控制工具，中心服务器不再是必须的

![](/home/shenyang/Pictures/25.png)

- hg:　纯python开发的版本控制工具
- Github: 依托Git二创建的一个平台，有独立的公司在运作
- 备注：所有文本类的东西都可以由版本控制工具来管理

### Git的历史

Git 最初由 Linus 为了维护 Linux 内核源码而开发。
Linus 当时因不堪忍受早期版本控制工具的各种问题,最终决定自己开发了一个,并且将它开源出来,供所有人使用。

#### １、起步

- 配置自己的账号和邮箱

  ```
  git config --global user.name '你的名字'
  git config --global user.email '你的邮箱'
  ```

- 设置要忽略的文件

  对于不需要让Git追踪的的文件可以在项目目录下创建.gitignore文件

  ```
  touch .gitignore
  ```

  .gitignore文件中可以写需要忽略的文件名，或者是某一类文件的通配符，如：

  ```
  *.pyc
  *.log
  *.sqlite3
  .DS_Store
  .venv/
  .idea/
  __pycache__/
  ```

#### ２、必须要掌握的GIt命令

| Command  | Description                    | 与远程通信 | 操作示例                         |
| -------- | ------------------------------ | ---------- | -------------------------------- |
| init     | 在本地初始化一个新的仓库       | －         | git init                         |
| add      | 添加到暂存区                   | －         | git add aaa bbb ccc/             |
| commit   | 将暂存区的修改提交到本地仓库   | －         | git commit -m '注释'             |
| push     | 将本地仓库的内容推送到远程仓库 | 有         | git push                         |
| pull     | 将远程仓库的更新拉取到本地仓库 | 有         | git pull                         |
| clone    | 将远程仓库克隆到本地           | 有         | git clone http://test.cn/bar.git |
| branch   | 管理分支                       | －         | git branch 分支名                |
| checkout | 切换分支/代码回滚/代码还原     | －         | git checkout 分支名　/ 提交      |
| diff     | 不同版本之间进行差异对比       | －         | git diff　 版本１　版本２        |
| merge    | 合并两个分支                   | －         | git merge 其他分支名             |
| status   | 查看当前分支的状态             | －         | git status                       |
| log      | 查看提交历史                   | －         | git log                          |
| reset    | 代码重置/代码回滚              | －         | git reset                        |
| blame    | 检查每行代码最后一次是谁修改的 | －         | git blame 文件名                 |

```

1. 配置
git config - -global user.name 'xxxx'
git config - -global user.email 'xxxx@yyy.com'

2. 增加了 .gitignore, 忽略不需要追踪的文件

3. git init  # 对仓库进行初始化，产生了一个 .git 的目录，这个文件夹就是本地仓库

4. git add ./  # 将当前文件夹下的所有文件添加到 “暂存区”

5. git reset xxx  # 将 “暂存区” 中的文件取消暂存状态

6. git commit - m '完成管理系统'  # 将 “暂存区” 中的代码提交到本地仓库

7. git push - u origin master  # 将本地仓库推送到远程仓库

8. ssh-keygen  # 在 ~/.ssh 目录下生成一对公钥和密钥

9. 将公钥内容复制到 Github

10. git pull  # 将远程仓库的更新，拉取到本地仓库

    A - ------ ->
       /          \
------------ -> * -----*--------*---- ->
 /
    B - -----------------*--->
```

```
解决冲突
​```shell
git push     #发现与别人修改的代码有冲突
gti pull     #将线上代码拉取到本地
gti status   #找到冲突文件都有哪些，冲突文件的状态是：both modified

#然后逐一打开冲突文件，按照冲突标记逐行解决冲突
＃冲突标记一般为
＃　　　　　>>>>>>>HEAD 
#         hello word
#         =======
#         hello shanghai
#         <<<<<<<

#冲突代码解决后，将代码中冲突的标记删除

git add ./
git commit -m '解决冲突，进行了一次合并'
git push
。。。
```

#### ３、游戏练习Git

<https://learngitbranching.js.org/>

# Redis 与　MongoDB

## 一、NoSQL概述

如今,大多数的计算机系统(包括服务器器、PC、移动设备等)都会产生庞大的数据量。其实,早在2012年的时候,全世界每天产生的数据量就达到了2.5EB(艾字节,)。这些数据有很大一部分是由关系型数据库来存储和管理的。实践证明,关系型数据库是实现数据持久化最为重要的方式,它也是大多数应用在选择持久化方案时的首选技术。
NoSQL 是一项全新的数据库革命性运动,虽然它的历史可以追溯到1998年,但是NoSQL真正深入人心并得到广泛的应用是在进入大数据时候以后,业界普遍认为NoSQL是更适合大数据存储的技术方案,这才使得NoSQL的发展达到了前所未有的高高度。2012年年《纽约时报》的一篇专栏中写到,大大数据时代已经降临,在商业、经济及其他领域中,决策将不再基于经验和直觉而基于数据和分析而作出。事实上,在天文学、气象学、基因组学、生物学、社会学、互联网搜索引擎、金融、医疗、社交网络、电子商务等诸多领域,由于数据过于密集和庞大,在数据的分析和处理理上也遇到了前所未有的限制和阻碍,这一切都使得对大数据处理技术的研究被提升到了新的高度,也使得各种NoSQL的技术方案进入到了公众的视野。

NoSQL数据库按照其存储类型可以大致分为以下几类:

------

| 类型       | 部分代表                         | 特点                                                         |
| ---------- | -------------------------------- | ------------------------------------------------------------ |
| 列族数据库 | HBase   Cassandra  Hypertable    | 顾名思义是按列存储数据的。最大的特点是方便存储结构化和半结构化数据，方便做数据压缩，对针对某一列或者某几列的查询有非常大的I/O优势，适合于批量数据处理和实时查询 |
| 文档数据库 | MongoDB   CouchDB  ElasticSearch | 文档数据库一般用类JSON格式存储数据,存储的内容是文档型的。这样也就有机会对某些字段建立索引,实现关系数据库的某些功能,但不提供对参照完整性和分布事务的支持 |
| kv数据库   | DynamoDB   Redis   LevelDB       | 可以通过key快速查询到其value,有基于内存和基于磁盘两种实现方案 |
| 图数据库   | Neo4j   FlockDB  janusGraph      | 使用图结构进行语义查询的数据库,它使用节点、边和属性来表示和存储数据。图数据库从设计上,就可以简单快速的检索难以在关系统中建模的复杂层次结构 |
| 对象数据库 | db4o   Versant                   | 通过类似面向对象语言的语法操作数据库,通过对象的方式存取数据  |

## 二、Redis的入门

Redis 是一种基于键值对的NoSQL数据库,它提供了对多种数据类型(字符串、哈希、列列表、集合、有序集合、位图等)的支持,能够满足很多应用场景的需求。Redis将数据放在内存中,因此读写性能是非常惊人的。与此同时,Redis也提供了持久化机制,能够将内存中的数据保存到硬盘上,在发生意外状况时数据也不会丢掉。此外,Redis还支持键过期、地理理信息运算、发布订阅、事务、管道、Lua脚本扩展等功能,总而而言之,Redis的功能和性能都非常强大,如果项目中要实现高速缓存和消息队列这样的服务,直接交给Redis就可以了。目前,国内外很多著名的企业和商业项目都使用了Redis,包括:Twitter、Github、StackOverflow、新浪微博、百度、优酷土豆、美团、小米、唯品会等。

### １、Redis简介

2008年年,一个名为Salvatore Sanfilippo的程序员为他开发的LLOOGG项目定制了专属的数据库(因为之前他无论怎样优化MySQL,系统性能已经无法再提升了,这项工作的成果就是Redis的初始版本。后来他将Redis的代码放到了全球最大的代码托管平台Github,从那以后,Redis引发了大量开发者的好评和关注,继而有数百人参与了Redis的开发和维护,这使得Redis的功能越来越强大和性能越来越好。

Redis是 remote dictionary server 的缩写,它是一个用 ANSI C 编写的高性能的key-value存储系统,与其他的key-value存储系统相比比,Redis有以下一些特点(也是优点):

- Redis的读写性能极高,并且有丰富的特性(发布/订阅、事务、通知等)。
- Redis支持数据的持久化(RDB和AOF两种方式),可以将内存中的数据保存在磁盘中,重启的时候可以再次加载进行使用。
- Redis支持多种数据类型,包括:string、hash、list、set,zset、bitmap、hyperloglog等
- Redis支持主从复制(实现读写分析)以及哨兵模式(监控master是否宕机并自动调整配置)
- Redis支持分布式集群,可以很容易的通过水平扩展来提升系统的整体性能。
- Redis基于TCP提供的可靠传输服务进行通信,很多编程语言都提供了Redis客户端支持

### ２、Redis的应用场景

- 高速缓存 - 将不常变化但又经常被访问的热点数据放到Redis数据库中,可以大大降低关系型数据库的压力,从而提升系统的响应性能。
- 排行榜 - 很多网站都有排行榜功能,利用Redis中的列表和有序集合可以非常方便的构造各种排行榜系统。
- 商品秒杀/投票点赞 - Redis提供了对计数操作的支持,网站上常⻅的秒杀、点赞等功能都可以利用Redis的计数器通过+1或-1的操作来实现,从而避免了使用关系型数据的 update 操作。
- 分布式锁 - 利用Redis可以跨多台服务器实现分布式锁(类似于线程锁,但是能够被多台机器上的多个线程或进程共享)的功能,用于实现一个阻塞式操作。
- 消息队列 - 消息队列和高速缓存一样,是一个大型网网站不可缺少的基础服务,可以实现业务解耦和非实时业务削峰等特性,这些我们都会在后面的项目中为大家展示。

### ３、Redis的安装和配置

可以使用 Linux 系统的包管理工具 apt 来安装 Redis: apt install redis

也可以通过在Redis的 官方网站 下载 Redis 的源代码,解压缩解归档之后通过 make 工具对源代码进行构建并安装。

```
wget http://download.redis.io/releases/redis-5.0.5.tar.gz
tar -xvf redis-5.0.5.tar
cd redis-5.0.5
make && make install
```

### ４、Redis的配置

在 redis 源代码目录下有一个名为redis.conf的配置文件,我们可以先查看一下该文件: vim　redis.conf

1. 配置将 Redis 服务绑定到指定的IP地址和端口。

```
bind 127.0.0.1
port 6379
```

2. 设置后台运行 (以守护进程方式运行)

```
daemonize yes
```

3. 设置日志级别, 可选值: ( debug : 调试, verbose : 详细, notice : 通知, warning : 警告)

```
loglevel warning
```

4. 配置数据库的数量, 默认为 16 个

```
databases 16
```

5. 配置数据写入规则

```
save 900 1 # 900 秒 (15 分钟) 内修改过 1 个 key, , 写入一次数据库
save 300 10 # 300 秒 (5 分钟) 内修改过 10 个 key, 写入一次数据库
save 60 10000 # 60 秒 (1 分钟) 内修改过 10000 个 key, 写入一次数据库
```

6. 配置Redis的持久化机制 - RDB。

```
rdbcompression yes # 压缩 RDB 文件
rdbchecksum yes # 对 RDB 文件进行校验
dbfilename dump.rdb # RDB 数据库文件的文件名
dir ./ # RDB 文件保存的目录
```

7. 配置Redis的持久化机制 - AOF。

```
appendonly no
appendfilename "appendonly.aof"
```

8. 配置Redis的主从复制,通过主从复制可以实现读写分离。

```
# Master-Replica replication. Use replicaof to make a Redis instance a
copy of
# another Redis server. A few things to understand ASAP about Redis
replication.

#	+------------------+	+---------------+
#	|		Msater		|	|	Rwplica		|
#	|	receive write	|	|	(exect copy) |
#	+-------------------+	+----------------+
#
# 1) 	Redis replication is asynchronous, but you can configure a master to stop accepting writes if it appears to be not connected with at least a given number of replicas.
# 2) 	Redis replicas are able to perform a partial resynchronization with the
#	master if the replication link is lost for a relatively small amount
of
#	time. You may want to configure the replication backlog size (see the next
#	sections of this file) with a sensible value depending on your needs.
# 3) 	Replication is automatic and does not need user intervention. #	After a network partition replicas automatically try to #reconnect to masters and resynchronize with them.
#
replicaof 主机IP地址 主机端口
```

9. 配置慢查询。

```
slowlog-log-slower-than 10000 # 一次操作超过 10000 毫秒被视作一次慢查询
slowlog-max-len 128 # 最多纪录 128 次满查询
```

### ５、Redis的服务器和客户端

接下来启动 Redis 服务器,下面的方式将以指定的配置文件启动 Redis 服务。

```
redis-server redis.conf
```

接下来用 Redis 客户端去连接服务器。

```
redis-cli -h localhost -p 6379
```

Redis有着非常丰富的数据类型,也有很多的命令来操作这些数据,具体的内容可以查看Redis命令参考,在这个网站上,除了了Redis的命令参考,还有Redis的详细文档,其中包括了通知、事务、主从复制、持久化、哨兵、集群等内容。

![](/home/shenyang/Pictures/26.png)

```
127.0.0.1:6379> set username admin
OK
127.0.0.1:6379> get username
"admin"
127.0.0.1:6379> set password "123456" ex 300
OK
127.0.0.1:6379> get password
"123456"
127.0.0.1:6379> ttl username
(integer) -1
127.0.0.1:6379> ttl password
(integer) 286
127.0.0.1:6379> hset stu1 name hao
(integer) 0
127.0.0.1:6379> hset stu1 age 38
(integer) 1
127.0.0.1:6379> hset stu1 gender male
(integer) 1
127.0.0.1:6379> hgetall stu1
1) "name"
2) "hao"
3) "age"
4) "38"
5) "gender"
6) "male"
127.0.0.1:6379> hvals stu1
1) "hao"
2) "38"
3) "male"
127.0.0.1:6379> hmset stu2 name wang age 18 gender female tel 13566778899
OK
127.0.0.1:6379> hgetall stu2
1) "name"
2) "wang"
3) "age"
4) "18"
5) "gender"
6) "female"
7) "tel"
8) "13566778899"
127.0.0.1:6379> lpush nums 1 2 3 4 5
(integer) 5
127.0.0.1:6379> lrange nums 0 -1
1) "5"
2) "4"
3) "3"
4) "2"
5) "1"
127.0.0.1:6379> lpop nums
"5"
127.0.0.1:6379> lpop nums
"4"
127.0.0.1:6379> rpop nums
"1"
127.0.0.1:6379> rpop nums
"2"
127.0.0.1:6379> sadd fruits apple banana orange apple grape grape
(integer) 4
127.0.0.1:6379> scard fruits
(integer) 4
127.0.0.1:6379> smembers fruits
1) "grape"
2) "orange"
3) "banana"
4) "apple"
127.0.0.1:6379> sismember fruits apple
(integer) 1
127.0.0.1:6379> sismember fruits durian
(integer) 0
127.0.0.1:6379> sadd nums1 1 2 3 4 5
(integer) 5
127.0.0.1:6379> sadd nums2 2 4 6 8
(integer) 4
127.0.0.1:6379> sinter nums1 nums2
1) "2"
2) "4"
127.0.0.1:6379> sunion nums1 nums2
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"
6) "6"
7) "8"
127.0.0.1:6379> sdiff nums1 nums2
1) "1"
2) "3"
3) "5"
127.0.0.1:6379> zadd topsinger 5234 zhangxy 1978 chenyx 2235 zhoujl 3520 xuezq
(integer) 4
127.0.0.1:6379> zrange topsinger 0 -1 withscores
1) "chenyx"
2) "1978"
3) "zhoujl"
4) "2235"
5) "xuezq"
6) "3520"
7) "zhangxy"
8) "5234"
127.0.0.1:6379> zrevrange topsinger 0 -1
1) "zhangxy"
2) "xuezq"
3) "zhoujl"
4) "chenyx"
127.0.0.1:6379> geoadd pois 116.39738549206541 39.90862689286386 tiananmen
116.27172936413572 39.99
135172904494 yiheyuan 117.27766503308104 40.65332064313784 gubeishuizhen
(integer) 3
127.0.0.1:6379> geodist pois tiananmen gubeishuizhen km
"111.5333"
127.0.0.1:6379> geodist pois tiananmen yiheyuan km
"14.1230"
127.0.0.1:6379> georadius pois 116.86499108288572 40.40149669363615 50 km
withdist
1) 1) "gubeishuizhen"
2) "44.7408"
```

### ６、在Python程序中使用Redis

可以使用pip安装redis模块。redis模块的核心是名为Redis的类,该类的对象代表一个Redis客户端,通过该客户端可以向Redis服务器发送命令并获取执行的结果。上面我们在Redis客户端中使用的命令基本上就是Redis对象可以接收的消息,所以如果了解了Redis的命令就可以在Python中玩转Redis。

```
>>> import redis
>>> client = redis.Redis(host='1.2.3.4', port=6379, password='1qaz2wsx')
>>> client.set('username', 'admin')
True
>>> client.hset('student', 'name', 'hao')
1
>>> client.hset('student', 'age', 38)
1
>>> client.keys('*')
[b'username', b'student']
>>> client.get('username')
b'admin'
>>> client.hgetall('student')
{b'name': b'hao', b'age': b'38'}
```

## 三、MongoDB概述

### １、MongoDB简介

MongoDB是2009年年问世的一个面向文档的数据库管理理系统,由 C++ 语言编写,旨在为Web应用提供可扩展的高性能数据存储解决方案。虽然在划分类别的时候后,MongoDB被认为是NoSQL的产品,但是它更像一介于关系数据库和非关系数据库之间的产品,在非关系数据库中它功能最丰富,最像关系数据库。

MongoDB将数据存储为一个文档,一个文档由一系列的“键值对”组成,其文档类似于JSON对象,但是MongoDB对JSON进行了二进制处理理(能够更更快的定位key和value),因此其文档的存储格式称为BSON。关于JSON和BSON的差别大家可以看看MongoDB官方网站的文章《JSON and BSON》

[https://www.mongodb.com/json-and-bson]: 

。

目前,MongoDB已经提供了对Windows、MacOS、Linux、Solaris等多个平台的支持,而而且也提供了多种开发语言的驱动程序,Python当然是其中之一。

### ２、MongoDB的安装和配置

可以从MongoDB的官方下载链接下载

[https://www.mongodb.com/download-center/community]: 

MongoDB,官方方为Windows系统提供了一个Installer程序,而Linux和MacOS则提供了了压缩文件。下面简单说一下Linux系统如何安装和配置MongoDB。

```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-amazon-3.6.5.tgz
gunzip mongodb-linux-x86_64-amazon-3.6.5.tgz
mkdir mongodb-3.6.5
tar -xvf mongodb-linux-x86_64-amazon-3.6.5.tar --strip-components 1 -C
mongodb-3.6.5/
export PATH=$PATH:~/mongodb-3.6.5/bin
mkdir -p /data/db
mongod --bind_ip 172.18.61.250
2018-06-03T18:03:28.232+0800 I CONTROL
[initandlisten] MongoDB starting :
pid=1163 port=27017 dbpath=/data/db 64-bit host=iZwz97tbgo9lkabnat2lo8Z
2018-06-03T18:03:28.232+0800 I CONTROL [initandlisten] db version v3.6.5
2018-06-03T18:03:28.232+0800 I CONTROL [initandlisten] git version:
a20ecd3e3a174162052ff99913bc2ca9a839d618
2018-06-03T18:03:28.232+0800 I CONTROL
OpenSSL 1.0.0-fips29 Mar 2010
...
2018-06-03T18:03:28.945+0800 I NETWORK
[initandlisten] waiting for
connections on port 27017
```

------

**说明:**上面的操作中,export命令是设置PATH环境变量,这样可以在任意路径下执行mongod来启动MongoDB服务器器。MongoDB默认保存数据的路路径是/data/db目录,为此要提前创建该目录。此外,在使用mongod启动MongoDB服务器器时,--bind_ip参数用来将服务绑定到指定的IP地址,也可以用--port参数来指定端口,默认端口为27017。

### ３、MongoDB基本概念

我们通过与关系型数据库进行对照的方式来说明MongoDB中的一些概念。

| ＳＱＬ      | MongoDB     | 解释（ＳＱＬ/MongoDB） |
| ----------- | ----------- | ---------------------- |
| datebase    | batebase    | 数据库/数据库          |
| table       | collection  | 二维表/集合            |
| row         | document    | 记录(行)/文档          |
| column      | field       | 字段(列)/域            |
| index       | index       | 索引/索引              |
| table joins | ---         | 表连接/嵌套文档        |
| primary key | primary key | 主键/主键( _id 字段)   |

### ４、通过Shell操作MongoDB

启动服务器后可以使用交互式环境跟服务器通信,如下所示。

```
mongo --host 172.18.61.250
MongoDB shell version v3.6.5
connecting to: mongodb://172.18.61.250:27017/
```

#### (1)查看、创建和删除数据库。

```
> // 显示所有数据库
> show dbs
admin 0.000GB
config 0.000GB
local 0.000GB
> // 创建并切换到school数据库
> use school
switched to db school
> // 删除当前数据库
> db.dropDatabase()
{ "ok" : 1 }
>
```

#### (2)创建、删除和查看集合。

```
> // 创建并切换到school数据库
> use school
switched to db school
> // 创建colleges集合
> db.createCollection('colleges')
{ "ok" : 1 }
> // 创建students集合
> db.createCollection('students')
{ "ok" : 1 }
> // 查看所有集合
> show collections
colleges
students
> // 删除colleges集合
> db.colleges.drop()
true
>
```

**说明:**在MongoDB中插入文档时如果集合不存在会自动创建集合,所以也可以按照下面的方式通过创建文档来创建集合。

#### (3)文档的CRUD操作。

```
> // 向students集合插入文档
> db.students.insert({stuid: 1001, name: '骆昊', age: 38})
WriteResult({ "nInserted" : 1 })
> // 向students集合插入文档
> db.students.save({stuid: 1002, name: '王大大锤', tel: '13012345678',
gender: '男'})
WriteResult({ "nInserted" : 1 })
> // 查看所有文档
> db.students.find()
{ "_id" : ObjectId("5b13c72e006ad854460ee70b"), "stuid" : 1001, "name" :
"骆昊", "age" : 38 }
{ "_id" : ObjectId("5b13c790006ad854460ee70c"), "stuid" : 1002, "name" :
"王大大锤", "tel" : "13012345678", "gender" : "男" }
> // 更新stuid为1001的文档
> db.students.update({stuid: 1001}, {'$set': {tel: '13566778899', gender:
'男'}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> // 插入入或更新stuid为1003的文档
> db.students.update({stuid: 1003}, {'$set': {name: '白元芳', tel:
'13022223333', gender: '男'}},
upsert=true)
WriteResult({
"nMatched" : 0,
"nUpserted" : 1,
"nModified" : 0,
"_id" : ObjectId("5b13c92dd185894d7283efab")
})
> // 查询所有文档
> db.students.find().pretty()
{
"_id" : ObjectId("5b13c72e006ad854460ee70b"),
"stuid" : 1001,
"name" : "骆昊",
"age" : 38,
"gender" : "男",
"tel" : "13566778899"
}
{
"_id" : ObjectId("5b13c790006ad854460ee70c"),
"stuid" : 1002,
"name" : "王大锤",
"tel" : "13012345678",
"gender" : "男"
}
{
"_id" : ObjectId("5b13c92dd185894d7283efab"),
"stuid" : 1003,
"gender" : "男",
"name" : "白元芳",
"tel" : "13022223333"
}
> // 查询stuid大于1001的文档
> db.students.find({stuid: {'$gt': 1001}}).pretty()
{
"_id" : ObjectId("5b13c790006ad854460ee70c"),
"stuid" : 1002,
"name" : "王大锤",
"tel" : "13012345678",
"gender" : "男"
}
{
"_id" : ObjectId("5b13c92dd185894d7283efab"),
"stuid" : 1003,
"gender" : "男",
"name" : "白元芳",
"tel" : "13022223333"
}
> // 查询stuid大于1001的文档只显示name和tel字段
> db.students.find({stuid: {'$gt': 1001}}, {_id: 0, name: 1, tel:
1}).pretty()
{ "name" : "王大锤", "tel" : "13012345678" }
{ "name" : "白元芳", "tel" : "13022223333" }
> // 查询name为“骆昊”或者tel为“13022223333”的文文档
> db.students.find({'$or': [{name: '骆昊'}, {tel: '13022223333'}]}, {_id:
0, name: 1, tel: 1}).pretty()
{ "name" : "骆昊", "tel" : "13566778899" }
{ "name" : "白元芳", "tel" : "13022223333" }
> // 查询学生文档跳过第1条文档只查1条文档
> db.students.find().skip(1).limit(1).pretty()
{
"_id" : ObjectId("5b13c790006ad854460ee70c"),
"stuid" : 1002,
"name" : "王大锤",
"tel" : "13012345678",
"gender" : "男"
}
> // 对查询结果进行排序(1表示升序,-1表示降序)
> db.students.find({}, {_id: 0, stuid: 1, name: 1}).sort({stuid: -1})
{ "stuid" : 1003, "name" : "白元芳" }
{ "stuid" : 1002, "name" : "王大锤" }
{ "stuid" : 1001, "name" : "骆昊" }
> // 在指定的一个或多个字段上创建索引
> db.students.ensureIndex({name: 1})
{
"createdCollectionAutomatically" : false,
"numIndexesBefore" : 1,
"numIndexesAfter" : 2,
"ok" : 1
}
>}
{
"_id" : ObjectId("5b13c92dd185894d7283efab"),
"stuid" : 1003,
"gender" : "男",
"name" : "白元芳",
"tel" : "13022223333"
}
> // 查询stuid大于1001的文档只显示name和tel字段
> db.students.find({stuid: {'$gt': 1001}}, {_id: 0, name: 1, tel:
1}).pretty()
{ "name" : "王大锤", "tel" : "13012345678" }
{ "name" : "白元芳", "tel" : "13022223333" }
> // 查询name为“骆昊”或者tel为“13022223333”的文文档
> db.students.find({'$or': [{name: '骆昊'}, {tel: '13022223333'}]}, {_id:
0, name: 1, tel: 1}).pretty()
{ "name" : "骆昊", "tel" : "13566778899" }
{ "name" : "白元芳", "tel" : "13022223333" }
> // 查询学生生文档跳过第1条文档只查1条文档
> db.students.find().skip(1).limit(1).pretty()
{
"_id" : ObjectId("5b13c790006ad854460ee70c"),
"stuid" : 1002,
"name" : "王大锤",
"tel" : "13012345678",
"gender" : "男"
}
> // 对查询结果进行排序(1表示升序,-1表示降序)
> db.students.find({}, {_id: 0, stuid: 1, name: 1}).sort({stuid: -1})
{ "stuid" : 1003, "name" : "白元芳" }
{ "stuid" : 1002, "name" : "王大锤" }
{ "stuid" : 1001, "name" : "骆昊" }
> // 在指定的一个或多个字段上创建索引
> db.students.ensureIndex({name: 1})
{
"createdCollectionAutomatically" : false,
"numIndexesBefore" : 1,
"numIndexesAfter" : 2,
"ok" : 1
}
>
```

使用MongoDB可以非常方便的配置数据复制,通过冗余数据来实现数据的高可用以及灾难恢复,也可以通过数据分片片来应对数据量迅速增长的需求。关于MongoDB更多的操作可以查阅官方文档 

[https://mongodb-documentation.readthedocs.io/en/latest/]: 

,同时推荐大家阅读Kristina Chodorow写的《MongoDB权威指南》

[https://www.ituring.com.cn/book/1172]: 



### ５、在Python程序中操作MongoDB

可以通过pip安装pymongo来实现对MongoDB的操作。

```
pip3 install pymongo
python3
```

```
>>> from pymongo import MongoClient
>>> client = MongoClient('mongodb://120.77.222.217:27017')
>>> db = client.school
>>> for student in db.students.find():
... print('学号:', student['stuid'])
... print('姓名:', student['name'])
... print('电话:', student['tel'])
...
学号: 1001.0
姓名: 骆昊
电话: 13566778899
学号: 1002.0
姓名: 王大锤
电话: 13012345678
学号: 1003.0
姓名: 白元芳
电话: 13022223333
>>> db.students.find().count()
3
>>> db.students.remove()
{'n': 3, 'ok': 1.0}
>>> db.students.find().count()
0
>>> coll = db.students
>>> from pymongo import ASCENDING
>>> coll.create_index([('name', ASCENDING)], unique=True)
'name_1'
>>> coll.insert_one({'stuid': int(1001), 'name': '骆昊', 'gender': True})
<pymongo.results.InsertOneResult object at 0x1050cc6c8>
>>> coll.insert_many([{'stuid': int(1002), 'name': '王大锤', 'gender': False},
{'stuid': int(1003), 'name': '白元芳', 'gender': True}])
<pymongo.results.InsertManyResult object at 0x1050cc8c8>
>>> for student in coll.find({'gender': True}):
... print('学号:', student['stuid'])
... print('姓名:', student['name'])
... print('性别:', '男' if student['gender'] else '女')
...
学号: 1001
姓名: 骆昊
性别: 男
学号: 1003
姓名: 白元芳
性别:
>>>
```

关于PyMongo更多的知识可以通过它的官方文档进行了解,也可以使用MongoEngine

[https://pypi.org/project/mongoengine/]: 

这样的库来简化Python程序对MongoDB的操作,除此之外,还有以异步I/O方式访问MongoDB的三方库motor

[https://pypi.org/project/motor/]: 

都是不错的选择。

# 使用WebSocket进行聊天

## 一、WebSocket介绍

### １、什么是Websocket

WebSocket 是一种网络通信协议。在 2009 年诞生,于 2011 年被 IETF 定为标准 RFC 6455 通信标准。WebSocket API 也被 W3C 定为标准。

WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上全双工 (full-duplex) 通讯的协议。没有了 Request 和 Response 的概念,两者地位完全平等,连接一旦建立,就建立了持久性连接,浏览器和服务器双方可以随时向对方发送数据。

HTML5 是 HTML 最新版本,包含一些新的标签和全新的 API。HTTP 是一种协议,目前最新版本是HTTP/2 ,所以 WebSocket 和 HTTP 有一些交集,两者相异的地方还是很多。两者交集的地方在 HTTP握手阶段,握手成功后,数据就直接从 TCP 通道传输。

### ２、Web上的即时通信

在没有WebSocket之前，服务器很难主动向客户端推送数据

Web为了实现即时通信，经历了最初的polling,到之后的Long polling,等若干种方式。

**短轮询 Polling**

![](/home/shenyang/Pictures/27.png)

在这种方式下，是不适合获取实时信息的，客户端与服务器之间会一直进行连接，每隔一段时间就询问一次，客户端会轮询，有没有新消息。这种连接方式连接数会很多，也会消耗ＣＰＵ的利用率

在ｗｅｂ端，短轮询用AJAX  JSONP  Polling轮询实现

![](/home/shenyang/Pictures/28.png)

- 优点：短连接，服务器处理简单，支持跨越，浏览器兼容性较好
- 缺点：有一定的延迟，服务器压力较大，浪费带宽流量，大部分都是无效请求



**⻓轮询 Long Polling**

![](/home/shenyang/Pictures/29.png)

长轮询是对轮询的改进版，客户端发送ＨＴＴＰ给服务器之后，看有没有新消息，如果没有新消息，就一直等待。直到有消息或者超时了，才会返回给客户端。消息返回后，客户端再次建立链接，如此反复。这种做法在某种程度上减小了网络带宽和ＣＰＵ利用率等问题

这种做法也有一定的弊端，实时性不高。如果是高实时性的系统，肯定不会采用这种方法。因为一个ｇｅｔ请求来回就需要２个ＲＴＴ，很可能在这段时间内，数据变化很大，客户端拿到自己的数据时已经延后很多了

- 优点：减少轮询次数，低延迟，浏览器兼容性较好
- 缺点：服务器需要保持大量连接



**WebSocket**

![](/home/shenyang/Pictures/30.png)

为了解决其他机制的问题，人们设计出了WebSocket协议

WebSocket是HTML5开始提供的一种独立在单个TCP连接上进行全双工通讯的有状态的协议（它不同于无状态的HTTP）,并且还能支持二进制帧，扩展协议，部分自定义的子协议，压缩等特性

### ３、与普通的HTTP协议的异同

- WebSocket协议的URL是ws://或者wss://开头的，而不是HTTP://或者HTTPS://
- WebSocket 使用与普通 HTTP 或 HTTPS 协议相同的 80 端口和 443 端口进行连接
- WebSocket 的 Header 中有连个特殊字段, 代表它是由 HTTP 协议升级为 WebSocket 协议

```
Connection: Upgrade
Upgrade: websocket
```

### ４、通过js建立一个简单的WebSocket连接

```
var ws = new WebSocket('ws://example.com/socket');
ws.onopen = function () {
	ws.send("Connection established. Hello server!");
}
ws.onmessage = function(event) {
console.log('client recv: ', event.data)
};
ws.onclose = function () { ... }
ws.onerror = function (error) { ... }
```

### ５、Tornodo中使用Websocket

```
class WebsockHandler(tornado.websocket.WebSocketHandler):
	def open(self):
		'''该方法处理建立连接时执行的操作'''
		pass

    def on_close(self):
   		'''该方法处理断开连接时执行的操作'''
    	pass
    	
    def on_message(self, message):
    	'''该方法处理收到消息时进行的操作'''
    	pass
    	
    def write_message(self, message):
    	'''该方法可以给其他人发送消息'''
    	pass
```

## 学习任务：

1. 通过 Tornado 开发一个聊天室程序
2. 通过 WebSocket 进行长连接通信
3. 使用用 Redis 保留留 100 条离线消息