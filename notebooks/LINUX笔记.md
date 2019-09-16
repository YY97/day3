# 一、Linux文件的基本属性

**每个文件的属性由左边第一部分的10个字符（如上的“dr-xr-xr-x”）来确定。**我们把十个字符拆开看：

- **10位字符表示：**

- **0位：**确定文件类型

- **1-3位：**确定该文件的所有者对文件的权限 **owner**

- **4-6位：**确定所有者的同组用户拥有该文件的权限 **group**

- **7-9位：**确定其他用户拥有该文件的权限 **others**

- **第一个字符：**代表这个文件的类型，是目录、文件，还是一个链接等等

- **[** **d** **]** 目录

- **[** **-**  **]** 文件

- **[** **l**  **]** 链接文档(link file)

- **[** **b** **]** 可供储存的接口设备(可随机存取装置)

- **[** **c** **]** 串行端口设备，例如键盘、鼠标(一次性读取装置)

- **接下来的字符：**以三个一组分成三组，用 r、w、x 三个参数的组合表示，位置不会改变

- **[ r  ]** 代表可读(read)

- **[ w ]** 代表可写(write)

- **[ x  ]** 代表可执行(execute)

- **[  -  ]** 没有权限

# 二、shell是什么

**Kernel**
Kernel 是操作系统的核心,直接与硬件打交道,处理很多底层的事情。
一般禁止普通用户直接操作,外部程序想要调用内核功能需要使用 “系统调用” 的接口

![](/home/shenyang/Pictures/15.png)

**Shell**
Shell 是一个应用程序,它连接了了用户和 Linux 内核,让用户能够更更加高效、安全、低成本地使用用
Linux 内核,这就是 Shell 的本质。
Shell 一一般分为 “用户界面面 (GUI)” 和 “命令行行 (CLI)” 两种
**常⻅的 GUI Shell:**Gnome,KDE,Xface
**常见的 CLI Shell:**
	sh: Bourne shell, 史蒂夫·伯恩在⻉尔实验室时编写。1978年年随Version 7 Unix首首次发布。
	csh: C shell, 比尔·乔伊在加州大学伯克利分校时编写。1979年年随BSD首次发布。
	bash: Bourne-Again shell, 1987年年由布莱恩·福克斯为了GNU计划而编写。原先是计划用在GNU操作系统上,但能运行于大多数类Unix系统的操作系统之上,包括Linux 与 MacOS 都将它作为默认shell。是应用用最广的 Shell。
	zsh: Z shell, 名称的含义是 “The last shell you’ll ever need!”,Zsh 对 Bourne shell做出了大量改进,同时加入了其他shell的某些功能,强化了自动补全功能,还加入了插件机制,定制性非常高,功能最为强大。
	可以通过 cat /etc/shells 查看当前系统安装了了哪些 Shell

### **Bash快捷键**：

```
ctl + f 前进一一个字符
ctl + b 后退一一个字符
ctl + a 回到行行行首首
ctl + e 回到行行行尾
ctl + w 向左删除一一个单词
ctl + u 向左删除全部
ctl + k 向右删除全部
ctl + y 粘贴上次删除的内容
ctl + l 清屏
```

# 三、shell echo命令

shellde echo指令用于字符串的的输出

命令格式：

```
echo string
```

## 1、显示普通字符串

```
echo "It is a test"
```

双引号可以省略

## 2、显示转义字符

```
echo "\"It is a test\""
```

```
结果是："It is a test"
```

双引号可以省略

# 四、Linux文件与目录管理

 **绝对路径：**
路径的写法，由根目录 / 写起，例如： /usr/share/doc 这个目录。

 **相对路径：**
路径的写法，不是由 / 写起，例如由 /usr/share/doc 要到 /usr/share/man 底下时，可以写成： cd ../man 

## 1、处理目录的常用命令

- ls: 列出目录
- ls-l:列出当前目录下的文件的详细信息
- cd或cd~：切换目录(回当前用户的宿主目录)
- cd.. :回到当前目录的上一级目录
- cd-:回到上一次所在的目录
- pwd：显示目前的目录的绝对路径
- mkdir：创建一个新的目录
- mkdir -p a/b/c:创建三层目录结构a/b/c
- mkdir -p a/{b,c}/{d,e,f} ：同:一层级创建多个
- rmdir：删除一个空的目录
- cp: 复制文件或目录
- rm: 移除文件或目录
- rm-rf:非空目录名，删除一个非空目录下的一切
- mv: 移动文件与目录，或修改文件与目录的名称

你可以使用 *man [命令]* 来查看各个命令的使用文档，如 ：man cp

## 2、Linux文件内容查看

- cat   由第一行开始显示文件内容
- tac   从最后一行开始显示，可以看出 tac 是 cat 的倒著写！
- nl   显示的时候，顺道输出行号！
- more 一页一页的显示文件内容
- less 与 more 类似，但是比 more 更好的是，他可以往前翻页！
- head 只看头几行
- tail 只看尾巴几行

### (1)文件操作：

**命令列表：**

cp aa ../bb/:  将 aa 文件复制到 ../bb 目目录
mv aa ../bb:  将 aa 文件移动到 ../ 并更名为 bb
rm foo:  删除名为 foo 的文件
touch abc:  在当前文件夹创建一个 abc 文件, 如果已存在则跳过
ln -s abc def:  为 abc 文件创建一个软链接

**cp/mv/rm的通用参数：**

-i : 覆盖前提示
-n : 如果目标文件已存在,则停止止操作
-f : 如果目标文件已存在,则强制操作,覆盖前不不提示
-r : 递归对文件夹执行行某操作 ( mv 不需要 -r )

### (2)硬链接与软连接：

**硬连接 **      ln foo bar

只能在同分区内创建
一个文件的多个硬链接相当于一个文件有多个名字,多个硬链接在磁盘上只占用一个文件的大小
修改硬链接时,所有同源的硬链接都会发生生变化

**软连接**          ln -s foo bar

可以跨越分区创建
内部只记录目标文件的路径,类似于 Windows 下的 “快捷方式”
通过软链接修改文件,源文件也会发生修改

**实验**：

```
[oracle@Linux]$ touch f1          #创建一个测试文件f1
[oracle@Linux]$ ln f1 f2          #创建f1的一个硬连接文件f2
[oracle@Linux]$ ln -s f1 f3       #创建f1的一个符号连接文件f3
[oracle@Linux]$ ls -li            # -i参数显示文件的inode节点信息
total 0
9797648 -rw-r--r--  2 oracle oinstall 0 Apr 21 08:11 f1
9797648 -rw-r--r--  2 oracle oinstall 0 Apr 21 08:11 f2
9797649 lrwxrwxrwx  1 oracle oinstall 2 Apr 21 08:11 f3 -> f1
```

从上面的结果中可以看出，硬连接文件 f2 与原文件 f1 的 inode 节点相同，均为 9797648，然而符号连接文件的 inode 节点不同。

```
[oracle@Linux]$ echo "I am f1 file" >>f1
[oracle@Linux]$ cat f1
I am f1 file
[oracle@Linux]$ cat f2
I am f1 file
[oracle@Linux]$ cat f3
I am f1 file
[oracle@Linux]$ rm -f f1
[oracle@Linux]$ cat f2
I am f1 file
[oracle@Linux]$ cat f3
cat: f3: No such file or directory
```

通过上面的测试可以看出：当删除原始文件 f1 后，硬连接 f2 不受影响，但是符号连接 f1 文件无效

**总结：**

 依此您可以做一些相关的测试，可以得到以下全部结论：

-  1).删除符号连接f3,对f1,f2无影响；
-  2).删除硬连接f2，对f1,f3也无影响；
-  3).删除原文件f1，对硬连接f2没有影响，导致符号连接f3失效；
-  4).同时删除原文件f1,硬连接f2，整个文件会真正的被删除。

## 3、压缩文件处理

```
tar
压缩: tar -czf abc.tar.gz abc/
解压: tar -xzf abc.tar.gz
zip
压缩: zip -r abc.zip abc/ 把abc压缩成abc.zip
解压: unzip abc.zip
```

## 4、查找文件find命令

```
查找当前文件夹下全部文件: find ./

只查找文件: find ./ -type f

只查找目录: find ./ -type d

只查找链接: find ./ -type l

按名称查找: find ./ -name '*.py'

按权限查找: find ./ -perm 0644

按大小查找: find ./ -size +1k -size -5k

以txt结尾的文件：find./-name'*.text'

```

# 五、Linux中的用户与组

Linux系统是一个多用户任务的分时操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号

[GID](https://www.baidu.com/s?wd=GID&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao) 是用户组ID (group ID) 

UID 是用户ID (user ID) 

```
每个用户都有唯一的用户名,并且 Linux 会分配一个唯一的 UID 与之对应。

同样每个用户组也有唯一的名称,Linux 会分配一个唯一的 GID 给每一一个用户组。

root 用用户的 uid 和 gid 都是 0

用户名与 UID 的对应关系记录在 /etc/passwd 中。

用户组与 GID 的对应关系记录在 /etc/group 中。

用户的密码信息记录在 /etc/shadow中

```

```
cat /etc/passwd  #查看用户信息

cat /etc/shadow  #查看用户的密码信息

cat /etc/group   #查看用户的组信息

```

## passwd格式(查看用户信息)

root ：x :0:0:root:/root:/bin/bash

```
用户信息的显示有7个字段

      字段1：用户名  --> root
      字段2：密码占位符  --> x （这里都是用x代替）
      字段3：uid，用户id  --> 0
      字段4：gid ，组id --> 0
      字段5：用户描述信息  --> root
      字段6：家目录  -->  /root
      字段7：登录 shell   （用户登陆shell ，当为/bin/bash表示可以登陆，/sbin/nologin表示不被授权登陆）
```

## shadow格式(查看用户密码信息)

单行样例root:$1$lrKCOpzq$IHP2BuuKxMdLaBw/:17877:0:99999:7:::

```
  密码信息的显示有9个字段
  
  字段1：用户名
  字段2：通过sha-512加密(二次加密，在经过第一次加密后，第二次加入随机数再次加密)的密码
  字段3：最后一次修改密码距离1970年1月1日的天数间隔
  字段4：密码最短有效期
  字段5：密码最长有效期
  字段6：密码过期前几天进行警告
  字段7：账户过期后，被锁定的天数
  字段8：账号失效时间距离1970年1月1日的天数间隔
  字段9：未分配功能

```

## group格式(查看组信息)

单行案例：root:x:0

```
组信息的显示有四个字段

      字段1：组名称 --> root
      字段2：组密码占位符  --> x
      字段3：gid --> 0
      字段4：组成员

```

# 六、用户管理

## 1、添加用户

**新建用户：**

```
     新建用户时，系统会将 /etc/skel 中的目录及文件拷贝到新建用户的家目录中
     在 /var/spool/mail 中，新建用户名的邮箱 
     在 /etc下的 passwd 、shadow 、group文件中，增加用户信息
```

**添加用户时的指定参数：**

```
添加用户时，使用 -g 指定新建用户的组，使用 -u 指定用户uid
-G 参数可以指定新建用户的附加组
使用  -s   /sbin/nologin  指定创建的用户没有登录系统的权限
还可以使用 -M 参数，指定创建的用户不在home目录下创建家目录
还可以使用 -d 参数 ，指定其家目录

```

**用法**: useradd -mU -G 组名 -p 密码 用户名
**参数详解:**
-G GROUPS : 新账户的附加组列列表
-m : 在 /home 目录创建用户的家目录
-U : 创建与用户同名的组
-p PASSWORD : 加密后的新账户密码

## 2、删除用户

**用法:** userdel -r 用户名

**参数详解:**
-r : 删除主目录和邮件池

```
不加 -r 参数，只删除 passwd、shadow 和 group 文件中的用户信息，/home 目录下的文件不删除，/var/spool/mail/ 下的文件不删除
加  -r 参数，删除 passwd、shadow 和 group 文件中的用户信息，同时删除用户的家目录和邮箱

```

## 3、修改用户密码

**用法：**passwd 用户名

```
   当前用户为 root 时：
	不需要知道当前的密码
    设置新密码时，不需要遵循密码要求

    当前用户为普通用户时：
    需要知道当前密码
    设置新密码时，必须遵循密码要求（1.不能少于8个字符，2.满足复杂度要求）
```

## 4、切换账户

**用法1:** su 用户名 : 仅切换用户身份
**用法2:** su -用户名 : 完全以这个用户进行登录,会初始化当前用户的设置

# 七、用户组管理

## 1、添加组

**用法：**groupadd [选项] 组名

**选项:**

```
-g GID : 为新组使用 GID

-p PASSWORD : 为新组使用此加密过的密码

-r : 创建一个系统账户

```



## 2、删除组

**用法：**groupdel 组名

## 3、修改用户属性

**用法:** usermod [选项] 用户名
**选项:**

```
-d HOME_DIR : 用户的新主目录

-g GROUP : 强制使用 GROUP 为新主组

-G GROUPS : 新的附加组列表 GROUPS

-a GROUP : 将用户追加至上边 -G 中提到的附加组中,并不从其它组中删除此用户

-L : 锁定用户帐号

-m : 将家目录内容移至新位置 (仅于 -d 一一起使用用)

-s SHELL : 该用户帐号的新登录 shell

-U : 解锁用户帐号

```

## 4、查看登陆的用户

```
who 查看谁正在登录

w 查看谁正在登录,并在显示每个登陆用户正在执行的任务

last 查看历史登陆记录

lastb 查看失败的登陆记录

lastlog 查看全部用户最后一次登陆的时间
```

# 八、文件的权限

## 1、权限的定义

| 标记 | 含义            |
| ---- | --------------- |
| r    | read,读权限     |
| w    | write,写权限    |
| x    | excute,执行权限 |

用户的三种身份：

1. owner 文件拥有者
2. group 同组人
3. other 其他人

使用用 ls -l 可以看到文文件的权限信息:
-rwxr-xr-- 1 bob staff  9824 8 28 21:22 test.py
-rw-r--r-- 1 tom staff 10787  8 27 12:57 01.md
-rw-r----- 1 tom staff 5053 8 28 23:42 sun.jpg

最左边一列就是每个文件的权限信息,共包含 9 个基本权限,分别是 owner / group / others 三种身份各有自己的 read / write / execute 权限。
以 -rwxr-xr-x 为例,第一个字符可以忽略,后面的 9 个字符分为三组:

1. rwx : 文件拥有者对该文件具有 “读、写、可执行” 的权限
2. r-x : 同组人人具有 “读、可执行” 的权限,没有写权限
3. r-- : 其他人只有 “读” 权限

## 2、权限的修改

### 通过符号修改权限

![](/home/shenyang/Pictures/16.png)

**例如：**

```
设置自己可读可写可执行,同组可读可执行,其他人可执行: chmod u=rwx,g=rx,o=x，test.py
给自己和同组人增加读写权限: chmod ug+rw abc.png
给同组人和其他人删除写权限: chmod go-w abc.png
给所有人增加执行权限: chmod a+x test.py
```

**r 读权限read  4**

**w 写权限write 2**

**x 操作权限execute  1**

```
例1 chmod 753 test.py

身份: 7 / 5 / 3 这三个数字分别对应着 owner / group / others 三个身份

权限值: 7/5/3这三个数字转成三位二进制数字分别为 111 / 101 / 011 
```

------

| 数字 | 二进制 | 权限 |
| ---- | ------ | ---- |
| 7    | 111    | rwx  |
| 5    | 101    | r-x  |
| 3    | 011    | -wx  |

## 3、修改文件拥有者

**用法:** chown  用户:组  文件

# 九、文本操作

```
echo xyz : 打印文本
echo xyz > a.txt : 将输出的文本重定向到文件a.txt中,a.txt原有内容会被覆盖
echo xyz >> a.txt : 将输出的文本追加到文件a.txt中,a.txt原有内容不不会被覆盖
cat 文件名 : 查看文文件
head -n N 文件名 : 查看文件的前 N 行
tail -n N 文件名 : 查看文件的后 N 行
less less文件 : 快速浏览文文件
    按 j 向下
    按 k 向上
    按 f 向下翻屏
    按 b 向上翻屏
    按 g 到全文开头
    按 G 到全文结尾
    按 q 退出
sort  文本或文件 : 将结果按升序排序
sort  -r 文本或文件 将结果按降序排序
uniq  去重, 依赖排序, 常跟在 sort 后面使用
awk  '{print $N}' 打印出相关列
wc 字符统计
    -c : 统计字符
    -w : 统计单词
    -l : 统计行
    例如: 统计代码行数 wc -l abc.py
管道符: 
	管道符可以连接两个命令,将前面的输出作为后面的输入
文本过滤 grep
	-i 忽略大小写
	-I 忽略二进制文件
	-r 递归查找目录
	-n 打印行号
	-c 只显示匹配到的个数
	-l 只显示匹配到的文件列表
	-o 只显示匹配到的单词
	-v 忽略制定的字段
	-E 通过正则表达式匹配
	--include=‘*.py' 仅包含py文件
	--exclude='*.js' 不包含js文件
```

# 十、vim

VIM 分为三种模式:命令模式,插入入模式,底栏命令模式

## 1、按 esc 键,进入命令模式

```
h, j, k, l 光标左、下、上、右移动
ctl + e 向下滚动
ctl + y 向上滚动
ctl + f 向下翻屏
ctl + b 向上翻屏
yy 复制整行yw 复制整行
p 粘贴到下一行
P 粘贴到上一行
dd 删除整行
d3w 向前删除3个单词
7x 删除7个字符
u  撤销
ctl + r 重做
c3w 剪切3个单词
gg 跳至文件首行
shift + g 跳至文件结尾
shift + h 跳至屏幕首行
shift + m 跳至屏幕中间
shift + l 跳至屏幕结尾
ctl + v 列编辑
shift + v 选中整列
shift + > 向右缩紧
shift + < 向左缩紧
```

## 2、按 i 键,进入插入模式

```
插入模式下正常输入即可
想做其他操作,必须先按 ESC 键回到命令模式
```

## 3、在命令模式时按 : 键,进入底栏命令模式

```
23 跳至至文件的第 23 行
%s/abc/123/g 把文件中所有的 abc 替换成 123
set nu 打开行号
set nonu 关闭行号
w 保存
q 退出
wq 保存并退出
```

## 4、vim配置文件



**~/.vimrc**

**学习网站：**

```
https://coolshell.cn/articles/5426.html
http://www.oschina.net/question/615783_148433
```

1. echo xyz:打印文本

2. echo xyz > a.txt: 将输出的文本重定向到文件的a.txt中，a.txt原有的内容会被覆盖

3. echo xyz >> a.txt: 将输出的文本追加到文件的a.txt中，a.txt原有的内容会不被覆盖

4. cat 文件名：查看文件

5. head -n N 文件名：查看文件的前N行

6. tail -n N 文件名：查看文件的后N行

7. less 文件：快速浏览文件

   - 按 j 向下
   - 按 k 向上
   - 按 f 向下翻屏
   - 按 b 向上翻屏
   - 按 g 到全文开头
   - 按 G 到全文结尾
   - 按 q 退出

   sort  文本或文件 : 将结果按升序排序
   sort  -r 文本或文件 将结果按降序排序
   uniq  去重, 依赖排序, 常跟在 sort 后面使用
   awk  '{print $N}'  打印出相关列

# 十一、进程状态

Linux是一个多任务操作系统，同一时刻允许多个任务同时工作，工作中的每一个任务就是一个进程，查看进程信息常用的命令有ps和top

## 1、ps命令

**功能描述**：ps 即 process status 的意思,用来查看进程状态。它显示的是敲下命令后一瞬间的进程状态，显示进程信息。

ps命令支支持3种不同类型的命令行参数:

.	Unix风格的参数,前面加 - ,如 ps -ef
. ​	BSD⻛格的参数,前面不加 - ,如 ps aux
. ​	GNU⻛格的长参数,前面加 -- ,如 ps --pid 123

个人是对这个命令是习惯BSD风格的，也就是习惯使用ps aux 而不是ps -ef。 这个命令经常配合grep使用

**ps -ef**

```
[root@boss ~]# ps -ef
UID   PID PPID  C   STIME   TTY   TIME     CMD
root 	1 	0 	0 	6月21 	?	00:26:10  /usr/lib
```

参数详解：

```
-e : 参数指定显示所有运行在系统上的进程
-f : 参数则扩展了输出
每列详解
    UID: 启动这些进程的用户。
    PID: 进程的进程ID。
    PPID: 父进程的进程号(如果该进程是由另一个进程启动的)。
    C: 进程生命周期中的CPU利利用用率。
    STIME: 进程启动时的系统时间。
    TTY: 进程启动时的终端设备。
    TIME: 程序累计占用 CPU 的时间
    CMD: 进程运行的命令
```

**ps aux**

```
[root@boss ~]# ps aux
USER  PID  %CPU  %MEM  VSZ  RSS   TTY   STAT   START 
root	1	0.0	 0.0   948  4000   ?    Ss     6月21


TIME    COMMAND

26:10  /usr/libsystemed
```

参数详解:

```
a : 显示跟任意终端关联的所有进程
u : 采用基于用户的格式显示
x : 显示所有的进程,甚至包括未分配任何终端的进程
每列信息
    USER : 执行这个进程的用户
    PID : 进程 ID
    %CPU : 当前进程的 CPU 占用
    %MEM : 当前进程的 内存 占用
    VSZ : 进程占用的虚拟内存大小,以千字节(KB)为单位。
    RSS : 进程占用的物理内存大小
    TTY : 进程启动时的终端设备。
    STAT : 进程状态
    START : 进程启动时刻
    TIME : 程序累计占用 CPU 的时间
    COMMAND : 启动进程的命令
关于STAT
	代表当前进程状态的双字符状态码。
	第一个字符表明进程状态:
        O : 代表正在运行
        S : 代表在休眠
        R : 代表可运行,正等待 CPU
        Z : 代表僵化,进程已结束但父进程已不存在
        T : 代表停止
	第二个参数进一步说明进程的状态细节:
        < : 该进程运行在高高优先级上。
        N : 该进程运行在低优先级上。
        L : 该进程有⻚面锁定在内存中。
        s : 该进程是控制进程。
        l : 该进程是多线程的。
        + : 该进程运行在前台。
```

## 2、top命令

ps 命令只能查看一瞬间的进程状态,如果想要持续查看某些进程的状态可以使用 top

![](/home/shenyang/Pictures/11.png)

**头信息逐行详解：**

```
1. 系统运行的整体状态: 开机时长,登陆用户数,系统负载
    系统负载: load average: 0.00, 0.02, 0.05
    分别代表: 一分钟负载,五分钟负载,十五分钟负载
    负载值越高代表服务器压力越大
    负载值不要超过 CPU 的核心心数。如果超过核心心数意味着有很多进程在等待使用 CPU
与 uptime 命令的结果一一样 (查看系统状态)
2. 任务情况: 任务总数,运行中的数量,休眠数量,停止数量,僵尸进程数量
3. CPU 使用情况:
    us: (user) 用户态占用
    sy: (system) 内核态占用
    id: (idle) 空闲的 CPU
4. 内存占用情况: 内存总量, 空闲内存, 使用的内存, 缓冲区占用用的内存
5. 交换分区的占用
    交换分区是一种将内存数据保存到硬盘的技术,一般在内存不不足足的时候使用
```

**进程区详解 ：**

```
PID: 进程的ID。USER: 进程属主的名字。
PR: 进程的优先级。
NI: 进程的谦让度值。
VIRT: 进程占用的虚拟内存总量。
RES: 进程占用的物理内存总量。
SHR: 进程和其他进程共享的内存总量。
S: 进程的状态 (与 ps 基本相同)。
%CPU: 进程使用的CPU时间比比例例。
%MEM: 进程使用的内存占可用内存的比例。
TIME+: 自进程启动到目前为止的CPU时间总量量。
COMMAND: 进程所对应的命令行名称,也就是启动的程序名。
```

- **技巧：**

  进程太多时，可以通过-p参数指定需要查看的进程ID,让进程信息更加精简

  ```
  top -p PID1,PID2,PID3......
  ```

## htop

如果感觉 top 不够直观,可以使用 htop

**安装: sudo apt install htop**

# 十二、进程的管理

kill:杀死进程，或者给进程发送信号

​	-1（HUP）平滑启动

​	-9（KILL）强制杀死进程

​	-15（TERM）正常终止进程（kill默认情况）

pkill [processName]按名字进行处理

killall [MatchedProcessName]处理名字匹配的进程

# 十三、其他状态

## 1、内存状态 free

```
[root@localhost ~]# free -m
  total    used    free   shared   buffers    
  725      677      66     1551     556
```

 total 是总内存数；

 used 是已经使用的内存数；

 free 是空闲的内存数；

 shared 是多个进程共享的内存总数；

 buffers 是缓冲内存数；

| **-b** | **以 Byte（字节）为单位，显示内存使用情况。**                |
| ------ | ------------------------------------------------------------ |
| **-k** | **以 KB 为单位，显示内存使用情况，此选项是 free 命令的默认选项。** |
| **-m** | **以 MB 为单位，显示内存使用情况。**                         |
| **-g** | **以 GB 为单位，显示内存使用情况。**                         |

## 2、硬盘

iostat :  查看硬盘写入和读取的状态
df -lh :  查看硬盘分区,及每个分区的剩余空间
du -hs ./ :  查看当前目录占用的硬盘大小

## 3、网络状态

```
ifconfig 查看网网卡状态, 常用用来检查自自身 IP 地址
netstat -natp 查看网网络连接状态
    -a : 显示所有选项
    -t : 显示所有与TCP相关的选项
    -u : 显示所有与UDP相关的选项
    -x : 显示所有与Unix域相关的套接字选项
    -n : 拒绝显示别名,能显示数字的全部转换为数字显示
    -p : 显示建立相关连接的程序名。
    -l : 显示所有状态为Listen的连接
    -e : 显示扩展信息,如当前链接所对应的用户
    -c : 间隔一段时间执行一次netstat命令。
    -s : 显示统计信息。对每种类型进行汇总
ping -i 0.5 -c 100 xx.xx.xx.xx
    -i : 间隔
    -c : 数量量
    -q : 安静模式, 只打印结果
lsof
    lsof -i :[PORT] 查看占用端口的程序
    lsof -i tcp 查看所有 TCP 连接
    lsof -u abc 查看用户 abc 打开的所有文件
    lsof -p 123 查看 pid 为 123 的进程打开的所有文件
路由追踪: 
	traceroute [HOST]
DNS 查询
    dig [DOMAIN]
    host [DOMAIN]
    nslookup [DOMAIN]
```

## 4、时间和日期

date :  查看日期与时间

cal :  查看日历
	--one :  查看本月的日历
	--three :  查看最近三个月的日历
	--year :  查看全年的日历

## 5、下载

curl:  执行 HTTP 访问,也可用来下载
wget : 下载
scp :  在服务器之间上传或下载 scp root@x.x.x.x:/root/abc ./abc

# 十四、shell编程与运维

## 1、shell脚本概述

Shell 脚本一般是以 .sh 结尾的文本文件, 当然, 也可以省略扩展名

## 2、shell脚本首行

脚本文件第一行通过注释的方式指明执行脚本的程序。
在 Shell 脚本中, # 开头的文本是注释, 但第一句 #! 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一Shell。

echo 命令用于向窗口输出文本
常见方式有:

```
#!/bin/sh

#!/bin/bash

#!/usr/bin/env bash

```

Python 脚本的第一句一般是 #!/usr/bin/env python

### 多行注释 

多行注释还可以使用以下格式：

```
:<<EOF
注释内容...
注释内容...
注释内容...
EOF
```

EOF 也可以使用其他符号:

```
:<<'
注释内容...
注释内容...
注释内容...
'

:<<!
注释内容...
注释内容...
注释内容...
!
```

## 3、第一个脚本

打开文本编辑器(可以使用 vi/vim 命令来创建文件)，新建一个文件 test.sh，扩展名为 sh（sh代表shell），扩展名并不影响脚本执行，见名知意就好

**实例：**

```
#!/bin/bash
echo "Hello World !"
```

## 4、运行shell脚本的两种方法：

### **(1)作为可执行程序**

将上面的代码保存为 test.sh，并 cd 到相应目录：

```
chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
查看脚本的退出状态: echo $?
    Linux 中的所有程序执行行行结束后都有状态码
    状态码为 零 表示正常, 状态码为 正整数 代表异常退出
```

**注意**，一定要写成 ./test.sh，而不是 **test.sh**，运行其它二进制的程序也一样，直接写 test.sh，linux 系统会去 PATH 里寻找有没有叫 test.sh 的，而只有 /bin, /sbin,  /usr/bin，/usr/sbin 等在 PATH 里，你的当前目录通常不在 PATH 里，所以写成 test.sh 是会找不到命令的，要用  ./test.sh 告诉系统说，就在当前目录找。

###  **(2)作为解释器参数**

这种运行方式是，直接运行解释器，其参数就是 shell 脚本的文件名，如： 

```
/bin/sh test.sh
/bin/php test.php
```

这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。

## 5、变量

### (1)定义

变量的定义和其他语言差距不大，需要的注意的是赋值前后没有空格

```
# 变量量定义: 等号前后没有空格
a=12345
b=xyz
```

### (2)使用

使用变量时, 变量名前面加上 $ 符

```
echo "---$a---\n===$b==="
printf "---$a---\n===$b===\n"


your_name="qinjx"
echo $your_name
echo ${your_name}
变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界
```

### (3)注意 引号 的差别

**单引号**

```
str='this is a string'
```

 单引号字符串的限制： 

-  单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
-  单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

**双引号**

```
your_name='runoob'
str="Hello, I know you are \"$your_name\"! \n"
echo -e $str
```

输出结果

```
Hello, I know you are "runoob"! 
```

 双引号的优点：

- 双引号里可以有变量
- 双引号里可以出现转义字符

#### 拼接字符串

```
your_name="runoob"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1
# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
```

#### 获取字符串长度

```
string="abcd"
echo ${#string} #输出 4
```

#### 提取子字符串

以下实例从字符串第 **2** 个字符开始截取 **4** 个字符：

```
string="runoob is a great site"
echo ${string:1:4} # 输出 unoo
```

#### 查找子字符串

查找字符 **i** 或 **o** 的位置(哪个字母先出现就计算哪个)

```
string="runoob is a great site"
echo `expr index "$string" io`  # 输出 4
```

**注意：** 以上脚本中 ` 是反引号，而不是单引号 '

### (4)定义当前Shell下的全局变量

定义: export ABC=9876543210123456789

定义完后, 在终端里用 source 加载脚本: source ./test.sh

### (5)常用的系统环境变量

```
$PATH : 可执行行行文文件目目录
$PWD : 当前目目录
$HOME : 家目目录
$USER : 当前用用户名
$UID : 当前用用户的 uid
```

## 6、分支语句：if

分支控制语句完整格式为:

```
if command
then
	commands
elif command
	commands
else
	commands
fi
```

### (1)if 语句检查判断的依据实际上是, 后面所跟的命令的状态码: 0 为 true, 其他值 为 false

```
if ls /xxx
then
	echo 'exist xxx'
else
	echo 'not exist xxx'
fi
```

### (2)条件测试命令: [ ... ]

- shell 提供了一种专用做条件测试的语句 [ ... ]

- 这一对方括号本质上是一个命令, 里面的条件是其参数, 所以 [ 的后面和 ] 的前面必须有空格, 否则会报错。

- 他可以进行三种比比较

  数值比较

  字符串比较

  文件比较

- 用法:

```
if [ condition ]
then
	commands
fi
```

### (3)条件列表

**数值比较**

| condition | 说明                   |
| --------- | ---------------------- |
| n1 -eq n2 | 检查n1是否与n2相等     |
| n1 -ge n2 | 检查n1是否大于或等于n2 |
| n1 -gt n2 | 检查n1是否大于n2       |
| n1 -le n2 | 检查n1是否小于或等于n2 |
| n1 -lt n2 | 检查n1是否小于n2       |
| n1 -ne n2 | 检查n1是否不等于n2     |

**字符串比较**

| condition    | 说明                   |
| ------------ | ---------------------- |
| str1 = str2  | 检查str1是否和str2相同 |
| str1 != str2 | 检查str1是否和str2不同 |
| str < str2   | 检查str1是否比str2小   |
| str1 > str2  | 检查str1是否比str2大   |
| -n str1      | 检查str1的长度是否非0  |
| -z str1      | 检查str1的长度是否为0  |

**文件比较**

| condition       | 说明                                     |
| --------------- | ---------------------------------------- |
| -d file         | 检查file是否存在并且是一个目录           |
| -e file         | 检查file是否存在                         |
| -f file         | 检查file是否存在并且是一个文件           |
| -r file         | 检查file是否存在并且可读                 |
| -w file         | 检查file是否存在并且可写                 |
| -x file         | 检查file是否存在并且可执行               |
| -s file         | 检查file是否存在并且非空                 |
| -O file         | 检查file是否存在并属于当前用户所有       |
| -G file         | 检查file是否存在并且默认组与当前用户相同 |
| file1 -nt file2 | 检查file1是否比file2新                   |
| file1 -ot file2 | 检查file1是否比file2旧                   |

## 7、循环语句：for

shell中的循环结构有三种：for、while 和 until，重点介绍一下for循环

### for循环的基本结构

```
for 变量 in item1 item2 ... itemN（序列）
do
    command1
    command2
    ...
    commandN
done
```

写成一行：

```
for 变量 in item1 item2 ... itemN（序列）; do command1; command2… done;
```

练习：打印1 到10中的偶数

```
for i in `seq 1 10`
do
	if [[ $[ $i % 2] == 0 ]]
	then
		echo "偶数: $i"
	else
		echo "奇数: $i"
	fi
done
```

1. seq START END 语句用来产生一个数字序列
2. $[ NUM1 + NUM2 ] 语句用来进行基本的数学运算
3. [[ ... ]] 语句用来更方便的进行比较判断

**C语言风格的 for 循环**

```
for ((i=0; i<10; i++))
do
	echo "num is $i"
done
```





# 十五、函数

## 1、函数的定义

定义函数时function不是必须的，可以省略

```
function foo() {
    echo "---------------------------"
    echo "Hello $1, nice to meet you!"
    echo "---------------------------"
}
```

**说明：**

 1、可以带function fun()  定义，也可以直接fun() 定义,不带任何参数。 

 2、参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。

## 2、函数的使用

- 在终端或脚本中直接输入函数名即可,不需要小括号
- 传参也只需将参数加到函数名后面,以空格做间隔,像正常使用命令那样

```
foo seamile
```

## 3、函数的参数

在Shell中，调用函数时可以向其传递参数。在函数体内部，通过 $n 的形式来获取参数的值，例如，$1表示第一个参数，$2表示第二个参数... 

 带参数的函数示例： 

```
fun(){
    echo "第一个参数为 $1 !"
    echo "第二个参数为 $2 !"
    echo "第十个参数为 $10 !"
    echo "第十个参数为 ${10} !"
    echo "第十一个参数为 ${11} !"
    echo "参数总数有 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
}
fun 1 2 3 4 5 6 7 8 9 34 73
```

输出结果：

```
第一个参数为 1 !
第二个参数为 2 !
第十个参数为 10 !
第十个参数为 34 !
第十一个参数为 73 !
参数总数有 11 个!
作为一个字符串输出所有参数 1 2 3 4 5 6 7 8 9 34 73 !
```

**注意：**$10 不能获取第十个参数，获取第十个参数需要${10}。当n>=10时，需要使用${n}来获取参数。 

```
bar() {
	echo "执行者是 $0"
	echo "参数数量s是 $#"
	echo "全部的参数 $@"
	echo "全部的参数 $*"
    if [ -d $1 ]; then# 检查传入的第一个参数是否是文件夹
        for f in `ls $1`
        do
        	echo $f
    	done
    elif [ -f $1 ]; then
        echo 'This is a file: $1' # 单引号内的变量不会被识别
        echo "This is a file: $1" # 如果不是文件夹, 直接显示文件名
    else
    	echo 'not valid'#前面都不匹配显示默认语句
    fi
}
```

| 参数处理 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| $#       | 传递到脚本的参数个数                                         |
| $*       | 以一个单字符串显示所有向脚本传递的参数                       |
| $$       | 脚本运行的当前进程ID号                                       |
| $!       | 后台运行的最后一个进程的ID号                                 |
| $@       | 与$*相同，但是使用时加引号，并在引号中返回每个参数。         |
| $-       | 显示Shell使用的当前选项，与set命令功能相同。                 |
| $?       | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。 |

# 十六、获取用户输入

语法：read  -p  提示信息  变量名

案例：编写一个脚本test.sh，要求执行之后提示用户输入文件的名称（路径），然后自动为用户创建该文件

```
1 #！/bin/bash
2 read -p '请输入需要创建的文件路径：'filepath
3 touch $filepath
4 echo '文件创建成功’
5 ls -l $filepath
```

```
read -p "请输入一个数字：“ num
echo "您输入的是：$num"
```

