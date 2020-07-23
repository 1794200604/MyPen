Linux



#### 1. 常用命令

##### 	1.1 ls(list)

​	查看当前文件夹下的内容

##### 	1.2 pwd(print work diectory)

​	查看当前所在文件夹

##### 	1.3 cd [目录名]	(change directory)

​	切换文件夹

##### 	1.4 touch [文件名] (touch)

​	如果文件不存在，新建文件

##### 	1.5  mkdir [目录名] (make directory)

​	创建目录

##### 	1.6 rm [文件名]	(remove)

​	删除指定的文件名

##### 	1.7 clear(clear)

​	清屏



#### 2. 终端命令格式

```shell
command [-options] [parameter]
```

* command: 命令名，相应功能的英文单词或单词缩写

* -options: 选项，可用来对命令进行控制，也可以省略

* parameter: 传给命令的参数，可以使零个、一个或者多个



#### 3.查询命令帮助信息

##### 3.1 --help

```shell
command --help
```

说明：

* 显示 **command**命令的帮助信息



##### 3.2 man

```shell
man command
```

说明：

* 查阅 **command** 命令的使用手册

**man** 是 **manual** 的所写，是 **Linux** 提供的一个手册，包含了绝大部分的命令、函数的详细说明

##### 3.3 使用man时的操作键：

1. 空格键：显示手册页的下一屏
2. Enter键：一次滚动手册页的一行
3. b：回滚一屏
4. f：前滚一屏
5. q：退出
6. /word：搜索word字符串



#### 4. 文件和目录常用命令

##### 4.1 查看目录内容

###### 	4.1.1 ls

```shell
# 创建隐藏文件(以.开头的为隐藏文件)
touch .[文件名]
# 查看隐藏文件
ls -a
# 以列表方式显示文件的详细信息
ls -l
#  配合-l使用
ls -l -h
```

###### 	4.1.2 ls通配符的使用

  * 	*代表任意个数个字符
		* 	？代表任意一个字符
		* 	[] 表示可以匹配字符组中的任意一个
		* 	[abc] 匹配abc中任意一个
		* 	[a-f] 匹配a到f范围的字符

##### 4.2 切换目录

###### 	4.2.1 cd

```shell
# .表示当前目录
[xiaoyu@MYNET 桌面]$ cd .
[xiaoyu@MYNET 桌面]$ pwd
/home/xiaoyu/桌面
# ..表示上级目录
[xiaoyu@MYNET 桌面]$ cd ..
[xiaoyu@MYNET ~]$ pwd
/home/xiaoyu
```



###### 	4.2.2 cd常用命令

* cd ~ 切换到当前用户的主目录(/home/用户目录)
* cd . 保持在当前目录不变
* cd .. 切换到上级目录
* cd - 可以在最近两次工作目录之间来回切换

##### 4.3 创建和删除操作

###### 	4.3.1 touch

###### 	4.3.2 rm

* -f 强制删除，忽略不存在的文件，无需提示
* -r 递归地删除目录下的内容，删除文件夹时必须加此参数

###### 	4.3.3 mkdir

* -p 递归创建目录

* ```shell
  [xiaoyu@MYNET 桌面]$ mkdir -p a/b/c/d
  ```

  

##### 4.4 拷贝和移动文件

###### 	4.4.1 cp

* -f 已经存在的目标文件直接覆盖，不会提示
* -i 覆盖文件前提示
* -r 若给出的源文件是目录文件，

```shell
# 复制文件或目录
[xiaoyu@MYNET 桌面]$ cp ~/文档/read.txt ./read.txt
[xiaoyu@MYNET 桌面]$ cp ~/文档/read.txt .
```



###### 	4.4.2 mv（用来移动文件或目录，也可以给文件或目录重命名）

* -i 覆盖文件前提示

###### 	4.4.3 tree

* -d 只显示目录

##### 4.5 查看文件内容

###### 	4.5.1 cat（查看文件内容、创建文件、文件合并、追加文件内容）

* -b 对非空输出行编号
* -n 对输出的所有行编号

###### 	4.5.2 more（分屏显示文件内容）

###### 	4.5.3 grep（搜索文本文件内容）

* -n 显示匹配行及行号

* -v 显示不包含匹配文本的所有行（求反）

* -i 忽略大小写

  

  两种模式：

  * ^a 行首，搜寻以a开头的行
  * ke$ 行尾，搜寻以ke结束的行

##### 4.6 其他

###### 	4.6.1 echo

* 会在终端中显示参数指定的文字，通常会和重定向联合使用

###### 	4.6.2 重定向 **>** 和 **>>**

* Linux允许将命令执行结果重定向到一个文件
* 将本应显示在终端上的内容 输出/追加 到指定文件中

其中：

* **> ** 表示输出，会覆盖文件原有的内容
* **>>**  表示追加，会将内容追加到已有文件的末尾



###### 	4.6.3 管道 **|**

* Linux允许将**一个命令的输出**可以**通过管道**作为**另一个命令的输入**
* 可以理解现实生活中的管子，管子的一头塞东西进去，另一头取出来，这里 **|**  的左右分为两端，左端塞东西(写)，有段取东西(读)

常用的管道命令有：

* **more** :分屏显示内容
* **grep** :在命令执行结果的基础上查询指定的文本



#### 5.关机/重启

##### 5.1 shutdown

* **shutdown** 命令可以安全关闭或者重新启动系统

  ```shell
  shtdown -r	#重新启动
  ```

提示：

* 不指定选项和参数，默认表示1分钟之后关闭电脑

* 远程维护服务器时，最好不要关闭系统，而应该重新启动系统

* 常用命令：

  ```shell
  # 重新启动系统， now表示现在
  $ shutdown -r now
  
  # 立刻关机，其中now表示现在
  $ shutdown now
  
  # 系统在今天的20:25 会关机
  $ shutdown 20:25
  
  # 系统再过10分钟后自动关机
  $ shutdown +10
  
  # 取消之前指定的关机计划
  $ shutdown -c
  ```

#### 6. 查看或配置网卡信息

##### 6.1 ifconfig(configure a network interface)

作用：查看/配置计算机当前的网卡配置信息

```shell
# 查看网卡配置信息
$ ifconfig

# 查看网卡对应的ip地址
$ ifconfig | grep inet
```

* **127.0.0.1** 被称为 本地回环/环回地址，一般用来测试本机网卡是否正常

##### 6.2 ping ip地址(ping)

作用：检测到目标ip地址的连接是否正常

```shell
# 检测到目标主机是否连接正常
$ ping IP地址

# 检测本地网卡工作正常
$ ping 127.0.0.1
```

* 终止终端程序的执行，绝大多数可以用**ctrl+c**



#### 7.远程登录和复制文件

##### 7.1 ssh基础（重点）

在Linux中SSH是非常常用的工具，通过SSH客户端我们可以连接到运行了SSH服务器的远程机器上

* SSH客户端是一种使用 **Secure Shell(SSH)** 协议连接到远程计算机的软件程序
* SSH 使目前较可靠，专为远程登录会话和其他网络服务提供安全的协议
  * 利用 SSH协议 可以有效防止远程管理过程中的信息泄露
  * 通过 SSH协议 可以对所有传输的数据进行加密，也能够防止DNS欺骗和IP欺骗

**(1)域名和端口号**

**域名**

* 域名：类似 www.baidu.com
* 是IP地址的别名

**端口号**

* IP地址：通过IP地址找到网络上的计算机
* 端口号：通过端口号可以找到计算机上运行的应用程序
  * SSH服务器的默认端口号是22
* 常见服务端口号：
  * SSH服务器：22
  * Web服务器：80
  * HTTPS：443
  * FTP服务器：21



**（2）SSH客户端的简单实用**

```shell
ssh [-p port] user@remote
```

* **user** 是在远程机器上的用户名
* **remote** 是远程机器的地址
* **port** 是 SSH Server 监听的端口

使用 **exit** 退出当前用户的登录



##### 7.2 scp（掌握）

* scp 就是 cecure copy，是一个在Linux下用来进行 远程拷贝文件的命令
* 它的地址格式与SSH基本相同，需要注意的是，在指定端口时用的是大写的 **-P** 二不是小写的

```shell
# 把本地当前目录下的01.py文件 复制到远程 家目录下的 桌面/01.py
# 注意： ':'后面的路径如果不是绝对路径，则以用户名的家目录作为参照路径
$ scp -P port 01.py user@remote:桌面/01.py

# 把远程 家目录下的 桌面/01/py 文件 复制到 本地当前目录下的 01.py
$ scp -P port user@remote:桌面/01.py 01.py

# 加上 -r 选项可以传送文件
# 把当前目录下的demo 文件夹 复制到 远程 家目录下的桌面
$ scp -r demo user@remote:桌面

# 把远程 家目录下的 桌面 复制到 当前目录下的 demo 文件夹
$ scp -r user@remote:桌面 demo
```

##### 7.3 SSH高级（知道）

* 免密码登录
* 配置别名
* 有关SSH配置信息都保存在用户家目录下的.ssh目录下



**（1）免密码登录**

* 配置公钥
  * 执行 **ssh-keygen**  即可生成SSH钥匙，一路回车即可
* 上传公钥到服务器
  * 执行 **ssh-copy-id -p port user@remote**，可以让远程服务器记住我们的公钥



​	**（2）配置别名**

* 在 **~/.ssh/config** 里面追加内容：

* ```shell
  Host win
  	HostName ip地址
  	User yu
  	Port 22
  ```



#### 8.用户权限

##### 	8.1 chmod

* **chmod**  可以修改 用户/组 对 文件/目录 的权限

* 命令格式：

* ```shell
  chmod +/-rwx 文件名|目录名
  ```



##### 	8.2 组管理 终端命令

```shell
# 添加组
groupadd 组名
# 删除组
groupdel 组名
# 确认组信息
cat/etc/group
# 递归修改文件/目录的所属组
chgrp -R 组名 文件/目录名
```



##### 8.3 用户管理 终端命令

```shell
# 添加新用户
# -m 自动建立用户家目录
# -g 指定用户所在的组，否则会建立一个和同名的组
useradd -m -g 组 新建用户名
# 设置用户密码
passwd 用户名
# 删除用户
userdel -r 用户名
# 确认用户信息
cat /etc/passwd | grep 用户名
```



##### 8.4 查看用户信息

```shell
# 查看用户UID和GID信息
id [用户名]
# 查看当前所有登录的用户列表
who
# 查看当前登录用户的账户名
whoami
```



##### 8.5 usermod

```shell
# 修改用户的注销
usermod -g 组 用户名

# 修改用户的附加组
usermod -G 组 用户名

# 修改用户登录 Shell
usermod -s /bin/bash
```



##### 8.6 which

* /etc/passwd 用于保存用户信息的文件
* /usr/bin/passwd 用于修改用户密码的程序



```shell
which ls

# 输出
# /bin/ls

which useradd

# 输出
# /usr/sbin/useradd
```



* /bin 是二进制执行文件目录，主要用于具体应用
* /sbin是系统管理员专用的二进制代码存放目录，主要用于系统管理
* /usr/bin 后期安装的一些软件
* /usr/sbin 超级用户的一些管理程序



##### 8.7 切换用户

```shell
# 切换用户，并且切换目录
su -用户名	# -可以切换到用户家目录，否则保持位置不变
# 退出当前登录账户
exit
```



##### 8.8 修改文件权限

```shell
# 修改拥有者
chown 用户名 文件名|目录名

# 修改组
chgrp -R 组名 文件名|目录名

# 修改权限
chmod -R 755 文件名|目录名
```



#### 9.系统信息相关命令

##### 9.1 时间和日期

```shell
# 查看日历，-y选项可以查看一年的日历
cal

# 查看系统时间
date
```



##### 9.2  磁盘信息

```shell
# disk free 显示磁盘剩余空间
df -h

du -h --max-depth=1

# disk usage 显示目录下的文件大小
du -h[目录名]

# -h 以人性化的方式显示文件大小
```



##### 9.3 进程信息

* 进程，通俗地说就是 当前正在执行的一个程序

```shell
# process status 查看进程的详细状况
ps aux

# 动态显示运行中的进程并且排序
top

# 终止指定代号的进程，-9表示强行终止
kill [-9] 进程代号

# a 显示终端上的所有进程，包括其他用户的进程
# u 显示进程的详细状态
# x 显示没有控制终端的进程
```



#### 10.其他命令

##### 10.1 查找文件

```shell
# 查找指定路径下的扩展名是.py的文件，包括子目录
find [路径] -name "*.py"
```



##### 10.2 软链接

```shell
# 建立文件的软链接，类似于Windows下的快捷方式
ln -s 被链接的源文件 链接文件
```



##### 10.3 硬链接

* 在使用 ln 时，没有 -s 则会创建一个硬链接



##### 10.4 打包压缩

```shell
# 打包文件
tar -cvf 打包文件.tar 被打包的文件/路径...

# 解包文件
tar -xvf 打包文件.tar

# c 生成档案文件，创建打包文件
# x 解开档案文件
# v 列出归档解档的详细过程，显示进度
# f 指定档案文件名称，f后面一定是.tar文件，所以必须放选项最后
```



##### 10.5 压缩/解压缩

**（1）gzip**

```shell
# 压缩文件
tar -zcvf 打包文件.tar.gz 被压缩的文件/路径...

# 解压缩文件
tar -zxvf 打包文件.tar.gz

# 解压缩到指定路径
tar -zxvf 打包文件.tar.gz -C 目录路径

# -C 解压缩到指定目录
```



**（2）bzip2(two)**

```shell
# 压缩文件
tar -jcvf 打包文件.tar.bz2 被压缩的文件/路径..

# 解压缩文件
tar -jxvg 打包文件.tar.bz2
```



#### 11.软件安装

##### 11.1 用过apt安装/卸载软件

```shell
# 安装软件
$ sudo apt install 软件包

# 卸载软件
$ sudo apt remove 软件名

# 更新已安装的包
$ sudo apt upgrade
```



#### 12.编译

```shell
# 编译生成makefile文件
make

# 清除之前失败编译的结果
make clean

# 编译出错时，清出编译生成的文件
make distclean
```



#### 13.更换yum源

```shell
# 先备份centos-base.repo
sudo cp /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak

# 然后编辑文件
vi /etc/yum.repos.d/CentOS-Base.repo 

# 在 mirrorlist= 开头行前面加 # 注释掉
# 并将 baseurl= 开头行取消注释
# 把该行内的域名替换
# 最后，更新软件包缓存
sudo yum makecache
```



#### 14.安装chrome浏览器

```shell
$ yum install https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
```



#### 15.临时升级gcc

```shell
# 查看gcc版本是否在5.3以上，centos7.6默认安装4.8.5
gcc -v
# 升级gcc到5.3及以上,如下：
升级到gcc 9.3：
yum -y install centos-release-scl
yum -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils
scl enable devtoolset-9 bash
```



#### 16.Redis

##### 1.启动Redis服务

```shell
[root@mynet bin]# redis-server kconfig/redis.conf

# 连接测试
[root@mynet bin]# redis-cli -p 6379
127.0.0.1:6379> ping
PONG

# 关闭Redis服务
127.0.0.1:6379> shutdown
not connected> exit
```



