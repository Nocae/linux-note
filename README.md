# Linux

## 各种设备在linux的文件名

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190226160828364.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdV9zaXNp,size_16,color_FFFFFF,t_70)



>在上图中的[a-p]表示从a字母到p字母的罗列例如，/dev/sda /dev/sdb ..... /dev/sdp
>
>注意以后会有很多[]



## Linux安装与设置

#### GPT分区表和MBR分区表的区别

http://www.360doc.com/content/18/0614/22/6140124_762487520.shtml

#### 挂载的含义

>将真实的存储设备与对应的文件进行绑定即为挂载，所在的目录即为挂载点

### 安装模式与启动

>如果磁盘容量小于2TB的话，系统默认会使用MBR分区表来安装

#### 初次安装建议

- 建议一,只划分"/"以及"交换分区"
- 建议二,预留一个备份的剩余磁盘容量
- 建议三,选择Linux安装程序提供的默认硬盘分区方式
- 建议四,使用usb3.0时可能会将该设备识别为硬盘,设置启动项时一定要注意.
- 建议五,如果硬盘大小小于2TB默认采用MBR分区
- 建议六,如果没有采用MBR而是采用GPT则需要创建bios boot分区
- 如果不想安装下载文件可以选择LiveCD等Live系列
- 如果想练习可使用最小安装版本(minimal)来安装



#### 关于centos名称解读:

centos-7-x86_64-Everything-1503-01.iso

- 7表示大版本
- x86_64代表64位操作系统
- Everything代表全功能版本
- 1503代表是2015年3月发布
- 01代表属于centos7.1

### 磁盘分区

- **标准分区**：类似/dev/vda1
- **LVM**：一种可以弹性增加或缩小文件系统容量的分区
- **LVM精简配置**：相当于LVM的高级版

#### 文件系统选项

- **ext2/ext3/ext4**：Linux早期使用的文件系统,ext3/ext4文件系统多了日志功能，对于系统的恢复比较快速。不常用了，嘤嘤嘤！
- **swap**：磁盘模拟为内存的交换分区,不会挂载到树目录,交换分区不需要指定挂载点
- **BIOS Boot**：GPT分区表可能会用到的东西若使用MBR就用不到了
- **xfs**：centos7默认的文件系统，对于大容量磁盘管理很好,格式化很快
- **vfat**：同时支持Windows和Linux系统，可以进行数据交换



> 安装系统后所有的root密码等都会记录到/root/anaconda-ks.cfg中;



## 命令部分

### 切换X Windows 与 命令行模式

>Ctrl + Alt + F1 **切换到X Windows窗口**
>Ctrl + Alt + F2~F6 **切换到tty2~tty6命令行模式**

***如果安装centos7时默认的是命令行界面，那么tty1~tty6会被命令行界面占用***

**centos7环境下，启动完成默认提供一个tty，需要切换时才产生额外的tty**

### 一般的命令格式：

```
    command [-options] parameter1 parameter2
```

- command 一般是命令或者可执行文件
- 如果命令符太长了可以使用\（反斜杠，嘤嘤嘤）来连接
- Linux中，***英文大小写字母是不一样的***

### 如果输入命令乱码

可能时Linux检测为中文编码修改为英文即可

> [root@YH ~]# local
> -bash: local: can only be used in a function
> [root@YH ~]# locale
> LANG=en_US.utf8
> LC_CTYPE="en_US.utf8"
> LC_NUMERIC="en_US.utf8"
> LC_TIME="en_US.utf8"
> LC_COLLATE="en_US.utf8"
> LC_MONETARY="en_US.utf8"
> LC_MESSAGES="en_US.utf8"
> LC_PAPER="en_US.utf8"
> LC_NAME="en_US.utf8"
> LC_ADDRESS="en_US.utf8"
> LC_TELEPHONE="en_US.utf8"
> LC_MEASUREMENT="en_US.utf8"
> LC_IDENTIFICATION="en_US.utf8"
> LC_ALL=
>
> 修改为英文
>
> [root@YH ~]# LANG=en_US.utf8
> [root@YH ~]# export LC_ALL=en_US.utf8



### linux基础命令系列

- date:显示时间日期
- cal:显示日历
- bc:简单的计算器

### 切换root账户

```
    su -
```

### 格式化输出日期

```
    date +%Y/%m/%d
```

### 格式化输出时间

```
    date +%H:%M
```

### 日历命令

```
    cal [month] [year]
```

### 热键的使用

**[Tab]**

- [Tab]接在一串命令的第一个字段后面则为【命令补全】
- [Tab]接在一串命令的第二个字段后面则为【文件补全】

**[Ctrl+D]**

通常代表键盘输入结束，或者替代**exit**命令

[shift+{page up}/{page dwon}]

翻页，命令过长屏幕翻页

### 如何用了解命令的使用

使用--help可以查看基本用法使用 man 加命令可以看到更详细的用法

例如输入man date后

```bash
DATE(1)                                             User Commands                                             DATE(1)

NAME
       date - print or set the system date and time

SYNOPSIS
       date [OPTION]... [+FORMAT]
       date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]

DESCRIPTION
       Display the current time in the given FORMAT, or set the system date.

       Mandatory arguments to long options are mandatory for short options too.

       -d, --date=STRING
              display time described by STRING, not 'now'

       -f, --file=DATEFILE
              like --date once for each line of DATEFILE

       -I[TIMESPEC], --iso-8601[=TIMESPEC]
              output  date/time in ISO 8601 format.  TIMESPEC='date' for date only (the default), 'hours', 'minutes',
              'seconds', or 'ns' for date and time to the indicated precision.

       -r, --reference=FILE
.....
```

这里可以看到有一个DATE(1)这个意思是一般用户可以使用的命令还有更多的数字解析如(从man man命令查看)

>       	 	 1   Executable programs or shell commands
>       	    2   System calls (functions provided by the kernel)
>       	    3   Library calls (functions within program libraries)
>       	    4   Special files (usually found in /dev)
>       	    5   File formats and conventions eg /etc/passwd
>       	    6   Games
>       	    7   Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7)
>       	    8   System administration commands (usually only for root)
>       	    9   Kernel routines [Non standard]

1(用户可以在shell中可以操作的命令或者可执行文件)、5(配置文件或是某些文件的格式)、8(系统管理员可用的管理命令)

上面这三个含义很重要



```bash
CAT(1)                                              User Commands                                              CAT(1)

NAME
       cat - concatenate files and print on the standard output

SYNOPSIS
       cat [OPTION]... [FILE]...

DESCRIPTION
       Concatenate FILE(s), or standard input, to standard output.

       -A, --show-all
              equivalent to -vET

       -b, --number-nonblank
              number nonempty output lines, overrides -n

       -e     equivalent to -vE

       -E, --show-ends
              display $ at end of each line

       -n, --number
              number all output lines

       -s, --squeeze-blank
              suppress repeated empty output lines

       -t     equivalent to -vT

       -T, --show-tabs
              display TAB characters as ^I

       -u     (ignored)

       -v, --show-nonprinting
              use ^ and M- notation, except for LFD and TAB

       --help display this help and exit

       --version
              output version information and exit

       With no FILE, or when FILE is -, read standard input.

EXAMPLES
       cat f - g
              Output f's contents, then standard input, then g's contents.

       cat    Copy standard input to standard output.

       GNU   coreutils   online   help:  <http://www.gnu.org/software/coreutils/>  Report  cat  translation  bugs  to
       <http://translationproject.org/team/>

AUTHOR
       Written by Torbjorn Granlund and Richard M. Stallman.

COPYRIGHT
       Copyright  ©  2013  Free  Software  Foundation,  Inc.   License  GPLv3+:  GNU   GPL   version   3   or   later
       <http://gnu.org/licenses/gpl.html>.
       This  is  free software: you are free to change and redistribute it.  There is NO WARRANTY, to the extent per‐
       mitted by law.

SEE ALSO
       tac(1)

       The full documentation for cat is maintained as a Texinfo manual.  If the info and cat programs  are  properly
       installed at your site, the command

              info coreutils 'cat invocation'

       should give you access to the complete manual.

GNU coreutils 8.22                                  November 2020                                              CAT(1)

```

再一次解析man page每一个区域有着不同的含义

- NAME 简短的命令数据说明
- SYNOPSIS 简短的命令语法简介
- DESCRIPTION 较为完整的说法,建议仔细看
- OPTIONS 可选项说明
- COMMANDS 当这个程序在执行的时候,可以在此程序中执行的命令
- FILES 这个程序或数据所使用或参考或连接到的某些文件
- SEE ALSO 可以参照跟这个命令或数据有相关的其他说明
- EXAMPLE 可以参考的实例

> 使用info也可以查看



> /usr/share下面基本都是帮助文档安装的软件基本的帮助都是在这个文档中



### 有关另一个文档编辑器

nano

使用命令后的page

> GNU nano 2.3.1                             File: 1.txt 
>
> 
>
> ^G Get Help         ^O WriteOut         ^R Read File        ^Y Prev Page        ^K Cut Text         ^C Cur Pos
> ^X Exit             ^J Justify          ^W Where Is         ^V Next Page        ^U UnCut Text       ^T To Spell

第一行,为版本号和文件名

下面几行为基本操作^代表ctrl



configure命令

configure文件是bai一个可执行的脚本文件，它有很多选du项，在待安装的zhi源码目录下使用命令./configure –help可以输出dao详细的选项列表。

其中--prefix选项是配置安装目录，如果不配置该选项，安装后可执行文件默认放在/usr /local/bin，库文件默认放在/usr/local/lib，配置文件默认放在/usr/local/etc，其它的资源文件放在/usr /local/share，比较凌乱。

如果配置了--prefix，如：

$ ./configure --prefix=/usr/local/test1



scp上传文件

### 正确的关机方法

**who**：查看目前有谁在线

**netstat -a**：查看网络的联机状态

**ps -aux**：查看后台执行的程序

**sync**：将数据同步写入硬盘

**shutdown**：常用的关机命令

**reboot、halt、poweroff**：重新启动、关机


#### shutdown

```
    shutdown [-krhc] [时间] [警告信息]
```

- -k：不要真的关机，只是发送警告信息出去
- -r：在将系统的服务停掉之后就重新启动（常用）
- -h：将系统的服务停掉以后，立即关机（常用）
- -c：取消已经在进行的shutdown命令内容
- 时间：指定系统关机时间，若没指定，默认一分钟自动进行



## 文件权限与目录配置

### 用户与组

所有用户的相关信息都放在/etc/passwd

个人的密码保存在/etc/shadow文件夹中

所有的组名都记录在/etc/group中

***这三个文件夹不可随便删除***

不解释了不明白自己百度



### 基本命令统计

- ls	:显示文件名以及属性 -al所有、-l --full-time显示所有完整的时间格式 -S排序

- chgrp :修改文件所属用户组 -R递归进行修改联通子目录下的所有文件
- chown :修改文件所属用户 -R同上、也可以修改用户组
  - chown 用户名 文件名(修改所属用户)
  - chown 用户名:组名 文件名(修改所属用户和组)
- chmod :修改文件权限
  - 三种修改模式 +(增加权限) -(删除权限) =(设置权限为)
  - 太长了看这个吧..https://www.runoob.com/linux/linux-comm-chmod.html
- cp    :复制文件



#### 文件属性详解

> drwxr-xr-x   2 root root  4096 Aug 14 17:34 .pip

例如上面的参数(用ls -al查出来的)



==第一个属性==

##### 文件权限

第一个字符表示目录、文件、连接

- 当为[d]时为目录
- 当为[-]则是文件
- 当为[|]则是连接
- 当为[b]表示为设备文件里面的可供存储的周边设备
- 若是[c]则表示属于设备文件属于串行端口设备,如键盘鼠标

接下来每三个字符一组分别又rwx组成,r代表可读,w代表可写,x代表可执行[-]代表没有权限(如果为目录的话没有x不能进入,w权限并不能代表可以删除文件)



权限对文件来说	

r代表是否可以获取文件中的内容。

w代表是否能修改、写入、新增、编辑。

x代表该文件是否可执行，不像Windows一样用后缀名来代表文件是否可执行



权限对目录来说	

r代表你可以查询该目录下内容(可以使用ls来查看)。

w建立新的文件或目录、删除已存在目录与文件、对文件或者目录进行改名、移动该目录内的文件、目录位置。

x代表是否能进入该目录了



第一组代表文件拥有者可具备的权限,第二组为所属组所具备的权限,第三组为其他人的权限

----

##### 文件默认权限

当你建立一个新的文件或者文件夹的时候默认权限是什么?

用umask可以指定目前用户在建立文件或目录时候给的权限

umask 设置默认减掉的权限例如umask 777则变成新建文件什么权限不给 umask 000 则给予最高权限

-p以数字形式显示权限设置情况

-S以字符串方式显示



### 文件隐藏属性

- chattr 修改文件隐藏配置--- 增加隐藏属性,-a 只能增加数据不能删除不能修改数据只有root才能设置属性 -i 不能删除、改名、设置连接、修改数据或新增数据只有root 才能修改属性
- lsattr [-adR] 目录或文件 显示文件隐藏配置 ----  -a基本属性也显示 -d如果时目录进显示出本身属性而不是目录内的文件名 -R连通子目录一起显示



第二个属性是有多少文件名连接到此节点.

第三个属性是文件或者目录拥有者.

第四个属性是文件的所属组.

第五个属性是文件大小

第六个属性是文件创建日期或是修改日期(月/日,不是今年显示年)



### 文件类型以及扩展名

自己看吧~~~额https://www.cnblogs.com/peida/archive/2012/11/22/2781912.html



## 文件与目录管理

特殊目录

>.	 代表此目录
>
>..	代表上层目录
>
>\-     代表前一个目录
>
>~	 代表当前身份的家
>
>~lll  代表这个身份的家



### 目录处理命令

- cd:切换
- pwd:显示当前目录 -P可以知道目录的真实路径
- mkdir:建立一个新目录 -p可以一次建立多级目录
- rmdir:删除一个空目录
- cp:复制 
  - -d若源文件为链接文件属性,则复制链接文件而不是文件本身 
  - -f若文件存在且无法开启则删除后再试
  - -a 相当于-dr --preserve=all大概是全复制(权限时间什么的都复制)
  - -i 若文件存在则覆盖时会询问
  - -p 连同属性一起复制过去
  - -r 递归复制
  - -l硬链接
  - -s软链接
  - -u目标与源文件有差异才复制j

- basename:获取字符串的文件名
- dirname:获取字符串的路径名



### 文件内容查看

- tac:从最后一行显示
- nl:同时输出行号
- more:一页一页显示 (空格下一页,enter下一行,:f立即显示行数,q:立即离开,b往前翻)
- less:与more相同就但是是从后面显示
- head:只看前几行
- tail:只看后几行
- od:以二进制方式读取内容
- cat:从第一行开始显示 -n打印行号包含空白页 -A 显示特殊字符

### 修改文件内容与新建

- 修改时间:当内容改变而不是权限或属性改变时才会改变的时间
- 状态时间:当文件状态改变,例如属性或权限改变时才会改变的时间
- 读取时间:当文件的内容被读取时就会改变
- 使用touch可以修改文件时间



### 查看文件类型

file+文件



### 文件查找

- which 查找执行文件 根据path环境变量所规范的路径去查找 -a显示所有而不是第一个,-i 显示所有查找的路径,主要针对bin/sbin下面的文件以及/usr/share/man下面的man page文件 
- 使用locate来查找,寻找的数据是由与建立的数据库/var/lib/mlocate里面的数据,这个数据库是日更,直接输入updatedb系统会自动去读取/etc/updatedn.conf这个文件的设置并更新数据库里面的数据
- find [PATH] [option] [action]
  - -mtime n
    - 例如今天为2011-05-05
    - n如果前面没有符号则为在第前当n天修改的文件 -mtime 3 则查看2011-05-02
    - -n列出在n天之内的被修改的文件 -mtime -3 则查看2011-05-03---2011-05-05
    - +n 列出在n天前被修改的内容 -ntime +3 则查看-----到2011-05-01
  - -uid n 根据用户的ID(/etc/passwd)查找
  - -giu n 根据组名id(/etc/group)进行查找
  - -user name :name为使用者名字
  - -group name: name为组名
  - -nouser :查找文件拥有者不在(/etc/passwd)
  - -nogroup :查找拥有用户组不在(/etc/group)内的文件
    - 上面两个命令可以用在查找已删除用户或者组但是没删除的文件
  - -name filename:查找文件名为filename的文件
  - -size [+-]SIZE:若用+则查找比SIZE大的,若用-则查找比SIZE小的
  - -type :根据类型查找
  - -perm :根据权限查找
  - -exec :进行额外操作,就是将查找的结果移交到后面的



### 关于执行文件路径变量$PATH

ｅｃｈｏ＄PATH可以输出

将路径加入PATH中的命令





## 进程管理

#### PS命令

查看当前系统正在执行的进程信息

- a  显示所有进程
- -a 显示同一终端下的所有程序
- -A 显示所有进程
- c  显示进程的真实名称
- -N 反向选择
- -e 等于“-A”
- e  显示环境变量
- f  显示程序间的关系
- -H 显示树状结构
- r  显示当前终端的进程
- T  显示当前终端的所有程序
- u  指定用户的所有进程
- -au 显示较详细的资讯
- -aux 显示所有包含其他使用者的行程 
- -C<命令> 列出指定命令的状况
- --lines<行数> 每页显示的行数
- --width<字符数> 每页显示的字符数
- --help 显示帮助信息
- --version 显示版本显示

>| 在Linux中这个叫管道符号 比如A|B将A命令运行的结果送给B
>
>grep 查找文件中符合条件的字符串

ps -aux|grep mysql这个命令就可以查看所有有关mysql的进程

ps -ef可以看父进程（一般不这么用看父目录可以使用pstree）

>详细请看这个网站
>
>https://www.cnblogs.com/xiangtingshen/p/10920236.html

#### kill命令

命令参数

- -9 杀死一个进程
- -1 重启一个进程
- -15 正常停止一个进程
- -l <信息编号> 　若不加<信息编号>选项，则 -l 参数会列出全部的信息名称

例如

强制杀死进程

```bash
kill -9 123456
```



杀死指定用户所有进程

```bash
kill -9 $(ps -ef | grep hnlinux) //方法一 过滤出hnlinux用户进程 kill -u hnlinux //方法二
```



>https://www.runoob.com/linux/linux-comm-kill.html





#### pstree命令

Linux pstree命令将所有行程以树状图显示，树状图将会以 pid (如果有指定) 或是以 init 这个基本行程为根 (root)，如果有指定使用者 id，则树状图会只显示该使用者所拥有的行程。

> https://www.runoob.com/linux/linux-comm-pstree.html



## 安装jdk

https://blog.csdn.net/pdsu161530247/article/details/81582980

source让配置文件生效

### 防火墙

firewall-cmd --list-ports查看开启



## 文件夹以及配置文件作用-----目录配置依据FHS

|      | 可分享                  | 不可分享(与主机有关不适合分享) |
| ---- | ----------------------- | ------------------------------ |
| 不变 | /usr(存放软件)          | /etc(配置文件)                 |
|      | /opt(第三方辅助软件)    | /boot(启动与内核文件)          |
| 可变 | /var/mail(用户邮箱)     | /var/run(程序相关)             |
|      | /var/spool/news(新闻组) | /var/lock(程序相关)            |

根目录下文件的作用https://www.cnblogs.com/jszd/p/11182190.html

- /bin:(普通用户和管理员常用命令)
- /boot:(主要放置启动会用到的文件)
- /dev:(任何设备与接口都是以文件形式存放在这个目录)
- /usr:(存放软件)
  - /share:存放命令帮助文档和者软件帮助文档
  - /games:与游戏相关的
  - /include:c++等程序语言的头文件与包含文件放置处
  - /libexec:某些不被一般用户常用的执行文件或脚本
  - /src:一般源码放在这里
- /etc:(系统配置文件几乎都在这个目录但只有root有权利修改,==建议不要将可执行文件放在该目录里面==)
  - /passwd:存放各个用户的信息
  - /shadow:存放个人密码
  - /group:所有组个名在这里面
  - /locale.conf:可以修改系统语言
  - /opt:这个目录在防止第三方辅助软件/opt的相关配置文件
  - /sysconfig
    - /network-scripts:网络配置目录
- /var
  - /cache:应用程序本身运行过程中产生的一些缓存
  - /lock(程序相关)
  - /run(程序相关)
  - /mail(用户邮箱)
  - /spool
    - /news(新闻组)
  - /log
    - /wtmp这个文件用来存放登录数据
- /run或/tmp数据接口文件常用来通过soocket来进行数据沟通
- /lib:(放置的是启动时会用到的库函数,以及在/bin和/sbin下面的命令会调用的库函数)
  - /modules:放置驱动程序
- /opt:(给第三方辅助软件防止的目录也有可能有人习惯安装在/usr/local下)
- /sbin:(很多命令是用来设置系统环境的,这些命令只有root才能设置系统里面包含了修复启动还原系统所需要的命令)
  - 某些服务器软件程序放置在/usr/sbin中.本机自行安装的软件所产生中的系统执行文件,则放置到/usr/local/sbin
- /srv:(网络服务器运行后所需要使用的数据目录)
- /home:(普通用户的家,~回到这个目录下的指定文件)
- /root:(root用户的家)
- /proc:(系统的信息例如内核、进程信息、外接设备、网络状况，他防止的数据都在内存中)
- /sys:不占硬盘容量也是保存系统信息的