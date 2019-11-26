# 一、CS/BS简介

概念：

```
BS:B browser 浏览器   S server  服务器   主流
CS:C client  客户端   S server  服务器
B/S结构是WEB兴起后的一种网络结构模式，WEB浏览器是客户端最主要的应用软件。这种模式统一了客户端，将系统功能实现的核心部分集中到服务器上，简化了系统的开发、维护和使用。
```

## １、CS/BS的区别

![](/home/shenyang/Desktop/每日资料/Django资料/day01/doc/image-20190720173825832.png)

## ２、CS/BS应用语言

```
CS/BS
	客户端和服务器的交互模型
		Client
			客户端
		Browser
			浏览器
		Server
		
			Web后端
				python
					django     8
					flask      1
					tornado    1
				java
					struts2/struts1
					hibernate
					spring
					springmvc
					mybatis
					springboot
					springclude
				php
					yii
					ci
					thinkphp
```

# 二、MVC

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

![](/home/shenyang/Pictures/40.jpg)

# 三、MTV

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

![](/home/shenyang/Pictures/41.png)

# 四、Django

## １、简介：

```
Django是一个开放源代码的Web应用框架，它最初是被开发来用于管理劳伦斯出版集团旗下的一些以新闻内容为主的网站的，即是CMS（内容管理系统）软件。并于2005年7月在BSD许可证下发布。这套框架是以比利时的吉普赛爵士吉他手Django Reinhardt来命名的。
	重量级，替开发者想了太多的事情，帮开发者做了很多的选择，内置了很多的功能
官方网站
	http://www.djangoproject.com
使用版本1.11.7
	LTS：长期支持版本
	以后再学2.2 LTS
```

## ２、虚拟环境

```
虚拟环境
	mkvirtualenv  虚拟环境的名字  -p  python路径
		eg：mkvirtualenv django 190x -p /usr/bin/python3
		创建虚拟环境
	deactivate
		退出虚拟环境
	workon
		进入虚拟环境
	rmvirtualenv
		删除虚拟环境
		
注意：ubuntu16版本和ubuntu18版本的虚拟环境修改区别
          # 以前的配置路径(ubuntu16.04)
          source /usr/local/bin/virtualenvwrapper.sh   
          #ubuntu18.04中的配置路径
          source ~/.local/bin/virtualwrapper.sh
          
          
深度（deepin）系统安装虚拟环境：
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

## ３、虚拟化技术

```
虚拟化技术
	（1）虚拟机      
	（2）虚拟容器
		Docker  
			支持很多种语言
	（3）虚拟环境--迷你
		python专用
		将python依赖隔离
```

## ４、安装

```
	pip install django
		pip install django==1.11.7   一定要使用==
		pip install django==1.11.7 -i https://pypi.douban.com/simple  豆瓣源
	查看django是否安装成功
		pip freeze
		pip list
		进入python环境
			import django
			django.get_version()
```

## ５、创建django项目

```
django-admin startproject 项目名字
        tree命令观察项目结构
        如果未安装   sudo apt install tree
```

### **项目结构：**

```
项目结构
	项目名字
		manage.py
			管理整个项目的文件
			以后的命令基本都通过他来调用
		项目名字
			__init__
				python包而不是一个文件夹
			settings
				项目全局配置文件
					ALLOWED_HOST=["*"]
					修改settings
						LANGUAGE_CODE='zh-hans'
						TIME_ZONE='Asia/Shanghai'
			urls
				根路由
					url（p1,p2）
			wsgi
				用在以后项目部署上，前期用不到
				服务器网关接口
				webserver gateway interface
```

### 启动项目:

```
启动项目
	python manage.py runserver
		使用开发者服务器启动项目
		默认会运行在本机的 8000端口上
	启动服务器命令
    (1)python manage.py runserver
    (2)python manage.py runserver 9000
    (3)python manage.py runserver 0.0.0.0:9000
```

### 创建一个应用

```
创建一个应用
	python manage.py startapp App/django-admin startapp App
	App结构
		__init__
		views
			视图函数
				视图函数种参数是request  方法的返回值类型是HttpResponse
		models
			模型
		admin
			后台管理
		apps
			应用配置
		tests
			单元测试
		migrations
			__init__
			迁移目录
```

### 拆分路由器

```
	python manager.py starpapp  Two
	
	two创建urls
		urlpatterns = [
    		url(r'^index/',views.index)
		]
	创建views方法
	主路由引用
		    url(r'^two/',include('Two.urls')),
	访问url
		127.0.0.1：8000/two/index/
```

### 编写第一个请求

```
1.编写一个路由
      url(p1, p2)
              url(r'^index/',views.index),
      p1 正则匹配规则
      p2 对应的视图函数
2.编写视图函数
	（1）本质上还是一个函数
		def index(request):
    		return HttpResponse('123')
		要求：只是默认第一个参数是一个request，必须返回一个response
	（2）返回值：
		1.HttpResponse()
			HttpResponse('123')
			HttpResponse('<h1>123</h1>')
	    2.render
			在App下创建templates
				注意名字是固定的，不能打错单词
			render方法的返回值类型也是一个HttpResponse类型的
			要求：
				第一个参数是request，第二个参数的是页面
	********注意需要在settings里的INSTALLED_APPS设置App路径*****
	将应用注册到项目的settings中INSTALLED_APPS中
             加载路由的方式
                  INSTALLED_APPS---》‘Two’
                  INSTALLED_APPS---》‘Two.apps.TwoConfig’  版本限制 1.9之后才能使用
3.模板配置有两种情况
		①在App中进行模板配置
		  - 只需在App的根目录创建templates文件夹即可
		  - 必须在INSTALLED_APP下安装app
		②在项目目录中进行模板配置
		  - 需要在项目目录中创建templates文件夹并标记
		  - 需要在settings中进行注册  settings--》TEMPLATES--》DIRS-					    												os.path.join(BASE_DIR,'templates')
		  注意：开发中常用项目目录下的模板    理由：模板可以继承，复用
```

### Django的工作机制

```
1.用manage .py runserver 启动Django服务器时就载入了在同一目录下的settings .py。该文件包含了项目中的配置信息，如URLConf等，其中最重要的配置就是ROOT_URLCONF，它告诉Django哪个Python模块应该用作本站的URLConf，默认的是urls .py

2.当访问url的时候，Django会根据ROOT_URLCONF的设置来装载URLConf。

3.然后按顺序逐个匹配URLConf里的URLpatterns。如果找到则会调用相关联的视图函数，并把HttpRequest对象作为第一个参数(通常是request)

4.最后该view函数负责返回一个HttpResponse对象。
```

# Day01上课笔记

```
1 创建虚拟环境

2 安装django
        pip install django==1.11.7

3 创建django项目
        django-admin startproject  xxx

4 启动服务器的命令
        python manage.py runserver

5 项目的结构
        项目名字
            项目名字
                init
                urls
                settings
                wsgi
            manage.py

6 修改虚拟环境的步骤
    file-->setting-->project interpreter-->add-->exist environment-->...
    虚拟环境的文件夹--》bin--》python

7 修改欢迎页面为中文
    在settings中修改LANGUAGE_CODE = 'zh-hans'

8 修改为当前系统时间
    在settings中修改TIME_ZONE = 'Asia/Shanghai'

9 允许所有主机访问
    在settings中修改ALLOWED_HOSTS = ['*']

10 启动服务器设置端口号和主机
    python manage.py runserver
    python manage.py runserver 9000
    python manage.py runserver 0.0.0.0:9000

11 视图函数的位置
    （1）项目名字下的视图函数  就是不用
        在urls定义路由路径
            url(r'^路径/',views.视图函数名字不加圆括号)
                eg:url(r'^index/',views.index)
        在views中定义视图函数
            def index(request):
                return HttpResponse('index')

     如果把所有的视图函数都放在项目下了 那么代码看起来就特别的臃肿
     所以我们一般的企业级开发 都是把每一个模块封装出一个app
    （2）App
            1.创建App
                 django-admin startapp App/python manage.py startapp App
            2.在App中创建urls
            3.在urls中创建urlpatterns=[] 我们称在app下urls叫做子路由
            4.在跟路由（项目下的urls）加载子路由  url(r'^app/',include('App.urls'))
            5.在子路由中定义请求资源路径也就是路由
                url(r'^index/',views.index)
            6.在App下的views下创建视图函数
            7.访问 127.0.0.1：8000/跟路由的名字/子路由的名字
                eg:127.0.0.1:8000/app/index/


```

# 一、模板显示

```
显示在模板中
	先挖坑
		{{ var }}
	再填坑
		渲染模板的时候传递上下文进来
		上下文是一个字典
		context={'key':'value'}
	模板的兼容性很强
		不传入不会报错
		多传入也会自动优化掉
	浏览器不认模板
		浏览器也叫做html解析器  只识别html文件
		在到达浏览器之前，已经进行了转换，将模板语言转换成了HTML
	for 支持
		{% for %}
	render底层实现：应用场景，发送邮件，邮件的内容需要使用render方法来操纵
		加载
			three_index = loader.get_template('three.html')
			context={'xxx':'xxxx'}
		渲染
			result = three_index.render(content=content)
			return HttpResponse(result)
```

# 二、修改数据库

```
在settings中的DATABASES中进行修改
- 'ENGINE': 'django.db.backends.mysql',
- ’NAME‘ ：         数据库名字
- ’USER‘：          用户名字
- ’PASSWORD‘：		密码
- ’HOST‘：           主机
- ’PORT‘：           端口号    注意：引号加不加“”都可以

```

```
注意迁移时驱动问题：
				（1）mysqlclient：python2,3都能直接使用，致命缺点-对mysql安装有要求，必须指定位置存在配置文件
    			（2）mysql-python：- python2 支持很好，- python3 不支持。
                （3）pymysql：会伪装成mysqlclient和mysql-python，
            
            - python2，python3都支持init中 import  pymysql      															   pymysql.install_as_mysqldb()
```



# 三、DML

```
数据操作
	(1)迁移
		生成迁移
			python manage.py makemigrations
		执行迁移
			python manage.py migrate
			才会真正在数据库产生表
	(2)ORM
		Object Relational Mapping 对象关系映射
		将业务逻辑和sql进行了一个解耦合
		通过models定义实现  数据库表的定义
	(3)模型定义
		（1）继承models.Model
		（2）会自动添加主键列
		（3）必须指定字符串类型属性的长度
			class Student(models.Model):
                 name = modes.CharField(max_length=16)
                 age = models.IntegerField(default=1)
	存储数据
		创建对象进行save()
	数据查询
		模型.objects.all()
		模型.objects.get(pk=2)
	更新
		基于查询
		save()
	删除
		基于查询
		delete()
```

# 四、Django shell

```
使用：django 终端，python manager.py shell
集成了django环境的python 终端
通常用来调试

from Two.models import Student
students = Student.objects.all()
for student in students:
         print(students.name)
```

# 五、数据级联

```
一对多模型关系：
	class Grade(models.Model):
      g_name = models.CharField(max_length=32)

    class Student(models.Model):
          s_name =models.CharField(max_length=16)
          s_grade=models.ForeignKey(Grade) 
案例：(1).多方获取一方，根据学生找班级名字
	  显性属性：就是你可以在中直接观察到的属性---》通过多方获取一方  那么可以使用多方调用显性属性直接获取一方数据
      student = Student.objects.get(pk=2)
	  grade = student.s_grade
	  return HttpResponse(grade.g_name)
	 (2).一方获取多方，根据班级  找所有的学生
      隐性属性：就是我们在类中观察不到的，但是可以使用的属性---》通过一方获取多方 那么可以使用一方数据的隐性属性 获取多方数据
	  grade = Grade.objects.get(pk=2)
	  students = grade.sutdent_set.all()
	  content = {
			'students':students
			}
	  return render(request,'students_list.html',content)
	  
```

```
关系
		·分类
			·ForeignKey：一对多，将字段定义在多的端中
			·ManyToManyField：多对多，将字段定义在两端中
			·OneToOneField：一对一，将字段定义在任意一端中

		·用一访问多
			·格式
				·对象.模型类小写_set
			·示例
				grade.students_set

		·用一访问一
			·格式
				·对象.模型类小写
			·示例
				·grade.students

		·访问id
			·格式
				·对象.属性_id
			·示例
				·student.sgrade_id
```



# 六、元信息

```
class Meta：指定表名和字段名字
     db_table = '表名'
     注意：表的字段一般都是下划线  eg：s_name
           类的属性一般都是驼峰式  eg: sName
```

# 七、定义字段

```
字段类型
		·AutoField
			·一个根据实际ID自动增长的IntegerField，
			通常不指定如果不指定，一个主键字段将自动添加到模型中

		·CharField(max_length=字符长度)
			·字符串，默认的表单样式是 TextInput

		·TextField
			·大文本字段，一般超过4000使用，默认的表单控件是Textarea

		·IntegerField
			·整数

		·DecimalField(max_digits=None, decimal_places=None)
			·使用python的Decimal实例表示的十进制浮点数
			·参数说明
				·DecimalField.max_digits
					·位数总数
				·DecimalField.decimal_places
					·小数点后的数字位数

		·FloatField
			·用Python的float实例来表示的浮点数

		·BooleanField
			·true/false 字段，此字段的默认表单控制是CheckboxInput

		·NullBooleanField
			·支持null、true、false三种值

		·DateField([auto_now=False, auto_now_add=False])
			·使用Python的datetime.date实例表示的日期
			·参数说明
				·DateField.auto_now
					·每次保存对象时，自动设置该字段为当前时间，
					用于"最后一次修改"的时间戳，它总是使用当前日期，默认为false
				·DateField.auto_now_add
					·当对象第一次被创建时自动设置当前时间，
					用于创建的时间戳，它总是使用当前日期，默认为false
			·说明
				·该字段默认对应的表单控件是一个TextInput. 
				在管理员站点添加了一个JavaScript写的日历控件，
				和一个“Today"的快捷按钮，包含了一个额外的invalid_date错误消息键
			·注意
				·auto_now_add, auto_now, and default 这些设置是相互排斥的，
				他们之间的任何组合将会发生错误的结果

		·TimeField
			·使用Python的datetime.time实例表示的时间，参数同DateField

		·DateTimeField
			·使用Python的datetime.datetime实例表示的日期和时间，参数同DateField

		·FileField
			·一个上传文件的字段

		·ImageField
			·继承了FileField的所有属性和方法，但对上传的对象进行校验，确保它是个有效的image


	字段选项
		·概述
			·通过字段选项，可以实现对字段的约束
			·在字段对象时通过关键字参数指定

		·null
			·如果为True，Django 将空值以NULL 存储到数据库中，默认值是 False

		·blank
			·如果为True，则该字段允许为空白，默认值是 False

		·注意
			·null是数据库范畴的概念，blank是表单验证证范畴的

		·db_column
			·字段的名称，如果未指定，则使用属性的名称

		·db_index
			·若值为 True, 则在表中会为此字段创建索引

		·default
			·默认值

		·primary_key
			·若为 True, 则该字段会成为模型的主键字段

		·unique
			·如果为 True, 这个字段在表中必须有唯一值
```

# 八、模型过滤(查询)

```
Django默认通过模型的objects对象实现模型数据查询。
Django有两种过滤器用于筛选记录：
	filter:返回符合筛选条件的数据集
	exclude	:返回不符合筛选条件的数据集
链式调用：
	多个filter和exclude可以连接在一起查询
	Person.objects.filter().filter().xxxx.exclude().exclude().yyyy
	Person.objects.filter(p_age__gt=50).filter(p_age__lt=80)注意数据类型
	Person.objects.exclude(p_age__gt=50)
	Person.objects.filter(p_age__in=[50,60,61])
```

# 九、创建对象的方式

```
创建对象的方式
	（1）创建对象1   常用(最常用的方法)
		person = Person（）   person.p_name='zs'  person.p_age=18
	（2）创建对象2
		直接实例化对象，设置属性
		创建对象，传入属性
		使用person =  Model.objects.create(p_name='zs',p_age=18)
			person.save()
		自己封装类方法创建
		在Manager中封装方法创建
	（3）创建对象3
		person = Person(p_age=18)
	（4）创建对象4
		注意:__init__已经在父类models.Model中使用，在自定义的模型中无法使用
		在模型类中增加类方法去创建对象
		@classmethod  
        def create(cls,p_name,p_age=100):
                  return cls(p_name=p_name,p_age=p_age)
        person = Person.create('zs')
```

# 十、查询集

## １、过滤器：

过滤器其实就是一个函数，基于所给的参数限制查询集结果，返回查询集的方法称为过滤器

```
概念：查询集表示从数据库获取的对象集合，查询集可以有多个过滤器
```

```

	查询经过过滤器筛选后返回新的查询集，所以可以写成链式调用
	获取查询结果集  QuerySet
	all
		模型.objects.all()
	filter
		模型.objects.filter()
	exclude
		模型.objects.exclude()
	order_by
		persons= Person.objects.order_by('id')
			默认是根据id排序
			注意要写的是模型的属性
	values
		persons= Person.objects.order_by('id') persons.values()
		注意方法的返回值类型   
	切片
		限制查询集，可以使用下标的方法进行限制
			左闭右开区间
		不支持负数
			下标没有负数
		实际上相当于 limit  offset
		studentList = Student.objects.all()[0:5]  
			第一个参数是offset  第二个参数是limit
	懒查询/缓存集
		查询集的缓存：每个查询集都包含一个缓存，来最小化对数据库的访问
		在新建的查询集中，缓存首次为空，第一次对查询集求值，会发生数据缓存，django会将查询出来的数据做	一个缓存，并返回查询结果，以后的查询直接使用查询集的缓存。
		- 都不会真正的去查询数据库
		
		- 懒查询
        - 只有我们在迭代结果集，或者获取单个对象属性的时候，它才会去查询数据
        - 为了优化我们结果和查询
        - 只有在遍历或者需要获取对象属性的时候才需要进行懒查询
```

## ２、获取单个对象

```
获取单个对象：
	get
		不存在会抛异常  DoesNotExist
		存在多于一个 MultipleObjectsReturned
		使用这个函数 记得捕获异常
	last
		返回查询集种的最后一个对象
	first
		需要主动进行排序
		persons=Person.objects.all().first()
	内置函数：框架自己封装得方法 帮助我们来处理业务逻辑
		count
			返回当前查询集中的对象个数
				eg：登陆
		exists
			判断查询集中是否有数据，如果有数据返回True没有反之
```

## ３、字段查询

```
字段查询：
	对sql中where的实现，作为方法filter(),exclude(),get()的参数
	语法:属性名称__比较运算符=值
		Person.objects.filter(p_age__gt=18)
	条件
		属性__操作符=临界值
		gt
			great than
		gte
			great than equals
		lt
			less than
		lte
			less than equals
		gt,gte,lt,lte：大于，大于等于，小于小于等于filter(sage__gt=30)
		in
			in：是否包含在范围内,filter(pk__in=[2,4,6,8])
				单引号可以使用
		exact*******
			exact：判断，大小写不敏感，filter(isDelete = False)
		startswtith
			类似于 模糊查询 like
		endswith
			以 xx 结束  也是like
		contains
			contains：是否包含，大小写敏感，filter(sname__contains='赵')
		isnull,isnotnull
			isnull,isnotnull：是否为空，filter(sname__isnull=False)
		ignore 忽略大小写
			iexact********************
			icontains
			istartswith
			iendswith
			以上四个在运算符前加上 i(ignore)就不区分大小写了 iexact...
```

## ４、时间查询

```
时间
	models.DateTimeField(auto_now_add=True)
	year
	month 会出现时区问题  需要在settings中的USE-TZ中设置为 False
	day
	week_day
	hour
	minute
	second
	orders = Order.objects.filter(o_time__month=9)
		有坑：时区问题
			关闭django中自定义的时区
				USE-TZ=False
			在数据库中创建对应的时区表
```

## ５、聚合函数

```
注意：mysql oracle中所说的聚合函数 多行函数  组函数 都是一个东西  max min avg sum count
聚合函数/组函数/多行函数/高级函数
	模型：
      class Customer(models.Model):
          c_name = models.CharField(max_length=16)
          c_cost = models.IntegerField(default=10)
	使用：
      使用aggregate()函数返回聚合函数的值
      Avg：平均值
      Count：数量
      Max：最大
      Min：最小
      Sum：求和
      eg:Student.objects.aggregate(Max('age'))
```

## ６、跨关系查询

```
模型：
		class Grade(models.Model):
    		g_name = models.CharField(max_length=16)
        class Student(models.Model):
            s_name = models.CharField(max_length=16)
            s_grade = models.ForeignKey(Grade)
    使用：
        模型类名__属性名__比较运算符，实际上就是处理的数据库中的join
        Grade  ---g_name      Student---》s_name  s_grade（外键)
        gf = Student.objects.filter(name='凤姐')
        print(gf[0].s_grade.name)
        grades = Grade.objects.filter(student__s_name='Jack')
        查询jack所在的班级
```

## ７、Q对象

```
用途：常用于逻辑运算，与或非
	年龄小于25：
            Student.objects.filter(Q(sage__lt=25))
        eg:男生人数多余5 女生人数多于10个：
             companies = Company.objects.filter(c_boy_num__gt=1).filter(c_gril_num__gt=5)
             companies = Company.objects.filter(Q(c_boy_num__gt=5)|Q(c_gril_num__gt=10))
        支持逻辑运算：
                    与或非
                    &
                    |
                    ~
        年龄大于等于的：
					Student.objects.filter(~Q(sage__lt=25))
	
```

## ８、Ｆ对象

```
常适用于表内属性的值的比较
	模型：
		class Company(models.Model):
              c_name = models.CharField(max_length=16)
              c_gril_num = models.IntegerField(default=5)
              c_boy_num = models.IntegerField(default=3)
	F：
		获取字段信息，通常用在模型的自我属性比较，支持算术运算
	eg:男生比女生少的公司
	companies = Company.objects.filter(c_boy_num__lt=F('c_gril_num'))
	eg:女生比男生多15个人
	companies = Company.objects.filter(c_boy_num__lt=F('c_gril_num')-15)
```

# Day02上课笔记

```
定义属性

	概述
		·django根据属性的类型确定以下信息
			·当前选择的数据库支持字段的类型
			·渲染管理表单时使用的默认html控件
			·在管理站点最低限度的验证

		·django会为表增加自动增长的主键列，每个模型只能有一个主键列，
		如果使用选项设置某属性为主键列后，
		则django不会再生成默认的主键列

		·属性命名限制
			·遵循标识符规则
			·由于django的查询方式，不允许使用连续的下划线



	库
		·定义属性时，需要字段类型，字段类型被定义在
		django.db.models.fields目录下，为了方便使用，
		被导入到django.db.models中

		·使用方式
			·导入from django.db import models
			·通过models.Field创建字段类型的对象，赋值给属性


	逻辑删除
		·对于重要数据都做逻辑删除，不做物理删除，
		实现方法是定义isDelete属性，类型为BooleanField，默认值为False


	字段类型
		·AutoField
			·一个根据实际ID自动增长的IntegerField，
			通常不指定如果不指定，一个主键字段将自动添加到模型中

		·CharField(max_length=字符长度)
			·字符串，默认的表单样式是 TextInput

		·TextField
			·大文本字段，一般超过4000使用，默认的表单控件是Textarea

		·IntegerField
			·整数

		·DecimalField(max_digits=None, decimal_places=None)
			·使用python的Decimal实例表示的十进制浮点数
			·参数说明
				·DecimalField.max_digits
					·位数总数
				·DecimalField.decimal_places
					·小数点后的数字位数

		·FloatField
			·用Python的float实例来表示的浮点数

		·BooleanField
			·true/false 字段，此字段的默认表单控制是CheckboxInput

		·NullBooleanField
			·支持null、true、false三种值

		·DateField([auto_now=False, auto_now_add=False])
			·使用Python的datetime.date实例表示的日期
			·参数说明
				·DateField.auto_now
					·每次保存对象时，自动设置该字段为当前时间，
					用于"最后一次修改"的时间戳，它总是使用当前日期，默认为false
				·DateField.auto_now_add
					·当对象第一次被创建时自动设置当前时间，
					用于创建的时间戳，它总是使用当前日期，默认为false
			·说明
				·该字段默认对应的表单控件是一个TextInput. 
				在管理员站点添加了一个JavaScript写的日历控件，
				和一个“Today"的快捷按钮，包含了一个额外的invalid_date错误消息键
			·注意
				·auto_now_add, auto_now, and default 这些设置是相互排斥的，
				他们之间的任何组合将会发生错误的结果

		·TimeField
			·使用Python的datetime.time实例表示的时间，参数同DateField

		·DateTimeField
			·使用Python的datetime.datetime实例表示的日期和时间，参数同DateField

		·FileField
			·一个上传文件的字段

		·ImageField
			·继承了FileField的所有属性和方法，但对上传的对象进行校验，确保它是个有效的image


	字段选项
		·概述
			·通过字段选项，可以实现对字段的约束
			·在字段对象时通过关键字参数指定

		·null
			·如果为True，Django 将空值以NULL 存储到数据库中，默认值是 False

		·blank
			·如果为True，则该字段允许为空白，默认值是 False

		·注意
			·null是数据库范畴的概念，blank是表单验证证范畴的

		·db_column
			·字段的名称，如果未指定，则使用属性的名称

		·db_index
			·若值为 True, 则在表中会为此字段创建索引

		·default
			·默认值

		·primary_key
			·若为 True, 则该字段会成为模型的主键字段

		·unique
			·如果为 True, 这个字段在表中必须有唯一值


	关系
		·分类
			·ForeignKey：一对多，将字段定义在多的端中
			·ManyToManyField：多对多，将字段定义在两端中
			·OneToOneField：一对一，将字段定义在任意一端中

		·用一访问多
			·格式
				·对象.模型类小写_set
			·示例
				grade.students_set

		·用一访问一
			·格式
				·对象.模型类小写
			·示例
				·grade.students

		·访问id
			·格式
				·对象.属性_id
			·示例
				·student.sgrade_id
```

# 一、Template概念

```
概念：模板
	在Django框架中，模板是可以帮助开发者快速生成，呈现给用户页面的工具
	模板的设计方式实现了我们MVT中VT的解耦，VT有着N:M的关系，一个V可以调用任意T，一个T可以供任意V使用
	模板处理分为两个过程
		加载
		渲染
	模板中的动态代码段除了做基本的静态填充，可以实现一些基本的运算，转换和逻辑
	早期的web服务器  只能处理静态资源请求  模板能处理动态资源请求 依据计算能生成相应的页面
	注意：在Django中使用的就是Django模板，在flask种使用得是jinja2模板
```

```
模板组成：模板主要有2个部分
			① HTML静态代码
			② 动态插入的代码段（挖坑，填坑）
```

# 二、模板语法

## (1)变量

```
变量
	视图传递给模板的数据
	获取视图函数传递的数据使用{{ var }}接收
	遵守标识符规则：
		拒绝关键字 保留字 数字。。。如果变量不存在，则插入空字符串
	来源：
		视图中传递过来的
		标签中，逻辑创建出来的
```

## (2)模板中的点语法

```

	属性或者方法
		student.name/student.getname
		class Student(models.Model):
    		s_name = models.CharField(max_length=16)
			def get_name(self):
        		return self.s_name
	弊端：模板中的小弊端，调用对象的方法，不能传递参数 为什么不能传递参数  因为连括号都没有
	索引	students.0.gname
	字典  student_dict.hobby
```

## (3)标签

```
特征：标签分为单标签和双标签
	　双标签必须闭合
```

### 功能标签

```
功能标签：（for）
              for
                  for i in xxx
                  empty
                      {% empty %}
                      判断之前的代码有没有数据 如果没有显示empty下面的代码
                      eg:{% for 变量 in 列表 %}
                              语句1 
                                 {% empty %}
                              语句2
                          {% endfor %}
                  forloop
                      循环状态的记录
                      {{ forloop.counter }} 表示当前是第几次循环，从1数数
                      {{ forloop.counter0}}表示当前是第几次循环，从0数数
                      {{ forloop.revcounter}}表示当前是第几次循环，倒着数数，到1停
                      {{ forloop.revcounter0}}表示当前第几次循环，倒着数，到0停
                      {{ forloop.first }} 是否是第一个  布尔值
                      {{ forloop.last }} 是否是最后一个 布尔值
```

```
功能标签：（if）
                  if
                      分支
                      判断
                      if - else
                      if - elif -else
```

### 注释

```

          单行注释
              {#  被注释掉的内容  #}
          多行注释
              {% comment %}
              内容
          	  {% endcomment %}
```

### withratio

```
			乘
            {% widthratio 数  分母  分子  %}
            {% widthratio count 1 5 %}
```

### 整除

```
{% if num|divisibleby:2 %}
                      整除
                      {% if forloop.counter|divisibleby:2%}
                      奇偶行变色
```

### ifequal

```
ifequal
            {%  ifequal  value1 value2 %}
                语句
        {% endifequal %}
            {% ifequal forloop.counter 5 %}
```

## (4)过滤器

```
add：
		<h4>{{ count|add:2 }}</h4>#加２
		<h4>{{ count|add:-2 }}</h4>＃减２
	upper：
	lower：
	safe
		确认安装
		进行渲染
		eg:
              code = """
                  <h2>睡着了</h2>
                  <script type="text/javascript">
                      var lis = document.getElementsByTagName("li");

                      for (var i=0; i< lis.length; i++){
                          var li = lis[i];
                          li.innerHTML="日本是中国领土的一部分!";
                      }
                  </script>
                   """
	endautoescape：
		{% autoescape off%}
			code
		{% endautoescape %}
```

## (5)结构标签

```
结构标签
	block
		块
		坑
		用来规划页面布局，填充页面
			首次出现代表规划
			第二次c出现代表填坑
			第三次出现也代表填坑，默认会覆盖
			第N次...
			如果不想被覆盖  block.super
	extends
		继承
		面向对象的体现
		提高模板的复用率
	include
		包含
		将其它模板作为一部分，包裹到我们的页面中
```

## (6)加载静态资源

```
加载静态资源
	static--》 html  css js  img font
	静态资源路径 /static/css/xxx.css
		不推荐硬编码
	需要在settings中添加  STATICFILES_DIRS=[os.path.join(BASE_DIR,'static')]
	推荐
		{% load static%}
		{%static,'css/xxx.css'%}
		思考：html和模板中的页面  都可以使用load吗？  注意必须在模板中使用
	坑点：仅在DEBUG模式下可以使用  如果settings中的DEBUG=False 那么是不可以使用的
```

# 三、常见的请求状态码

```
请求状态码
	2xx
		成功
	3xx
		重定向 302  301 永久重定向
	4xx
		客户端错误
	5xx
		服务端错误
	
	200 成功   301 永久重定向  302 重定向  404 路径  405 请求方式  500 业务逻辑错误
	403 防跨站攻击
```

# 四、view视图函数

## １、概念及其基础语法

### (1)概念：

```
视图函数MTV中的View，相当于MVC中的Controller作用，控制器 接收用户输入（请求），
	 协调模板模型，对数据进行处理，负责的模型和模板的数据交互。
	
视图函数返回值类型：（1）以Json数据形势返回
						前后端分离
						return  JsonResponse
				 （2）以网页的形势返回    HttpResponse   render   redirect
						重定向到另一个网页
						错误视图(40X,50X)
```

### (2)url匹配正则注意事项:

```
url匹配正则注意事项:  
					正则匹配时从上到下进行遍历，匹配到就不会继续向后查找了
					匹配的正则前方不需要加反斜线
					正则前需要加 （r）表示字符串不转义
url匹配规则：按照书写顺序，从上到下匹配，没有最优匹配的概念，匹配到就停止了			
			eg：hehe/hehehe
```

### (3)url接受参数

```
url接受参数：
          （1）如果需要从url中获取一个值，需要对正则加小括号
                url(r'^grade/(\d+)$',views.getStudents),
                注意，url匹配中添加了 () 取参，在请求调用的函数中必须接收	
                def  getStudents(request,classId)：
                    一个参数
          （2）如果需要获取url路径中的多个参数，那就添加多个括号，默认按照顺序匹配路径名字
                url(r'^news/(\d{4})/(\d)+/(\d+)$',views.getNews),
                匹配年月日 def getNews(request,year,month,day)：
                    多个参数
                eg:def get_time(request,hour, minute, second):
    					return HttpResponse("Time %s: %s: %s" %(hour, minute, second))
          （3）参数也可以使用关键字参数形势
                 url(r'^news/(?P<year>\d{4})/(?P<month>\d)+/(?P<day>\d+)$',views.getNews),
                    多个参数并且指定位置
               eg:def get_date(request,  month, day, year):
   						 return HttpResponse("Date %s- %s- %s" %(year, month, day))
   						 
   		总结路径参数：
                  位置参数
                  	  eg：127.0.0.1：8000/vie/testRoute/1/2/3/
                  	      r('^testRoute/(\d+)/(\d+)/(\d+)/')
                      使用圆括号包含规则
                      一个圆括号代表一个参数
                      代表视图函数上的一个参数
                      参数个数和视图函数上的参数一一对应（除默认request）
                  关键字参数
                      可以在圆括号指定参数名字 （?P<name>reg）
                      视图函数中存在和圆括号中name对应的参数
                      参数不区分顺序
                      个数也需要保持一致，一一对应
```

## ２、内置函数

```
内置函数
	locals()
		将局部变量，使用字典的形式打包
		key是变量的名字
		value是变量的值
```

## ３、反向解析

```
反向解析
	反向解析的用处：获取请求资源路径，避免硬编码。
	
	配置
		(1)在根urls中
              url(r'^views/', include('ViewsLearn.urls',namespace='view')),
                      在根路由中的inclue方法中添加namespace参数
		(2)在子urls中
              url(r'^hello/(\d+)',views.hello,name='sayhello'),
			         在子路由中添加name参数
		(3)在模板中使用
              <a href="{% url 'view:sayhello' %}">Hello</a>

			调用的时候 反向解析的路径不能有编译错误  格式是  {% url 'namespace:name%}'
                        
		如果存在位置参数
			{% url  ‘namespace:name'   value1 value2 ... %}
		如果存在关键字参数
			{% url 'namespace:name'   key1=value1 key2=vaue2 ...%}
		在模板中使用
			<a href="{% url 'view:sayhello'  year=2017 %}">Hello</a>
	优点
		如果在视图，模板中使用硬编码连接，在url配置发生改变时，需要变更的代码会非常多，这样导致我们的代码结构不是很容易维护，使用反向解析可以提高我们代码的扩展性和可维护性。
```

# 第三天

# 一、request对象

**概念**：django框架根据Http请求报文自动生成的一个对象，包含了请求各种信息。

```
属性：
       path：请求的完整路径
       method：GET  1.11版本最大数据量2K
	          POST 参数存在请求体中，文件上传等。
			  请求的方法，常用GET,POST
			  应用场景：前后端分离的底层 判断请求方式 执行对应的业务逻辑
	   GET：QueryDict类字典结构 key-value
		                      一个key可以对应多个值
		                      get 获取最后一个
		                      getlist 获取多个
							类似字典的参数，包含了get请求方式的所有参数
	  POST： 类似字典的参数，包含了post请求方式的所有参数
	  encoding：编码方式，常用utf-8
	  FILES：类似字典的参数，包含了上传的文件  文件上传的时候会使用  
	         页面请求方式必须是post   form的属性enctype=multipart/form-data
	         flask和django通用的   一个是专属于django
	  COOKIES：类似字典的参数，包含了上传的文件  获取cookie
	  session：类似字典，表示会话
	  META：   应用反爬虫  REMOTE_ADDR  拉入黑名单
	           客户端的所有信息 ip
	           print(request.META)
			  for key in request.META:
			        print(key, request.META.get(key))
			  print("Remote IP", request.META.get("REMOTE_ADDR"))
```

## QueryDict和Dict的区别

```
#dict是字典对象，没有urlencode()方法
#QueryDict是对象，有urllencode()方法,作用是把QueryDict对象转换为url字符串
#queryDict默认的value值是一个列表
#dict的默认value是一个字符串
```

# 二、HttpResponse对象

当浏览器访问服务器的时候　　那么服务器响应的数据类型

## 响应分类：（1）HTML响应   （2）JsonResponse（前后端分离）

**html响应**

```
（1）基类HttpResponse   不使用模板，直接HttpResponse()
	def hello(request):
             response = HttpResponse()
             response.content = "德玛西亚"
             response.status_code = 404
             response.write("千锋")
             response.flush()
        return response
     方法
		 init				初始化内容
	     write(xxx)			直接写出文本
         flush()				冲刷缓冲区
         set_cookie(key,value='xxx',max_age=None,exprise=None)
         delete_cookie(key)		删除cookie，上面那个是设置
         
（2）render转发：
		方法的返回值类型也是一个HttpResponse

（3）HttpResponseRedirect重定向
     HttpResponse的子类，响应重定向:可以实现服务器内部跳转
	return HttpResponseRedict('/grade/2017')使用的时候推荐使用反向解析
	
	状态码：302
	
	简写方式：简写redirect方法的返回值类型就是HttpResponseRedirect
```

```
	反向解析：
            （1）页面中的反向解析 url方法
                      	  {% url 'namespance:name'
                      url 位置参数
                          {% url 'namespace:name'  value1 value2 %}
                      url关键字参数
                          {% url 'namespace:name' key1=value1 key2 = value2 %}
            （2）python代码中的反向解析（一般python代码的反向解析都会结合重定向一起使用）
                          reverse('namespace:name')
                      位置参数
                          reverse('namespace:name', args=(value1, value2 ...))
                          reverse('namespace:name', args=[value1, value2 ...])
                      关键字参数
                          reverse('namespace:name', kwargs={key1:value2, key2:value2 ...})

```

## 转发(渲染)和重写向的区别？

```
重定向     是一件事做完  去做另一件事 eg 添加 成功 之后 去查询
转发/渲染  一件事没有做完
# 转发共享了request对象
# 重定向是执行了2次请求
```



**JsonResponse**

```
这个类是HttpRespon的子类，它主要和父类的区别在于：
1.它的默认Content-Type 被设置为： application/json

2.第一个参数，data应该是一个字典类型，当 safe 这个参数被设置为：False ,那data可以填入任何能被转换为JSON格式的对象，比如list, tuple, set。 默认的safe 参数是 True. 如果你传入的data数据类型不是字典类型，那么它就会抛出 TypeError的异常。

def get_info(request):
	data = {
        "status": 200,
        "msg": "ok",
    }
	return JsonResponse(data=data)
	
# HttpResponsePermanentRedirect  永久重定向
# HttpResponsePermanentRedirect的父类是HttpResponseRedirectBase
# # HttpResponseRedirectBase是HttpResponse的子类
```

**HttpResponse子类**

```
HttpResponse子类
	HttpResponseRedirect 
		-302
	HttpResponsePermanentRedirect
		- 重定向，永久性- 
		-301
	HttpResponseBadRequest	
		-400
	HttpResponseNotFound
		- 404
	HttpResponseForbidden
		- 403   csrf 防跨站攻击 
	HttpResponseNotAllowed
		- 405   
	HttpResponseServerError
		- 500
	Http404- Exception
           - raise 主动抛异常出来
```

# 三、会话技术

```
为什么会有会话技术
	服务器如何识别客户端
	Http在Web开发中基本都是短连接
	请求生命周期从Request开始，到Response就结束
会话技术：cookie session  token（自定义的session）
```

## (1)cookie:

```
	客户端会话技术，数据都存储在客户端，以key-value进行存储，支持过期时间max_age，默认请求会携带本网站的所有cookie，cookie不能跨域名，不能跨浏览器，cookie默认不支持中文base64
	cookie是服务器端创建  保存在浏览器端
	设置cookie应该是服务器 response
	获取cookie应该在浏览器 request
	删除cookie应该在服务器 response
cookie使用：
	设置cookie：response.set_cookie(key,value）
	获取cookie：username =request.COOKIES.get("username")
	删除cookie：response.delete_cookie("content")
	
	可以加盐：加密 获取的时候需要解密
		加密  response.set_signed_cookie('content', uname, "xxxx")
		解密  
			 获取的是加盐之后的数据
			 	uname = request.COOKIES.get('content)
			 获取的是解密之后数据
			 uname = request.get_signed_cookie("content", salt="xxxx")
		
	通过Response将cookie写到浏览器上，下一次访问，浏览器会根据不同的规则携带cookie过来
		max_age:整数，指定cookie过期时间  单位秒
		expries:整数，指定过期时间，还支持是一个datetime或	timedelta，可以指定一个具体日期时间
		max_age和expries两个选一个指定
		过期时间的几个关键时间
			max_age 设置为 0 浏览器关闭失效
			设置为None永不过期
			expires=timedelta(days=10) 10天后过期
```

## (2)session

```
	服务端会话技术，数据都存储在服务端，默认存在内存 RAM，在django被持久化到了数据库中，该表叫做
	Django_session,这个表中有三个字段，分别为seesion_key,session_data,expris_date.
	Django中Session的默认过期时间是14天，支持过期，主键是字符串，默认做了数据安全，使用了BASE64
		- 使用的base64之后 那么这个字符串会在最后面添加一个=
		- 在前部添加了一个混淆串
	依赖于cookies
session使用：
	设置session
		    request.session["username"] = username
	获取session
		    username = request.session.get("username")
	使用session退出
            del request.session['username']
                cookie是脏数据
            response.delete_cookie('sessionid')
                session是脏数据
            request.session.flush()
			   冲刷
	session常用操作
		get(key,default=None) 根据键获取会话的值
		clear() 清楚所有会话
		flush() 删除当前的会话数据并删除会话的cookie
		delete request['session_id'] 删除会话
		session.session_key获取session的key
		request.session[‘user’] = username
			数据存储到数据库中会进行编码使用的是Base64
```

## (3)token

**基本概念**：Token的中文意思是‘令牌’，主要是用于身份验证

```
Facebook，Twitter，Google+，Github 等大型网站都在使用。比起传统的身份验证方法，Token 有扩展性强，安全性高的特点，非常适合用在 Web 应用或者移动应用上,如果使用在移动端或客户端开发中，通常以Json形式传输，服务端会话技术,自定义的Session,给他一个不能重复的字符串,数据存储在服务器中
```

**验证方法：　　　×××面试内容**

```
使用基于 Token的身份验证方法，在服务端不需要存储用户的登录记录。大概的流程是这样的：
1.客户端使用用户名跟密码请求登录
2.服务端收到请求，去验证用户名与密码
3.验证成功后，服务端会签发一个 Token，再把这个Token 发送给客户端
4.客户端收到 Token以后可以把它存储起来，比如放在 Cookie里或者 Local Storage里
5.客户端每次向服务端请求资源的时候需要带着服务端签发的Token
6.服务端收到请求，然后去验证客户端请求里面带着的 Token，如果验证成功，就向客户端返回请求的数据
```

**python常用Token的生成方法**

```
（1）binascii.b2a_base64(os.urandom(24))[:-1]
	使用举例：
		>>> import binascii
		>>> import os
		>>>binascii.b2a_base64(os.urandom(24))[:-1]

		b'J1pJPotQJb6Ld+yBKDq8bqcJ71wXw+Xd'
	总结：这种算法的优点是性能快， 缺点是有特殊字符， 需要加replace 来做处理。
（2）sha1(os.urandom(24)).hexdigest()
	使用举例：
		>>> import hashlib
		>>> import os
		>>> hashlib.sha1(os.urandom(24)).hexdigest()

		'21b7253943332d0237a720701bcb8161b82db776'
	总结：这种算法的优点是安全，不需要做特殊处理。缺点是覆盖范围差一些。
 （3）uuid4().hex
 	使用举例：
 		>>> import os
		>>> import uuid
		>>> uuid.uuid4().hex

		'c58a80d3b7864b0686757b95e9626e47'
	总结：Uuid使用起来比较方便， 缺点为安全性略差一些。
（4）base64.b32encode(os.urandom(20))/base64.b64encode(os.urandom(24))
	使用举例：
		>>> import base64
		>>> import os
		>>>base64.b32encode(os.urandom(20))
		
		b'NJMTBMOYIXHNRATTOTVONT4BXJAC25TX'
		
		>>>base64.b64encode(os.urandom(24))

		b'l1eU6UzSlWsowm8M8lH5VaFhZEAQ4kQj'
	
	总结：可以用base64的地方，选择binascii.b2a_base64是不错的选择
		 根据W3的SessionID的字串中对identifier的定义，SessionID中使用的是base64，但在Cookie的值内使用需要注意“=”这个特殊字符的存在；
		 如果要安全字符（字母数字），SHA1也是一个不错的选择，性能也不错；

```

**Token的应用**

```
import hashlib

# 待加密内容
strdata = "xiaojingjiaaseafe16516506ng"

h1 = hashlib.md5()
h1.update(strdata.encode(encoding='utf-8'))

strdata_tomd5 = h1.hexdigest()

print("原始内容：", strdata, ",加密后：", strdata_tomd5)

import time
import base64
import hmac


# 生产token
def generate_token(key, expire=3600):
    r'''''
        @Args:
            key: str (用户给定的key，需要用户保存以便之后验证token,每次产生token时的key 都可以是同一个key)
            expire: int(最大有效时间，单位为s)
        @Return:
            state: str
    '''
    ts_str = str(time.time() + expire)
    ts_byte = ts_str.encode("utf-8")
    sha1_tshexstr = hmac.new(key.encode("utf-8"), ts_byte, 'sha1').hexdigest()
    token = ts_str + ':' + sha1_tshexstr
    b64_token = base64.urlsafe_b64encode(token.encode("utf-8"))
    return b64_token.decode("utf-8")


# 验证token
def certify_token(key, token):
    r'''''
        @Args:
            key: str
            token: str
        @Returns:
            boolean
    '''
    token_str = base64.urlsafe_b64decode(token).decode('utf-8')
    token_list = token_str.split(':')
    if len(token_list) != 2:
        return False
    ts_str = token_list[0]
    if float(ts_str) < time.time():
        # token expired
        return False
    known_sha1_tsstr = token_list[1]
    sha1 = hmac.new(key.encode("utf-8"), ts_str.encode('utf-8'), 'sha1')
    calc_sha1_tsstr = sha1.hexdigest()
    if calc_sha1_tsstr != known_sha1_tsstr:
        # token certification failed
        return False
        # token certification success
    return True


key = "xiaojingjing"
print("key：", key)
user_token = generate_token(key=key)

print("加密后：", user_token)
user_de = certify_token(key=key, token=user_token)
print("验证结果：", user_de)

key = "xiaoqingqing"
user_de = certify_token(key=key, token=user_token)
print("验证结果：", user_de)
```

## (4)cookie与session的区别***面试内容

```
1、cookie数据存放在客户端上，session数据放在服务器上。
2、cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗 
考虑到安全应当使用session。
3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能 
考虑到减轻服务器性能方面，应当使用COOKIE
```

## (5)session与token的区别***面试内容

```
1.作为身份认证 token安全性比session好，因为每个请求都有签名还能防止监听以及重放攻击
2.Session 是一种HTTP存储机制，目的是为无状态的HTTP提供的持久机制。Session 认证只是简单的把User 信息存储到Session 里，因为SID 的不可预测性，暂且认为是安全的。这是一种认证手段。 但是如果有了某个User的SID,就相当于拥有该User的全部权利.SID不应该共享给其他网站或第三方.
3.Token,如果指的是OAuth Token 或类似的机制的话，提供的是 认证 和 授权 ，认证是针对用户，授权是针对App。其目的是让 某App有权利访问 某用户 的信息。这里的 Token是唯一的。不可以转移到其它 App上，也不可以转到其它 用户上。
```

# 四、csrf豁免

```
CSRF
	防跨站攻击
	实现机制
		页面中存在{% csrf_token %}时
		在渲染的时候，会向Response中添加 csrftoken的Cookie
		在提交的时候，会被添加到请求体中， 会被验证有效性
    csrf（https://www.jianshu.com/p/d1407591e8de）
解决csrf的问题/csrf豁免：
    1 注释中间件
    2 在表单中添加{%csrf_token%}
    3 在方法上添加 @csrf_exempt
```

# 第四天

# 一、Model-->DB

```
Model -> DB
          迁移步骤
              生成迁移文件  python manage.py makemigrations
              执行迁移文件  python manage.py migrate
            
          迁移文件的生成
              根据models文件生成对应的迁移文件
              根据models和已有迁移文件差别 生成新的迁移文件
                
          迁移原理  了解
              先去迁移记录查找，哪些文件未迁移过
                  app_label + 迁移文件名字
              执行未迁移的文件
              执行完毕，记录执行过的迁移文件
                
          可以指定迁移的app  python manage.py makemigrations app
                           python manage.py migrate    
          重新迁移
              删除迁移文件
                  migrations所涉及的迁移文件
              删除迁移文件产生的表
              删除迁移记录
                  django-migrations
```

# 二、DB-->Model

```
DB -> Model
	反向生成到指定得app下 --》  python manage.py inspectdb > App/models.py
	元信息中包含一个属性  managed=False   不支持迁移
	- 如果自己的模型不想被迁移系统管理，也可以使用 managed=False进行声明
```

# 三、模型关系

## (1)一对一

```
应用场景
	用于拆分复杂的表
	扩展新的功能
	oneToOneField
	确认主从关系
	底层实现，使用外键实现，对外键添加了唯一的约束
```

```
class Student(models.Model):
    s_name = models.CharField(max_length=32)


class IDCard(models.Model):
    id_num = models.CharField(max_length=18, unique=True)
    id_student = models.OneToOneField(Student, null=True, blank=True, on_delete=models.SET_NULL)
```

### 添加

```
添加主表数据
          def add_student(request):
              s_name = request.GET.get('name')
              student = Student()
              student.s_name = s_name
              student.save()
              return HttpResponse('添加学生成功')
```

```
添加从表数据
          def add_idcard(request):
              i_card = request.GET.get('card')
              id_card = IdCard()
              id_card.i_card = i_card
              id_card.save()
              return HttpResponse('添加card成功')
```

```
数据绑定
          def bind(request):
              student = Student.objects.last()
              idcard = IdCard.objects.last()
              idcard.i_student = student
              # idcard.i_student = student.id
              idcard.save()
              return HttpResponse('绑定成功')
```

```
思考：
      student是主表  idcard是从表
      1 再添加一个主表数据  然后执行绑定可不可以  可以
      2 再添加一个从表数据  然后执行绑定可不可以  不可以
```

### 删除

```
主表数据删除/on_delete
                默认  CASECADE
                    默认级联数据被删除
                    从表数据删除，主表不受影响
                    主表数据删除，从表数据直接删除
                models
                    SET_NULL
                        置空
                        前提允许为NULL
                        常用
                    SET_DEFAULT
                        置为默认值
                        前提存在默认值
                    SET
                        自己赋值
                models.PROTECT
                    从表数据受保护的
                    当存在级联数据的时候，删除主表数据，会抛出异常
                    主表不存在级联数据的时候，可以删除
                    开发中为了防止误操作，我们通常会设置为此模式
```

```
django默认是级联删除   删除主表的时候 从表数据都会删除
执行顺序是:从表的数据删除之后  主表的数据跟着删除
      def delete_student(request):
          student = Student.objects.get(pk=1)
          student.delete()
          return HttpResponse('删除成功')
```

```
def delete_idcard(request):
    idcard = IdCard.objects.get(pk=1)
    idcard.delete()
    return HttpResponse('删除成功')
```

```
外键的字段的约束  如果将on_delete修改为models.PROTECT 那么如果有级联关系 删除主表的时候 会抛异常
如果没有级联关系  那么就会直接删除
def deleteprotect_student(request):
    student = Student.objects.get(pk=3)
    student.delete()
    return HttpResponse('删除成功')
```

```
外键的字段的约束  如果将on_delete设置为models.setnull  那么如果有级联关系 会将从表的外键设置为null
主表数据也会删除   如果没有级联关系  会直接删除主表数据
def deletesetnull_student(request):
    student = Student.objects.get(pk=4)
    student.delete()
    return HttpResponse('删除成功')
```

### 查询

```
查询/获取
	从获取主
		显性属性
			该显性属性会返回一个对象
	主获取从
		隐性属性
		默认就是从表模型名小写
		该表模型名 会返回一个对象
```

```
根据idcard 获取student    显性属性
def get_student(request):
    idcard = IdCard.objects.get(pk=3)
    print(idcard.i_student.s_name)
    return HttpResponse('查询student')
```

```
根据student 获取 idcard
def get_idcard(request):
    student = Student.objects.get(pk=2)
    主查从   获得主表的对象之后 该对象 有一个属性 是隐形属性
    这个属性 是外键那个模型的小写
    print(student.idcard.i_card)
    return HttpResponse('查询idcard')
```

## (2)一对多

````
class Dept(models.Model):
    d_name = models.CharField(max_length=32,unique=True)

class Emp(models.Model):
    e_name = models.CharField(max_length=32)
    #外键默认不能为空
    e_dept = models.ForeignKey(Dept,null=True,blank=True,on_delete=models.SET_NULL)
````

### 添加

```
外键不能为空
```

```
def add_dept(request):
    d_name = request.GET.get('name')
    dept = Dept()
    dept.d_name = d_name
    dept.save()
    return HttpResponse('插入dept成功')
```

```
def add_emp(request):
    e_name = request.GET.get('name')
    emp = Emp()
    emp.e_name = e_name
    emp.save()
    return HttpResponse('插入emp成功')
```

```
def bind(request):
    dept = Dept.objects.last()
    emp = Emp.objects.last()
    emp.e_dept = dept
    emp.save()
    return HttpResponse('绑定成功')
```

### 删除:数据删除同一对一一样

````
删除主表数据 默认级联从表数据
修改on_delete属性为models.PROTECT
	有级联数据数据 抛异常
	没有级联数据 可以正常删除
修改on_delete=models.SET_NULL
	有级联数据 外键值设置为null
	没有级联数据 直接删除
删除字表数据 不管字表返回得是列表还是单个数据 都可以直接删除  应用场景 多选删除
````

````
删除默认是级联删除
def deletedept(request):
    dept = Dept.objects.get(pk=2)
    dept.delete()
    return HttpResponse('删除成功')
````

```
删除从表的时候  会将所有符合条件的删除
def deleteemp(request):
    Emp.objects.filter(e_dept_id=1).delete()
    return HttpResponse('删除成功')
```

```
def deleteprotectdept(request):
    dept = Dept.objects.get(pk=3)
    dept.delete()
    return HttpResponse('删除成功')
```

```
def deletesetnulldept(request):
    dept = Dept.objects.get(pk=1)
    dept.delete()
    return HttpResponse('删除成功')
```

### 查询:及联对象查询

```
从获取主
	显性属性
主获取从
	隐性属性
	默认是 模型小写_set
		该属性得返回值类型是relatedManager类型
		注意relatedManager是一个不可以迭代得对象  所以需要调用Manager得方法
	relatedManager也是Manager的一个子类
		filter
		exclude
		all
		切片
		...
```

```
def finddept(request):
    emp = Emp.objects.get(pk=7)
    print(emp.e_dept)
    return HttpResponse('查询成功')
```

````
def findemp(request):
    dept = Dept.objects.get(pk=4)
    一对多的时候 如果通过主查从  那么主的对象调用从的模型小写_set   
    xxx_set方法的返回值类型是RelatedManager
    RelatedManager对象可以调用all  fiter exclude。。。。。。
    emps = dept.emp_set
    for emp in emps.all():
        print(emp.e_name)
    return HttpResponse('查询成功')
````

## (3)多对多

```
ManyToManyField
产生表的时候会产生单独的关系表
关系表中存储关联表的主键，通过多个外键实现的，多个外键联合唯一
会产生额外的关系表
	表中使用多个外键实现
	外键对应关系表的主键
```

```
class Custom(models.Model):
    c_name = models.CharField(max_length=32)

class Goods(models.Model):
    g_name = models.CharField(max_length=32)
    g_custom = models.ManyToManyField(Custom)
```

### 添加

```
主添加从
	customer.goods_set.add(goods)
		隐性属性
从添加主
	goods.g_customer.add(customer)
		显性属性
需要注意的是：关系表中外键的联合唯一
```

```
def addcustom(request):
    custom = Custom()
    custom.c_name = 'zs1'
    custom.save()
    return HttpResponse('添加成功')
    
def addgoods(request):
    goods = Goods()
    goods.g_name = '小当家1'
    goods.save()
    return HttpResponse('添加成功')
```

```
从 -- 主   从对象.属性.add(主对象)
首先必须有数据才可以插入 该数据必须是查询出来的
def addgoods1(request):
    custom = Custom.objects.get(pk=1)
    goods = Goods.objects.get(pk=1)
    goods.g_custom.add(custom)
    # goods.save() 没有实际作用
    return HttpResponse('添加成功')
```

```
主 -- 从   主对象.从模型名_set.add(从对象)
def addcustom1(request):
    custom = Custom.objects.get(pk=3)
    goods = Goods.objects.get(pk=3)
    custom.goods_set.add(goods)
    return HttpResponse('添加成功')
```

### 删除

```
goods.g_customer.remove(customer)
	显性属性
custom.goods_set.remove(goods)
	隐性属性
```

```
删除  eg：删除用户  那么关系表的数据会不会删除
会删除  默认是级联删除   不建议
def deletecustom(request):
    custom = Custom.objects.get(pk=1)
    custom.delete()
    return HttpResponse('删除成功')
```

```
删除    从 -- 主
def deleterelation(request):
    custom = Custom.objects.get(pk=2)
    goods = Goods.objects.get(pk=2)
    goods.g_custom.remove(custom)
    return HttpResponse('删除成功')
```

````
删除   主 -- 从
def deleterelation1(request):
    custom = Custom.objects.get(pk=3)
    goods = Goods.objects.get(pk=3)
    custom.goods_set.remove(goods)
    return HttpResponse('删除成功')
````

### 查询

```
customer.goods_set.all()
```

```
从 -- 主  显性属性
def findrelation(request):
    goods = Goods.objects.get(pk=3)
    gs = goods.g_custom.all()
    print(gs)
    return HttpResponse('查询成功')
```

```
def findrelation1(request):
    custom = Custom.objects.get(pk=3)
    print(custom.goods_set.all())
    return HttpResponse('查询成功')
```

www.pythontutor.com/visualize.html#mode=display

# 第五天

# 一、模型继承

```
默认一个模型在数据库中映射一张表
如果模型存在继承的时候，父模型产生表映射
子模型对应的表会通过外键和父表产生关联
从表外键引用主表的主键
	不能说从表外键引用主表的主键就一定是模型继承　　因为一对一　一对多　都会引用主表得外键
关系型数据库性能
	数据量越大性能越低
	关系越多越复杂　性能越低
```

```
抽象模型
	在父类的Model的元信息中添加  abstract=True
		class Meta:
      		abstract=True
	抽象的模型不会在数据库中产生表
	子模型拥有父模型中的所有字段
	class Animal(models.Model):
    	a_name = models.CharField(max_length=16)
    	class Meta:
        	abstract = True
        	
	class Cat(Animal):
    	c_eat = models.CharField(max_length=32)

	class Dog(Animal):
    	d_legs = models.IntegerField(default=4)
```

# 二、静态资源

```
静态资源
	静态资源和模板的区别
	(1)模板的路径不可以直接访问　　必须通过请求来访问
		static资源可以直接访问
	(2)模板的语法不可以在静态资源中书写
注意：
	(1)使用的时候注意配置资源位置
			STATICFILE_DIRS
			使用｛％ load static ％｝
			{% static '相对路径'　%}
	(2)全栈工程师　　要求会templates
		开发工程师　　前后端分离static
```

# 三、文件上传

````
要求：客户端
	必须使用POST
	指定enctype='multiplepart/form-data'
````

```
原生代码：适用django也适用于flask
	从request.FILES中获取到上传上来的文件
	打开一个文件，从上传上来的文件进行读取，向打开的文件中进行写入
		必须以二进制的格式来书写
	每次写入记得 flush
	
	def upload_file(request):
          if request.method == "GET":
              return render(request, 'upload.html')
          elif request.method == "POST":
              icon = request.FILES.get("icon")
              print(type(icon))
              with open("/home/xxx/xxx/Day06/xxx/static/img/icon.jpg", 'wb') as save_file:
                  for part in icon.chunks():
                      save_file.write(part)
                      save_file.flush()

              return HttpResponse("文件上传成功")
              
 实现步骤：
         （1）表单得请求方式是post
         （2）添加表单得属性 enctype='multipart/form-data'  二进制传输
         （3）input得type属性值为file
         （4）获取表单中得file值  request.FILES.get获取的是文件的名字
         （5）with open打开一个路径，然后以wb的模式使用
             for i in xxx.chunks()
                fp.write()
                fp.flush()
                fp.close()
```

```
Django内置：
	（1）创建模型并且指定ImageField属性（注意依赖于pillow，pip install pillow）
		eg：u_icon = models.ImageField(upload_to='icons')
		imageField在数据库中的数据类型是varchar,默认长度为100
	（2）settings中指定 MEDIA_ROOT
            MEDIA_ROOT = os.path.join(BASE_DIR, 'static/upload')
            注意：media_root后面的数据类型不是一个列表
				会自动的创建文件夹
				该文件夹的路径是MEDIA_ROOT + ImageField的upload的值
	注意：1：重复添加同一个图片，那么会直接添加进去，文件的名字是文件名原名+唯一串
		 2：数据库icon的值是upload_to + 文件名字
		
	隐藏bug：linux系统下文件夹的第一级字目录下 最多存储65535个文件
	
		u_icon = models.ImageField(upload_to='%Y/%m/%d/icons')
		支持时间格式化
			%Y
			%m
			%d
			%H
			...
			专门用来解决linux的bug的   文件夹的第一级字目录下 最多存储65535个文件
	案例：
            def image_field(request):
                  if request.method == "GET":
                      return render(request, 'image_field.html')
                  elif request.method == "POST":
					username = request.POST.get("username")
                      icon = request.FILES.get("icon")
                      user = UserModel()
                      user.u_name = username
                      user.u_icon = icon
                      user.save()
                      return HttpResponse("上传成功%d" % user.id)
            模型：
            class UserModel(models.Model):
                  name = models.CharField(max_length=64)
                  #ImageField依赖Pillow库 所以需要安装  pip install pillow
                  #upload_to 依赖MEDIA_ROOT
                  icon = models.ImageField(upload_to='%Y/%m/%d/icons')
                  
 实现步骤：
         （1）表单的提交方式必须是post
         （2）添加表单的属性enctype = mutipart/form-data
         （3）在settings中设置MEDIA_ROOT = os.path.join(BASE_DIR,'XXX')
         （4）创建模型  模型的属性是imagefield 
         （5）注意imagefield依赖于pillow
          (6)imagefield的约束是upload_to 该属性值和MEDIA_ROOT会进行拼接
         （7）实例化对象 然后save保存即可
```

# 四、缓存

```
目的：
	缓解服务器的读写压力
	提升服务器的响应速度
	提升用户体验
	将执行过的操作数据 存储下来，在一定时间内，再次获取数据的时候，直接从缓存中获取
	比较理想的方案，缓存使用内存级缓存
	Django内置缓存框架
	存储中间数据的一种介质
原则：
    较少的代码
    对缓存后端封装一致性操作
    有点类似于ORM的感觉
    可扩展性
    应该存在通用基类
```

## Django内置缓存实现（三种方案）

```
（1）使用系统封装的
	装饰器封装在视图函数上
		@cache_page(30)
		需要注意的是不需要写timeout
	模板中也可以缓存--django内置得数据库缓存
		@cache_page(30)
		def testCache1(request):
			time.sleep(5)
			return HttpResponse('testCache1')
	    数据库缓存相对比较低效
```

```
（2）基于数据库：在真实的数据库中去创建缓存表
	（1）创建缓存表
		python manage.py createcachetable [table_name]
	（2）settings中配置缓存信息
		CACHES
			default
				'BACKEND': 'django.core.cache.backends.db.DatabaseCache'
				'LOCATION': 'my_cache_table'
				'TIMEOUT': 60 * 5  缓存时间以set方法为主
    eg：
    CACHES={
              'default':{
                  'BACKEND':'django.core.cache.backends.db.DatabaseCache',
                  'LOCATION':'my_cache_table',
                  'TIMEOUT':60,
                  'KEY_PREFIX':'python190x',
              }
           }
```

```
（3）基于redis-内存级数据库
	Django-redis-cache
		使用redis实现django-cache的扩展
		操作缓存的API没有发生任何变更
		变更的就是连接缓存的配置
	常见的有两个实现
		django-redis 
			http://django-redis-chs.readthedocs.io/zh_CN/latest/#django
			pip install django-redis
		django-redis-cache
			https://pypi.python.org/pypi/django-redis-cache/
			pip install django-redis-cache
	基本配置
		CACHES={
                    'redispython190x':{
                        'BACKEND':'django_redis.cache.RedisCache',
                        'LOCATION':'redis://127.0.0.1:6379/1',
                        'OPTIONS':{
                                'CLIENT_CLASS':'django_redis.client.DefaultClient'
                        }
                    }
                }
	查看redis缓存
		select 1
		keys *
		get :1:news
		查看过期时间  tts  :1:news
```

```
多缓存：
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.db.DatabaseCache',
        'LOCATION': 'my_cache_table',
        'TIMEOUT': 60 * 5

    },

    'redis_backend': {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
	写多套配置，定义不同的名字
	存入缓存的时候，获取不同的缓存对象
	想使用哪个缓存就创建哪个缓存的实例对象
	
	装饰器缓存
		@cache_page(30, cache='cache_name')
		可以使用装饰器 指定想要的数据库
	数据库缓存
		 cache = caches['cache_name']
```

# 五、中间件

## (1)概念：

- 中间件是一个轻量级，底层的插件，可以介入到Django的请求和响应过程（面向切面编程）
- 中间件的本质就是一个python类
- 面向切面编程(Aspect Oriented Programming)简称AOP。AOP的主要实现目的是针对业务处理过程中的切面进行提取，它所面对的是处理过程中的某个步骤或者阶段，以获得逻辑过程中各部分之间低耦合的隔离效果

![](/home/shenyang/Desktop/每日资料/Django资料/day06/doc/media/aop.png)

```
django内置的一个底层插件
从属于面向切面编程AOP
	在不修改源代码的情况下，动态去添加一些业务逻辑处理
中间件的典型实现 装饰器
	中间件就是使用类装饰实现的
```

## (2)面向对象编程

````
	切点
		（1）process_request
			process_request(self,request):在执行视图前被调用，每个请求上都会调用，不主动进行返回或返回HttpResponse对象
			
		（2）process_view
			process_view(self,request,view_func,view_args,view_kwargs)：调用视图之前执行，每个请求都会调用，不主动进行返回或返回HttpResponse对象
			
		（3）process_template_response	
			process_template_response(self,request,response):在视图刚好执行完后进行调用，每个请求都会调用，不主动进行返回或返回HttpResponse对象
			
		（4）process_response
			process_response(self,request,response):所有响应返回浏览器之前调用，每个请求都会调用，不主动进行返回或返回HttpResponse对象
			
		（5）process_exception
			process_exception(self,request,exception):当视图抛出异常时调用，不主动进行返回或返回HttpResponse对象
	切面
		切点处切开可以获得的数据
````

## (3)实现步骤

````
实现步骤：
书写，自定义中间件
	1. 在工程目录下创建middleware目录
	2. 目录中创建一个python文件
	3. 在python文件中导入中间件的基类
	from django.utils.deprecation import MiddlewareMixin
	4. 在类中根据功能需求，创建切入需求类，重写切入点方法
	class LearnAOP(MiddlewareMixin):
		def process_request(self,request):
			print('request的路径',request.GET.path)
	5. 启用中间件，在settings中进行配置，MIDDLEWARE中添加
	middleware.文件名.类名
````

## (4)应用

```
应用：
      白名单
      def get_phone(request):
          if random.randrange(100) > 95:
              return HttpResponse("恭喜你抢到了小米8")
           return HttpResponse("正在排队")
      if request.path == "/app/getphone/":
              if ip == "127.0.0.1":
                  if random.randrange(100) > 20:
                          return HttpResponse("恭喜您免费获取小米8 256G版")
       黑名单
            if request.path == "/app/getticket/":
                   if ip.startswith("10.0.122.1"):
                        return HttpResponse("已抢光")
       作业：如果一分钟之内访问了10次 那么返回 小爬虫快走开，如果1分钟之内访问了30次 封ip 5分钟  正常访问 返回来了老弟
```

```
当某一段业务逻辑发生了错误  那么就会执行process_exception方法
process_exception
	界面友好化 应用交互友好化
	def process_exception(self, request, exception):
	        print(request, exception)
	        return redirect(reverse('app:index'))
```

## (5)注意：

中间件的执行顺序

中间件注册的时候是一个列表

 如果我们没有在切点处直接进行返回，中间件会依次执行

 如果我们直接进行了返回，后续中间件就不再执行了

# 六、分页器

## (1)概念

分页是了提升用户体验，并且减小服务器的负担而开发的

分页：
    真分页   每一次点击下一页或者上一页 都会像数据库发送请求 并且返回数据
    假分页   一次性读取所有数据  然后再内存中进行分页
    企业级开发中常用 真分页   

```
原生实现：
偏移加限制
	offset  limit
	students = Student.objects.all()[per_page*(page-1): page * per_page]
```

## (2)封装实现

```
封装实现
	Paginator（分页工具）
		对象创建
			:Paginator(数据集，每一页数据数)
			paginator = Paginator(students, per_page)
		属性
			count对象总数
			num_pages：页面总数
			page_range: 页码列表，从1开始
		方法:
			page(整数): 获得一个page对象
				       该方法的返回值类型是Page
		常见错误:
			InvalidPage：page()传递无效页码
			PageNotAnInteger：page()传递的不是整数
			Empty：page()传递的值有效，但是没有数据
	Page（具体哪一页）
		对象获得
			通过Paginator的page()方法获得
		属性
			object_list：	当前页面上所有的数据对象
			number：	当前页的页码值
			paginator:	当前page关联的Paginator对象
		方法
			has_next()	:判断是否有下一页
			has_previous():判断是否有上一页
			has_other_pages():判断是否有上一页或下一页
			next_page_number():返回下一页的页码
			previous_page_number():返回上一页的页码
			len()：返回当前页的数据的个数
			
			
应用场景：paginator对象  适用于 页码的遍历  eg 上一页 xxx  下一页
         page对象       适用于 是否有上一页 下一页  上一页页码  下一页页码 
```

# 七、富文本

## (1)概念：

富文本:Rich Text Format（RTF），是有微软开发的跨平台文档格式，大多数的文字处理软件都能读取和保存RTF文档，其实就是可以添加样式的文档，和HTML有很多相似的地方

写论坛，博客时使用的一种带样式的文本插件

## (2)插件的使用方式

```
		（1）安装插件
			pip install django-tinymce
		（2）在instatlled_app中添加tinymce
		（3）初始化
			在settings中注册tinymce应用
                  设置默认的配置文件
                      TINYMCE_DEFAULT_CONFIG = {
                            'theme':'advanced',
                            'width':800,
                            'height':600,
                  		}
		（4）创建模型
			from tinymce.models import HTMLField
                class Blog(models.Model):
                    sBlog = HTMLField()
		（5）使用
			在自己的页面中使用
			对应的输入方式 文本域 <textarea></textarea>
			引入tinymce
				<script type="text/javascript" src="/static/tiny_mce/tiny_mce.js"></script>
			初始化绑定文本域
				<script type="text/javascript">
                       tinyMCE.init({
                              "mode": "textareas",
                              "theme": "advanced",
                              "width": 800,
                              "height": 600
                          })
				</script>
```

# 八、thefuck

## (1)概念

```
一个终端指令修复工具
	当指令在输入错误的时候，我们可以通过fuck进行弥补
		可以提供指令修复方案
		enter
			确定
		control+c
			取消
		↑↓ 
			调整
```

## (2)使用

```
		（1）sudo apt update
		（2）sudo apt install python3-dev python3-pip
		（3）sudo pip3 install thefuck
		（4）更新环境变量
                      vim ~/.bashrc
                      eval "$(thefuck --alias fuck)"
                      source ~/.bashrc
```

