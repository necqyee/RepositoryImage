# 代码

```
date 时间
alias 别名

vi /etc/motd 设置开机欢迎
cat /etc/os-release 查看系统版本
```

# Linux系统命令基础

## Linux系统文件与启动流程

```
/etc初始化系统重要文件
    /etc/sysconfig/network-scripts/ifcfg-eth0:网卡配置文件
    /etc/resolv.conf:Linux系统DNS客户端配置文件
    /etc/hostname (CentOS7) /etc/sysconfig/network:(CentOS 6)主机名配置文件
    /etc/hosts:系统本地的DNS解析文件
    /etc/fstab:配置开机设备自动挂载的文件
    /etc/rc.local:存放开机自启动程序命令的文件
    /etc/inittab:系统启动设定运行级别等配置的文件
    /etc/profile及/etc/bashrc:配置系统的环境变量/别名等的文件
    /etc/profile.d:用户登录后执行的脚本所在的目录
    /etc/issue和/etc/issue.net:配置在用户登录终端前显示信息的文件
    /etc/init.d:软件启动程序所在的目录(centos 6)
    /usr/lib/systemd/system/ 软件启动程序所在的目录(centos 7)
    /etc/motd:配置用户登录系统之后显示提示内容的文件
    /etc/redhat-release:声明RedHat版本号和名称信息的文件
    /etc/sysctl.conf:Linux内核参数设置文件
    
/proc重要路径
	/proc/meminfo:系统内存信息
	/proc/cpuinfo:关于处理器的信息，如类型，厂家，型号，性能等
	/proc/loadavg:系统负载信息，uptime 的结果
	/proc/mounts:已加载的文件系统的列表
	
/var目录下文件
    /var/log:记录系统及软件运行信息文件所在的目录
    /var/log/messages:系统级别日志文件
    /var/log/secure:用户登录信息日志文件
    /var/log/dmesg:记录硬件信息加载情况的日志文件
```



## Linux目录详解

<img src="https://necqyee.oss-cn-guangzhou.aliyuncs.com/image/251.png" alt="img" style="zoom:50%;" />

```
/bin：bin是Binary的缩写, 这个目录存放着最经常使用的命令。

/boot：这里存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件。

/dev ：dev是Device(设备)的缩写, 该目录下存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的。

/etc：这个目录用来存放所有的系统管理所需要的配置文件和子目录。

/home：用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

/lib：这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库。

/lost+found：这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。

/media：linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下。

/mnt：系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。

/opt： 这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

/proc：这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。 这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器：

echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all

/root：该目录为系统管理员，也称作超级权限者的用户主目录。

/sbin：s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。

/selinux： 这个目录是Redhat/CentOS所特有的目录，Selinux是一个安全机制，类似于windows的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的。

/srv： 该目录存放一些服务启动之后需要提取的数据。

/sys：这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs 。

sysfs文件系统集成了下面3种文件系统的信息：针对进程信息的proc文件系统、针对设备的devfs文件系统以及针对伪终端的devpts文件系统。该文件系统是内核设备树的一个直观反映。当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。

/tmp：这个目录是用来存放一些临时文件的。

/usr：这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于windows下的program files目录。

/usr/bin：系统用户使用的应用程序。

/usr/sbin：超级用户使用的比较高级的管理程序和系统守护程序。

/usr/src：内核源代码默认的放置目录。

/var：这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。

在linux系统中，有几个目录是比较重要的，平时需要注意不要误删除或者随意更改内部文件。

/etc： 上边也提到了，这个是系统中的配置文件，如果你更改了该目录下的某个文件可能会导致系统不能启动。

/bin, /sbin, /usr/bin, /usr/sbin: 这是系统预设的执行文件的放置目录，比如 ls 就是在/bin/ls 目录下的。

值得提出的是，/bin, /usr/bin 是给系统用户使用的指令（除root外的通用户），而/sbin, /usr/sbin 则是给root使用的指令。

/var： 这是一个非常重要的目录，系统上跑了很多程序，那么每个程序都会有相应的日志产生，而这些日志就被记录到这个目录下，具体在/var/log 目录下，另外mail的预设放置也是在这里。
```



## Linux文件及目录管理命令

|   **命令**   |     **对应英文**     |        **作用**        |
| :----------: | :------------------: | :--------------------: |
|      ls      |         list         |     查看文件夹内容     |
|     pwd      | print work directory |    查看当前所在目录    |
|  cd 目录名   |   Change directory   |       切换文件夹       |
| touch 文件名 |        touch         | 如果文件不存在，则创建 |
| mkdir 目录名 |    Make directory    |        创建目录        |
|  rm 文件名   |        Remove        |      删除指定文件      |

### cd命令

```
.    当前目录
..   上一层目录
-    前一个工作目录
~    当前【用户】所在的家目录
/    顶级根目录
```

### ls命令

显示目录下内容及属性信息的命令

```
-a 显示指定目录下所有子目录与文件，包括以.开头的隐藏文件
-l 以列表方式显示文件的详细信息   ls -l 等于ll 用法
-h, --human-readable     与-l 一起，输出文件大小 (例如 1K 234M 2G)
-t 根据最后修改时间排序，默认是以文件名排序，通常与-l 连用
-F 在条目后加上文件类型的指示符号(* ， /， = ， @ ， | ，其中的一个)
    注:可以标识文件类型
    加上 * 代表可执行的普通文件
    加上 = 表示套接字
    加上 | 表示FIFOS(队列系统)
    加上 @表示符号链接
    加上 / 表示文件夹
-d 显示目录本身的信息 而不是显示目录的内容
-r, --reverse                 逆序排列
-S                            根据文件大小排序,从大到小排序
-i 显示索引节点信息(索引节点相当于身份证号，存储了文件元信息，大小，位置，权限)
--full-time 以完整的时间格式输出(也就是按照中国的时间日期显示)
```

案例

```
ls -lt      按照时间进行排序
ls -lrt     找出最新的文件
ls -d */    列出当前所有目录
ll -hS    ./*    显示出当前目录下所有内容详细，且以kb,mb,gb单位从大到小排序
```

### pwd命令

```
输出当前所处的一个绝对路径
```

### su命令

```
su命令切换
语法
su - 用户名 # 完全的环境变量用户切换
```

### logout命令

```
退出当前系统用户
```

### *mkdir命令*

```
创建文件夹
用法：mkdir [选项]... 目录...
若指定目录不存在则创建目录。

-m, --mode=模式       设置权限模式(类似chmod)，而不是rwxrwxrwx 减umask
-p, --parents         递归创建文件夹，且绝对路径
mkdir {1..3}加花括号创建连续的目录，用..隔开 花括号内可以是连续的数字、连续的字母mkdir {a..e}
```

案例

```
mkdir -p /opt/alex/chaoge/xx/ll
mkdir chaoge{1..100} #mkdir chaoge1 mkdir chaoge2 ... mkdir chaoge100 
```

### *touch命令*

```
用法：touch [选项]... 文件...
将每个文件的访问时间和修改时间改为当前时间。

touch有两个作用
1.创建普通文件，在Linux下文件的后缀格式仅仅是一个名字而已，通过touch创建的都是普通文件
2.修改文件时间

不存在的文件将会被创建为空文件，除非使用-c 或-h 选项。

touch {连续数字或字母} 创建多个文件序列
touch {1..10}
touch {a..z}

  -c, --no-create       不创建任何文件
  -t STAMP              使用[[CC]YY]MMDDhhmm[.ss] 格式的时间替代当前时间
  touch -t 10240606 mjj.exe #10月24日06:06
  -r, --reference=文件  使用指定文件的时间属性替代当前文件时间
```

### *cp复制*

```
用法：cp [选项]... [-T] 源文件 目标文件
　或：cp [选项]... 源文件... 目录
　或：cp [选项]... -t 目录 源文件...
将源文件复制至目标文件，或将多个源文件复制至目标目录。

-r 递归式复制目录，即复制目录下的所有层级的子目录及文件 -p 复制的时候 保持属性不变
-d 复制的时候保持软连接不变(快捷方式)
	#cp -d link_luffy link_luffy2
-a 等于-pdr
-p                等于--preserve=模式,所有权,时间戳，复制文件时保持源文件的权限、时间属性
-i, --interactive        覆盖前询问提示
	#cp 就是 cp -i
```

案例

```
案例1

复制 > copy > cp
#移动xxx.py到/tmp目录下
cp xxx.py /tmp/
#移动xxx.py顺便改名为chaoge.py
cp xxx.py /tmp/chaoge.py

Linux下面很多命令，一般没有办法直接处理文件夹,因此需要加上（参数） 
cp -r 递归,复制目录以及目录的子孙后代
cp -p 复制文件，同时保持文件属性不变    可以用stat
cp -a 相当于-pdr

#递归复制test文件夹，为test2
cp -r test test2

cp是个好命令，操作文件前，先备份
cp main.py main.py.bak

移动多个文件，放入文件夹c中
cp -r  文件1  文件2  文件夹a   文件夹c

[root@pylinux opt]# cp luffy_boy.zip  luffy_boy.zip.bak2
cp：是否覆盖"luffy_boy.zip.bak2"？ y

[root@pylinux opt]# cp luffy_boy.zip  luffy_boy.zip.bak2 -i
cp：是否覆盖"luffy_boy.zip.bak2"？ y

cp确认是否覆盖是-i参数作用，默认alias因为添加了别名
[root@pylinux opt]# alias
alias cp='cp -i'

案例2

[root@pylinux opt]# cp luffyCity/ luffyCity2    #必须添加-r参数才可以复制递归目录
cp: omitting directory 'luffyCity/'
[root@pylinux opt]#
[root@pylinux opt]#
[root@pylinux opt]#
[root@pylinux opt]# cp -r luffyCity/ luffyCity2
[root@pylinux opt]#
[root@pylinux opt]#
[root@pylinux opt]# ls
luffyCity  luffyCity2
```

取消cp别名的方式

- 使用命令绝对路径
- 命令开头用反斜线 \
- 取消cp命令别名
- 写入环境变量配置文件

```
1.
[root@pylinux opt]# which cp
alias cp='cp -i'
    /usr/bin/cp
[root@pylinux opt]# /usr/bin/cp luffy_boy.zip luffy_boy.zip.bak

2.
[root@pylinux opt]# \cp luffy_boy.zip luffy_boy.zip.bak

3.
[root@pylinux opt]# unalias cp
[root@pylinux opt]#
[root@pylinux opt]# cp luffy_boy.zip luffy_boy.zip.bak

4.
[root@pylinux opt]# vim ~/.bashrc  #可以注释掉如下配置
# .bashrc

# User specific aliases and functions

alias rm='rm -i'
#alias cp='cp -i'
alias mv='mv -i'
```

快速备份配置文件

![img](https://necqyee.oss-cn-guangzhou.aliyuncs.com/image/261.jpg)







## 绝对路径与相对路径

Linux下特别注意文件名/路径的写法，可以将所谓的路径(path)定义为绝对路径(absolute)和相对路径(relative)。这两种文件名/路径的写法依据是这样的：

- 绝对路径：由根目录(/)为开始写起的文件名或者目录名称，如/home/oldboy/test.py;

- 相对路径：相对于目前路径的文件名写法。例如./home/oldboy/exam.py或../../home/oldboy/exam.py，简单来说只要开头不是/，就是属于相对路径

因此你必须了解，相对路径是：以你当前所在路径的相对路径来表示的。

例如你现在在/home 这个目录下，如要进入/var/log这个路径，如何写呢？

1. cd /var/log (绝对路径)
2. cd ../var/log(相对路径)

结果如图：

因为你在/home底下，因此你要回到上一层(../)之后，才能继续前往/var，特别注意：

- . :代表当前的目录，也可以用./ 来表示
- .. :代表上一层的目录，也可以用../来表示

![img](https://necqyee.oss-cn-guangzhou.aliyuncs.com/image/280.png)

















