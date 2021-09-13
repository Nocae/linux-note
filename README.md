<<<<<<< HEAD


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
>
>文件系统与目录树结合的操作我们称为[挂载]

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

#### chmod修改权限，数字类型修改文件权限

```linux
       chmod [-R] xyz 文件或目录

       xyz：数字类型的权限属性，为rwx属性数值的相加
       -R：进行递归修改，连同子目录下的所有文件都会修改
```

#### chmod修改权限，符号类型修改文件权限

![](https://www.runoob.com/wp-content/uploads/2014/08/rwx-standard-unix-permission-bits.png)


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

w代表是否能**修改、写入、新增、编辑(不包括删除该文件)**。

x代表该文件是否可执行，不像Windows一样用后缀名来代表文件是否可执行



权限对目录来说	

r代表你可以查询该目录下内容(可以使用ls来查看)。

w建立新的文件或目录、删除已存在目录与文件（不论该文件的权限是什么）、对文件或者目录进行改名、移动该目录内的文件、目录位置。

x代表**是否能进入该目录**



第一组代表文件拥有者（owner）可具备的权限,第二组为所属组（group）所具备的权限,第三组为其他人（others）的权限

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
>~acc  代表这个身份的家(acc表示用户名)

### 文件与目录的查看：ls

- -a:全部的文件，连同隐藏文件（开头为.文件）一起列出来（常用）
- -A:全部的文件，连同隐藏的文件，但不包括.与..这两个目录
- -d:仅列出目录本身，而不是列出目录内的文件数据（常用）
- -f:直接列出结果，而不进行排序（ls默认会以文件名排序）
- -F:根据文件、目录等信息，给予附加数据结构
  - *:代表可执行文件；/:代表目录；=:代表socket文件；|:代表FIFO文件
  -l:详细信息显示，包含文件的属性与权限等数据（常用）


### 目录处理命令

- cd:切换
- pwd:显示当前目录 **-P可以知道目录的真实路径**
- mkdir:建立一个新目录 **-p可以一次建立多级目录，-m设置文件的权限，不使用默认权限**
- rmdir:**删除一个空目录**，-p连同上层“空”目录也一起删除
- rm -r xx 删除目录包括目录下的文件
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

将路径加入PATH中的命令 = ${PATH}:A

A为你要添加的路径



## Linux磁盘与文件管理系统

ext2（Linux second Extended file system）

由于ext2是属于索引表加数据的一种形式所以几乎不用磁盘碎片整理，但是FAT这种链式磁盘管理方式就需要磁盘碎片整理

ext2基本是多个区块群组，每个区块群组都有独立的inode、数据区块、超级区块系统,文件系统最前面有一个启动扇区

ext2原则上:

- 不再能修改区块的大小与格式除非格式化
- 每个区块最多能够放置一个文件数据
- 如果文件大于区块则会多占其他区块
- 如果文件小于区块则不能再放别的数据



> 不同启动扇区安装到别的文件系统最前端这样就能制作多重引导的环境

每一个区块群组有六个主要内容

- 数据区块

  - 有1K|2K|4K三种

    

    | 区块大小           | 1K   | 2K    | 4K   |
    | ------------------ | ---- | ----- | ---- |
    | 最大单一文件       | 16GB | 256BG | 2TB  |
    | 最大文件系统总容量 | 2TB  | 8TB   | 16TB |

    是根据inode决定的

- inode

  - 包含文件的读写属性、用户组、大小、时间、文件特性标识、真正指向的内容、每个inode表固定128B、每个文件都会占一个inode、记录一个数据区要用4B
  - inode容量计算假设区块为1K、有12个直接指向、1个间接指向、1个双间接、1个三间接
    - 所以直接指向容量=12\*1K = 12K
    - 间接容量=1K*1K/4 = 256K ----因为间接指向会指向一个新的inode但是这个inode必须直接指向数据区块所以1K/4
    - 双间接容量=256\*256\*1K=256^2 * 1K
    - 三间接容量=256^3 \* 1K
    - 总和为16GB

- superblock

  - 主要信息有数据区块和inode的总量
  - 未使用以及已经使用的inode、数据区块的数量
  - 数据区块与inode的大小
  - 文件系统的挂载时间、最近一次写入数据的时间、最近一次检验磁盘的时间等
  - 一个有效位数 0来显示文件已经挂载，1来显示为挂载

- Filesystem Description

  - 用来描述每个区块群的开始与结束，以及说明每个区块（超级区块、最招标、inode对照表）等的位置

- 区块对照表

  - 区块的使用情况都在这个表中

- inode对照表

  - 记录inode使用和未使用的inode号

ext2可以使用dumpe2fs去查看情况



> 现在centos默认为xfs所以无法使用dumpe2fs去查看



### 与目录树的关系

在新建一个目录的时候就会分配一个inode和至少一个区块

使用ls -i可以查看inode号码



### Linux文件系统的运行

当系统加载一个文件如果该文件没有被修改则设置为干净(clear),如果被修改了就设置为脏(dirty)不定时的会向硬盘中会写,还可以使用sync来进行同步来达到数据的一致性------异步处理



文件系统与内存的关系:

- 系统会把常用的文件放到内存中这样会加快系统性能,所以内存经常满了是正常的
- 关机命令会主动调用sync来将数据写到磁盘中
- 若不能正常关机数据不能写到硬盘中,因此重启时会有很长时间的数据校验,甚至可能导致文件系统的损坏

### Linux文件系统

查看支持的

> ls -l /lib/modules/$(uname -r)/kernel/fs

查看加载到内存的

> cat /proc/filesystems



VFS用来识别管理管理文件系统



接下来谈谈为啥要一起ext系统选择xfs

- 支持度最广,格式化很慢
- xfs适合高容量和巨型文件
- 速度虽然与xfs相似但是恢复速度-创建速度都是很慢

xfs分为三个部分数据区、文件系统活动登陆区、实时运行区

- 数据区：包含inode、数据区块、超级区块等数据，xfs与ext的不同是可以有多种不同的容量可以设置512B~64KB但由于文件系统的关系最高是4K，而inode最大是256B~2MB，一般默认256B够用了
- 文件系统活动登陆区：文件变化会记录在这里这个部分可以指定外部的磁盘来作为区块。
- 实时运行区：当文件建立时会在这个区段内找到一个到数个extent区块，将文件放置在这里等待分配完毕后，再写入data section的inode与区块中。extent区块可以设置4K~1G，最好和stripe一样大，最好不要乱动可能会影响到物理磁盘的性能

> 使用xfs_info去观察

xfs_info参数详解

```bash
[root@study ~]# df -T /boot
Filesystem Type 1k-blocks     Used     Available Use% Mounted on
/dev/vda2  xfs   1038336      133704  904632    13     /boot
# 可以看出来是xfs文件系统，观察一下
 
[root@study ~]# xfs_info /dev/vda2
1  meta-data=/dev/vda2         isize=256    agcount=4, agsize=65536 blks
2           =                  sectsz=512   attr=2, projid32bit=1
3           =                  crc=0        finobt=0
4  data     =                  bsize=4096   blocks=262144, imaxpct=25
5           =                  sunit=0      swidth=0 blks
6  naming   =version 2         bsize=4096   ascii-ci=0 ftype=0
7  log      =internal          bsize=4096   blocks=2560, version=2
8           =                  sectsz=512   sunit=0 blks, lazy-count=1
9  realtime =none              extsz=4096   blocks=0, rtextents=0
```

- 第 1 行里面的 isize 指的是 inode 的容量，每个有 256Bytes 这么大。至于 agcount 则是 前面谈到的储存区群组 (allocation group) 的个数，共有 4 个， agsize 则是指每个储 存区群组具有 65536 个 block 。配合第 4 行的 block 设置为 4K，因此整个文件系统的容 量应该就是 4655364K 这么大!
- 第 2 行里面 sectsz 指的是逻辑扇区 (sector) 的容量设置为 512Bytes 这么大的意思。
- 第 4 行里面的 bsize 指的是 block 的容量，每个 block 为 4K 的意思，共有 262144 个 block 在这个文件系统内。
- 第 5 行里面的 sunit 与 swidth 与磁盘阵列的 stripe 相关性较高。这部份我们下面格式化 的时候会举一个例子来说明。
- 第 7 行里面的 internal 指的是这个登录区的位置在文件系统内，而不是外部设备的意 思。且占用了 4K * 2560 个 block，总共约 10M 的容量。
- 第 9 行里面的 realtime 区域，里面的 extent 容量为 4K。不过目前没有使用。



### 使用df与du来查看磁盘使用情况



- df:列出文件系统的整体磁盘使用量
  - -h .以GB,MB,KB的形式显示
  - -u .不用磁盘容量,以inode来显示
  - -T .连通文件系统名称也列出来
  - -a .列出所有的文件系统包含/proc等文件系统
  - -i .列出inode资讯
- du:查看文件系统的磁盘使用情况
  - -a或-all 显示目录中个别文件的大小。
  - -b或-bytes 显示目录或文件大小时，以byte为单位。
  - -c或--total 除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和。
  - -D或--dereference-args 显示指定符号连接的源文件大小。
  - -h或--human-readable 以K，M，G为单位，提高信息的可读性。
  - -H或--si 与-h参数相同，但是K，M，G是以1000为换算单位。
  - -k或--kilobytes 以1024 bytes为单位。
  - -l或--count-links 重复计算硬件连接的文件。
  - -L<符号连接>或--dereference<符号连接> 显示选项中所指定符号连接的源文件大小。
  - -m或--megabytes 以1MB为单位。
  - -s或--summarize 仅显示总计。
  - -S或--separate-dirs 显示个别目录的大小时，并不含其子目录的大小。
  - -x或--one-file-xystem 以一开始处理时的文件系统为准，若遇上其它不同的文件系统目录则略过。
  - -X<文件>或--exclude-from=<文件> 在<文件>指定目录或文件。
  - --exclude=<目录或文件> 略过指定的目录或文件。
  - --max-depth=<目录层数> 超过指定层数的目录后，予以忽略。
  - --help 显示帮助。
  - --version 显示版本信息。

### 软硬链接

硬链接指代的是一个事实的文件并且新建一个硬链接并不会消耗inode号,因为他俩指向同一文件

不能跨文件系统,不能连接目录

ln硬链接

ln -s软连接

软链接就是快捷方式,至于大小....   ->右边几个字母大小就是几字节

```
lrwxrwxrwx 1 root root     11 12-07 16:01 link2013 -> log2013.log
```



当我们创建一个新目录的时候一般会有一下几个东西:

n

n/.

n/..

所以如果你新建一个目录则新目录会有两个链接(n或n/.)和n/.. 而上层目录的链接数会+1(因为n/..会跳到他)



### 如何划分新硬盘

#### 观察硬盘分区状态

使用lsblk列出所有存储设备

-i 代表使用ascii码

-p 代表输出完整名称不仅仅是最后的名称

>[root@YH ~]# lsblk
>NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
>sr0     11:0    1 141.4M  0 rom  
>vda    253:0    0    50G  0 disk 
>└─vda1 253:1    0    50G  0 part /

- NAME       代表设备文件名，会自动省略dev
- MAJ:MIN    代表设备是通过两个代码来实现的,分别是主要设备和次要设备
- RM         代表是否可卸载
- SIZE       代表最大容量
- RO         代表是否为只读设备
- TYPE       代表是硬盘(disk)还是分区(part)或是只读存储器(rom)等输出
- MOUNTPOINT 代表挂载目录



使用blkid来列出设备的UUID等参数

>[root@YH ~]# blkid
>/dev/sr0: UUID="2021-08-14-17-43-46-00" LABEL="config-2" TYPE="iso9660" 
>/dev/vda1: UUID="4b499d76-769a-40a0-93dc-4a31a59add28" TYPE="ext4" 



parted列出磁盘分区表类型与分区信息



### 建议的分区操作

先使用lsblk找到磁盘

使用blkid 磁盘  进行查看磁盘类型 或是使用parted 磁盘

==如果要进行分区注意了fdisk是MBR的分区表,而gdisk是GPT的分区表---!!!千万不要在MBR上面使用gdisk也不要在GPT上面使用fdisk==

使用fdisk或是gdisk进行分区

分区前先用p进行查看分区情况查看section的位置以免覆盖,使用n可以新建分区

<建议上面的操作用帮助先验证是否正确>

在使用w之前都可以用q退出来撤销,分区完后使用w进行写入,由于硬盘可能在使用中所以分区可能不会发生需要用重启或者partpeobe这个命令进行更新Linux内核信息-s会显示出来



==parted也可以进行分区==



使用fdisk进行分区

>由于我的linux采用的是ext4所有暂时先介绍fdisk

```bash
================首先使用这个命令进入分区系统============

[root@YH local]# fdisk /dev/vda
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

================d代表删除分区===============
Command (m for help): d
Selected partition 1
Partition 1 is deleted
============然后再新建一个分区===========
Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 
==========默认即可========
First sector (2048-104857599, default 2048): 
Using default value 2048
=============最后的区号=============
Last sector, +sectors or +size{K,M,G} (2048-104857599, default 104857599): 83886079
Partition 1 of type Linux and of size 40 GiB is set

====================进行第二个分区=================
Command (m for help): n
Partition type:
   p   primary (1 primary, 0 extended, 3 free)
   e   extended
Select (default p): p
Partition number (2-4, default 2): 
First sector (83886080-104857599, default 83886080): 
Using default value 83886080
Last sector, +sectors or +size{K,M,G} (83886080-104857599, default 104857599): 
Using default value 104857599
Partition 2 of type Linux and of size 10 GiB is set
=================写入分区=================
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.

WARNING: Re-reading the partition table failed with error 16: Device or resource busy.
The kernel still uses the old table. The new table will be used at
the next reboot or after you run partprobe(8) or kpartx(8)
Syncing disks.

==============使用这个命令更新分区表===============
[root@YH local]# partprobe
Warning: Unable to open /dev/sr0 read-write (Read-only file system).  /dev/sr0 has been opened read-only.
[root@YH local]# lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sr0     11:0    1 141.4M  0 rom  
vda    253:0    0    50G  0 disk 
├─vda1 253:1    0    40G  0 part /
└─vda2 253:2    0    10G  0 part 
[root@YH local]# blkid 
/dev/sr0: UUID="2021-09-10-09-46-39-00" LABEL="config-2" TYPE="iso9660" 
/dev/vda1: UUID="4b499d76-769a-40a0-93dc-4a31a59add28" TYPE="ext4" 
[root@YH local]# parted /dev/vda
GNU Parted 3.1
Using /dev/vda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print                                                            
Model: Virtio Block Device (virtblk)
Disk /dev/vda: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  42.9GB  42.9GB  primary  ext4
 2      42.9GB  53.7GB  10.7GB  primary

(parted) q                                                                

```



分区后进行格式化

使用mkfs

>[root@YH dev]# mkfs
>mkfs         mkfs.btrfs   mkfs.cramfs  mkfs.ext2    mkfs.ext3    mkfs.ext4    mkfs.minix   mkfs.xfs  

用tab tab可以查看出可以使用上面这个分区格式化命令(如果要进行格式化的分区已经存在文件系统需要加-f进行强制格式化)



#### 如果发生了意外导致关机

需要使用xfs_repair处理xfs文件系统

至于ext4则使用fsck.ext4进行处理

要使用上面的命令进行扫描磁盘不能挂载必须卸载



### 文件系统的挂载与卸载

挂载

- 单一文件系统不应该重复挂载
- 单一目录不应该重复挂载多个文件系统
- 要作为挂载点的目录,理论上要空目录才行

> 挂载了文件系统之后原目录下的东西会暂时消失

- mount:挂载命令

  ```bash
  [root@YH dev]# blkid
  /dev/sr0: UUID="2021-09-10-09-46-39-00" LABEL="config-2" TYPE="iso9660" 
  /dev/vda1: UUID="4b499d76-769a-40a0-93dc-4a31a59add28" TYPE="ext4" 
  /dev/vda2: UUID="77514366-9351-4fa2-b27e-7458d242e76c" TYPE="xfs" 
  [root@YH dev]# mkdir -p /usr/local/YH
  [root@YH dev]# cd /usr/local
  [root@YH local]# ls
  bin  etc  games  include  lib  lib64  libexec  qcloud  sbin  share  src  yd.socket.server  YH
  [root@YH local]# mount UUID="77514366-9351-4fa2-b27e-7458d242e76c" /usr/local/YH
  [root@YH local]# df /usr/local/YH
  Filesystem     1K-blocks  Used Available Use% Mounted on
  /dev/vda2       10475520  8276  10467244   1% /usr/local/YH
  
  ```

  如果挂载u盘则不能是NTFS格式

- remount:重新挂载

- umount:卸载

  - -f 强制卸载
  - -l 立即卸载(强制性再-f之上)

如果想要改为开机挂载需要修改/etc/fstab文件,但是实际的挂载文件在/etc/mtab内,但是如果fstab这个文件出现语法错误会导致无法开机

```bash
[root@YH ~]# cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Thu Mar  7 06:38:37 2019
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=4b499d76-769a-40a0-93dc-4a31a59add28 /                       ext4    defaults        1 1
==文件名==                               ==挂载目录==            ==文件系统==
```





需要进入担任维护模式运行

>mount -n -o remount,rw

### 磁盘/文件参数

硬盘上主要通过major与minor数值代表设备

例如:

```bash
[root@YH local]# lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sr0     11:0    1 141.4M  0 rom  
vda    253:0    0    50G  0 disk 
├─vda1 253:1    0    40G  0 part /
└─vda2 253:2    0    10G  0 part /usr/local/YH
```

253代表主设备代码(major)而0代表次设备代码(minor)



- mknod:可以设置major与minor
- xfs_admin:可以修改设备的UUID与Label name
- tune2fs:修改ext4的UUID和Lable

### 内存交换分区

按照物理分区进行划分

1. 分区
2. 格式化 mkswap:格式化为交换分区
3. 使用,将该分区启动 swapon:启动
4. 观察通过free与swapon -s



使用文件创建内存交换文件

1. 使用dd命令在/tmp下面新增一个文件
2. 使用mkswap 将新建的文件转换为内存交换文件格式
3. 使用swapon
4. 使用swapoff关闭并设置自动启用



## 鸭缩

常见的鸭缩格式有\*.z \*.zip \*.gz \*.bz2 \*.xz \*.tar \*.tar.gz \*.tar.bz2 \*.tar.xz

其中\*.tar代表打包程序,\*.z \*.zip \*.gz \*.bz2 \*.xz代表鸭缩文件, \*.tar.gz这种代表先打包后鸭缩

> 由于鸭缩一次只能鸭缩一个文件所以才要用tar对多个文件进行打包



### 鸭缩命令

- gzip:
  - -c数据输出可以数据流定向 
  - -d 解吖缩
  - -t 验证一致性 
  - -v 鸭缩比 
  - -#鸭缩等级 1最快,鸭缩比最差 9最慢 
  - 默认情况下用gzip鸭缩后源文件不在了
  - 读取用zcat
  
- bzip2:
  - 参数同上
  - 读取用bzcat
  
- xz:
  - 用法同上
  - 读取用xzcat
  
  
  

**源文件**

```bash
[root@YH YH]# ls -als
total 88682
    0 drwxr-xr-x   2 root root       81 Sep 11 09:03 .
    4 drwxr-xr-x. 14 root root     4096 Sep 10 10:45 ..
    1 -rw-r--r--   1 root root       46 Sep 11 08:43 1.txt.gz
88677 -rw-r--r--   1 root root 90805089 Jan 20  2018 Java语言程序设计.进阶篇.原书第10版.pdf
```

**用gzip鸭缩后**

```bash
[root@YH YH]# ls -alsr
total 71500
71495 -rw-r--r--   1 root root 73210438 Jan 20  2018 Java语言程序设计.进阶篇.原书第10版.pdf.gz
    1 -rw-r--r--   1 root root       46 Sep 11 08:43 1.txt.gz
    4 drwxr-xr-x. 14 root root     4096 Sep 10 10:45 ..
    0 drwxr-xr-x   2 root root       84 Sep 11 09:03 .
```

鸭缩比19.4%



**用bzip2:**

> 1.262:1,  6.338 bits/byte, 20.78% saved, 90805089 in, 71940276 out.



**用xz:**

>  100 %         66.3 MiB / 86.6 MiB = 0.766   2.2 MiB/s       0:39 



### 打包命令

- tar:

  - -c 建立打包文件
  - -t 查看打包文件的内容有哪些文件名
  - -x 解包或解吖缩
  - -z 通过gzip的支持进行鸭缩或者解吖
  - -j 通过bzip2的支持进行鸭缩或解吖
  - -J 通过xz的支持进行鸭缩或解吖
  - -v 鸭缩与解吖过程中的文件名显示出来
  - **-f 后面要立即接要被处理的文件名**
  - -C 解吖到指定文件目录
  - -p 保留碑文数据的原本权限与属性
  - -P 保留绝对路径允许备份数据中含有根目录存在之意

- 常用的tar命令

  - 鸭缩:tar -jcv -f filename.tar.bz2 要被鸭缩的文件或目录;
  - 查询:tar -jtv -f filename.tar.bz2;
  - 解吖缩:tar -jxv -f filename.tar.bz2 -C 要解压的目录
  - 解开单一文件:
    - tar -jtv -f /root/etc.tar.bz2 | grep '要解吖的文件名' 这样可以查出来
    - tar -jxv -f 打包的文件.tar.bz2 待解开的文件名

  注意鸭缩的时候最好自己加上.tar.[bz2|xz|gz]



==建议经常使用tar备份etc==

time tar -zpcv -f etc.tar.gz /etc

```bash
real	0m3.923s
user	0m1.125s
sys	0m0.097s
```



time tar -jpcv -f etc.tar.bz2 /etc

```bash
real	0m2.945s
user	0m2.838s
sys	0m0.053s
```



time tar -Jpcv -f etc.tar.xz /etc

```bash
real	0m12.140s
user	0m11.764s
sys	0m0.129s
```

原本大小

> 37MB	/etc

```bash
-rw-r--r--   1 root root  9453958 Sep 11 10:08 etc.tar.bz2
-rw-r--r--   1 root root 10732764 Sep 11 10:04 etc.tar.gz
-rw-r--r--   1 root root  7632840 Sep 11 10:09 etc.tar.xz
```



#### 如果要打包目录但是不包含某些文件

tar -jcv -f /root/system.tar.bz2 --exclude=/root/etc*

--exclude=不想要包含的文件

*代表通配符



### 备份



#### 仅备份比某个时候更新的文件

--newer(包含mtime与ctime)

--newer-mtime(只能用mtime)

- atime:***\*显示的是文件中的数据最后被访问的时间\****
- mtime:***\*显示的是文件内容被修改的最后时间\****
- ctime:***\*显示的是文件的权限、拥有者、所属的组、链接数改变、文件内容改变的时间。\****

> 通常所说的tarfile代表只进行打包,tarbali代表打包鸭缩



#### 关于SELinux问题

SELinux可能会让你的系统无法读写配置文件,导致影响到系统的正常使用

如果使用上面的方法进行备份恢复但是无法正常使用可能是/etc/shadow这个密码文件的SELinux类在还原时被修改了导致无法正常登录

处理方法:

- 方法一:修改/etc/selinux/config文件将SELinux改成permissive模式重启;
- 方法二:在第一次恢复系统后不要立即重启先使用restorecon -Rv /etc 自动修复一下SELinux即可
- 方法三:通过各种可行的方式登录系统,建立/.autorelabel文件,重新启动后系统会自动修复SELinux并会再次重启后正常



#### XFS文件系统的备份与还原

xfsdump命令：增量备份,与git差不多显示出与上一份增加的文件的差异

记录文件放在/var/lib/xfsdump/inventory

注意:

- 不支持没有挂载的文件系统备份
- 必须使用root
- 只能备份xfs
- 备份的数据只能用xfsrestore解析
- 通过UUID来识别各个备份文件
- 支持文件系统的备份并不支持特定目录的备份,不能备份/etc

备份测试

```bash
xfsdump -l 0 -L vda2_all -M vda2_all -f /vda2.dump /usr/local/YH
进行备份

xfsdump -I
查看结果

dd if=/dev/zero of=/usr/local/YH/test.img bs=1M count=10
新增文件

 xfsdump -l 1 -L vda2_2 -M vda2_2 -f /vda2.dump1 /usr/local/YH
再次新增
//注意只有建立过-l 0 才能-l [1~9]进行增量备份

```



使用-xfsrestore进行恢复

xfsrestore [-f 备份文件] -r 待恢复目录



- dd:

  - if(input file):可以是设备

  - of(output file):可以是设备

  - bs:设置一个block的大小,默认512Bytes(一个扇区大小)

  - count多少个bs

  - > dd if=/dev/zero of=/usr/local/YH/test.img bs=1M count=10
    > 10+0 records in
    > 10+0 records out
    >
    > 例如上面这个例子代表将/dev/zero备份到/usr/local/YH/test.img 每个分区为1M 设置10个分区 下面10+0代表10个完整的1M以及0个未满1M的意思

    使用dd复制后如果发现无法使用某些分区或者文件系统使用下面的命令

    >xfs_repair -L /dev/sda1 #清理log
    >
    >uuidgen 获得新的uuid
    >
    >xfs_admin -U 新获得的UUID 设备驱动
    >
    >由于dd连uuid也一起复制二xfs主要使用uuid来区分文件系统所以要在给一个uuid

- cpio:以后再说



## vim

### vim的缓存与恢复

当我们编辑文件时会在与编辑的目录下生成一个.filename.swp的文件,例如

vi /YH.txt 会有.YH.text.swp 这个文件就是用来记录修改信息的

如果发生意外vim中断下次进入时按R即可恢复缓存内容但是那个缓存文件需要你自己删除否则会一直警告

如果这个缓存没用了按D进行删除vim会自己再建立一个

> 注意vi与vim不一样有的时候系统默认vi就是vim使用alias命令即可查看
>
> [root@YH vitest]# alias
> alias cp='cp -i'
> alias egrep='egrep --color=auto'
> alias fgrep='fgrep --color=auto'
> alias grep='grep --color=auto'
> alias l.='ls -d .* --color=auto'
> alias ll='ls -l --color=auto'
> alias ls='ls --color=auto'
> alias mv='mv -i'
> alias rm='rm -i'
> alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

区块编辑

移动到区块最开始的位置按下ctrl+v然后移动光标会这样

![image-20210912110828669](C:\Users\lll\AppData\Roaming\Typora\typora-user-images\image-20210912110828669.png)

按下y进行复制按p可以粘贴

### 多文件编辑

vim可以使用 vim [file1] [file2]进行同时编辑

使用:files可以显示所有要编辑的文件

>:files
>1 %a   "man.test.conf"                line 1
>2      "/etc/host"                    line 0
>Press ENTER or type command to continue



### 多窗口编辑

| 命令                 | 结果                                                       |
| -------------------- | ---------------------------------------------------------- |
| :sp [filename]       | 添加一个窗口不加filename就是创建两个窗口但是同一文件       |
| ctrl+w+↑或者ctrl+w+↓ | 进行窗口的切换                                             |
| ctrl+x               | 下方弹出所有的可补全提示常用的有ctrl+o以文件扩展名方式补充 |
| :set nu              | 设置与取消行号,nonu取消行号                                |
| :set autoindent      | 设置是否自动缩进,noautoindent不缩进                        |
| :set all             | 显示目前所有的环境参数设置值                               |

![img](https://img2018.cnblogs.com/blog/1442837/201811/1442837-20181121151226556-202455126.png)



### 中文乱码问题

- 系统默认的语言:/etc/locale.conf

- bash的语系:LANG、LC_ALL变量有关

- 文件原本编码
- 打开终端的软件
- 使用iconv进行转码



## Shell

查看可使用的shell

/etc/shells这个文件

再/etc/passwd这个文件中最后一个内容代表登陆后使用的shell类型

![image-20210913091729821](C:\Users\lll\AppData\Roaming\Typora\typora-user-images\image-20210913091729821.png)

- 对于shell一般能存1000条命令,对于上次登陆的命令都留在~/.bash_history,而这一次都放在内存中
- 如果安装了bash-completion按tab时可以进行(选项/参数补齐)功能
- alise别名功能,举个例子 ll=ls -l --color=auto

- 使用type来查看是否为内置命令
  - type [-tpa] name
  - -t 会显示一些其他属性
  - -p 如果接name为外部命令才会显示完整名称
  - -a 会由path变量定义的路径中所有含有name的命令都列出来

### 环境变量

使用echo $PATH可以输出PATH变量

使用=可以对环境变量进行改变

> [root@YH mail]# YH=1
>
> [root@YH mail]# echo $YH
> 1

但是必须符合以下规则

- 变量与变量内容必须用=连接

- 等号两边不能有空格

- 变量名只能是字母或数字,但是不能是数字开头

- 双引号内如果有特殊字符,则会保留原意

  - >[root@YH ~]# YH=$PATH
    >[root@YH ~]# echo $YH
    >/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin

- 单引号内如果有特殊字符则不会保留原意

  - >[root@YH ~]# YH='$PATH'
    >[root@YH ~]# echo $YH
    >$PATH

- 使用``或者$()可以在命令中使用命令

  - > cd /lib/modules/\`uname -r\`/kernel
    >
    > 其中uname -r的值为
    >
    > [root@YH kernel]# uname -r
    > 3.10.0-1160.11.1.el7.x86_64

- 使用unset进行取消设置



shell一般有两种登录方式而这两种登录方式读取根据文件读取的shell也不一样

我们普通的登录时用密码就称为login,而使用Xwindows登录时第一次会输入密码再然后就不用输入密码了这种成为non-login

login启动时会读取以下两个配置文件:

- /etc/profile:这是系统整体的设置
- ~/.bash_profile或~/.bash_login或~/.profile:属于用户个人设置

#### bash环境配置文件

https://blog.csdn.net/qq_36121238/article/details/103473054

太多了。。。



### 查看环境变量

- 使用env命令

  - >XDG_SESSION_ID=5449               <\=\=\=主机名
    >HOSTNAME=YH                
    >TERM=xterm                <\=\=\=使用的终端环境类型
    >SHELL=/bin/bash                 <\=\=\=使用的bash类型
    >HISTSIZE=3000                        <\=\=\=记录的命令个数
    >SSH_CLIENT=144.12.230.5 48025 22
    >OLDPWD=/usr/local/YH                <\=\=\=上一个工作目录
    >SSH_TTY=/dev/pts/6
    >USER=root                          <\=\=\=使用者名称
    >LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=01;05;37;41:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.axv=01;35:*.anx=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=01;36:*.au=01;36:*.flac=01;36:*.mid=01;36:*.midi=01;36:*.mka=01;36:*.mp3=01;36:*.mpc=01;36:*.ogg=01;36:*.ra=01;36:*.wav=01;36:*.axa=01;36:*.oga=01;36:*.spx=01;36:*.xspf=01;36:
    >MAIL=/var/spool/mail/root                        <\=\=\=mailbox的位置 
    >PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
    >PWD=/usr/local
    >LANG=en_US.utf8                <\=\=\=语言                             
    >SHLVL=1
    >HOME=/root                   <\=\=\=用户目录  
    >LOGNAME=root
    >SSH_CONNECTION=144.12.230.5 48025 172.17.0.5 22
    >LESSOPEN=||/usr/bin/lesspipe.sh %s
    >PROMPT_COMMAND=history -a; history -a; printf "\033]0;%s@%s:%s\007" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/~}"
    >XDG_RUNTIME_DIR=/run/user/0
    >HISTTIMEFORMAT=%F %T 
    >_=/usr/bin/env

- 使用set观察(包含环境变量与自定义变量)
  - 其中PS1这个变量用于改变[11:08:32 root@YH YH]# 
  - 很多就不细讲了
- $?上一个命令的返回值一般正常返回0
- $$查看bash的pid
- OSTYPE、HOSTTYPE、MACHTYPE
- export将自定义变量转换为环境变量，子进程可以使用父进程的环境变量但是无法使用自定义变量
  - export [变量名称]如果不写变量名称会把所有环境变量都列出来
- 使用locale可以显示出所有支持的语系



### 设置变量

- 使用read可以交互式设置变量

  - read [-p提示字符t等待秒数] variable将数据读取到variable变量中

- declare,typeset:声明变量类型,如果declare后面没有任何参数直接显示出所有的变量名与内容与set差不多,

  - declare [-a数组-i整形-x与export一样-r设为readonly]
> 设置永久变量https://blog.csdn.net/u010794523/article/details/38622275/




### 使用ulimit

由于Linux可以多个用户同时登录使用所有要为每个用户设置资源占比

- ulimit

  - -a 　显示目前资源限制的设定。
  - -c <core文件上限> 　设定core文件的最大值，单位为区块。
  - -d <数据节区大小> 　程序数据节区的最大值，单位为KB。
  - -f <文件大小> 　shell所能建立的最大文件，单位为区块。
  - -H 　设定资源的硬性限制，也就是管理员所设下的限制。
  - -m <内存大小> 　指定可使用内存的上限，单位为KB。
  - -n <文件数目> 　指定同一时间最多可开启的文件数。
  - -p <缓冲区大小> 　指定管道缓冲区的大小，单位512字节。
  - -s <堆叠大小> 　指定堆叠的上限，单位为KB。
  - -S 　设定资源的弹性限制。(警告)
  - -t <CPU时间> 　指定CPU使用时间的上限，单位为秒。
  - -u <程序数目> 　用户最多可开启的程序数目。
  - -v <虚拟内存大小> 　指定可使用的虚拟内存上限，单位为KB。


### 删除变量中的内容

#从前面删除[最小匹配]  ${变量#关键字}

##从前面删除[最大匹配]  ${变量##关键字}

%从后面删除[最小匹配]  ${变量%关键字}

%%从后面删除[最大匹配]  ${变量%%关键字}

/替换符合字符串的第一个内容  ${变量/旧字符串/新字符串}

//替换符合字符串的所有字符串  ${变量//旧字符串/新字符串}



### 别名

alise 

命名规则与变量命名规则几乎一样

alise 别名='命令 选项'

### history

查看历史命令的命令

- n:最近n条命令
- -c:清除目前的shell中所有history内容
- -a:将目前新增的history写入到histfiles中默认写入~/.bash_history
- -r:将目前的history记录内容读到shell的histfiles中
- -w:将目前history内容写入histfiles中

使用!命令

- !!执行上一条命令
- !n执行第n条命令
- !vi执行近来vi开头的命令

### 命令执行顺序

- 包含绝对或者相对路径的命令
- 由alias命令执行
- 由bash内置的命令执行
- 通过$PATH变量来找到第一个命令执行



#### bash的欢迎信息

/etc/issue

/etc/motd





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

- **可分享**：可以分享给其他系统挂载使用的目录，包括执行文件与用户的邮件等数据，能够分享给网络上其他主机挂载用的目录
- **不可分享**：自己机器上面运行的设备文件或是与程序有关的socket文件等，由于仅与自身机器有关，所以当然就不适合分享给其他主机
- **不变**：有些数据是不会经常变动的，跟随着发行版而不变动。例如函数库、文件说明、系统管理员所管理的主机服务配置文件
- **可变动**：经常修改的数据，例如日志文件、一般用户可自行接受的新闻组等

>事实上FHS针对目录树架构仅定义出三层目录下面应该放置什么数据而已，分别是下面这三个目录的定义：

- /（root，根目录）：与启动系统有关
- /usr（unix software resource）：与软件安装/执行有关
- /var（variable）：与系统运行过程有关

根目录（/）的意义与内容

>所有的目录都是由根目录衍生出来，同时根目录与启动、还原、系统修复等操作有关
>系统启动时需要特定的启动软件、内核文件、启动所需程序、函数库等文件数据
>软系统出现错误是，根目录也必须包含能够修复文件系统的程序才行

>FHS标准建议：根目录所在的分区应该越小越好，且应用程序所安装的软件最好不要与根目录放在同一个分区内，保持根目录越小越好。如此不但性能较佳，根目录所在的文件系统也较不容易发生问题。

根目录下文件的作用https://www.cnblogs.com/jszd/p/11182190.html

- /bin:(普通用户和管理员常用命令，存放在**单人维护模式下还能够被使用的命令**)
- /boot:(主要放置启动会用到的文件)
- /dev:(任何设备与接口都是以文件形式存放在这个目录)
  - /shm通常是利用虚拟出来的磁盘通常占内存的一般物理内存,在里面建东西的速度是很快的
- /usr:(存放系统软件资源，放置的数据属于可分享与不可变动)
  - /bin:所有一般用户能够使用的命令都放在这里。同时此目录下不应该有子目录
  - /lib:与/lib功能相同所以/lib链接到此目录的
  - /local:root在本机安装自己下载的软件，建议安装到本目录，便于管理
  - /sbin:非系统正常运行所需要的系统命令。目前/sbin目录就链接到此目录中的
  - /share:存放命令帮助文档和者软件帮助文档，几乎都是文本文件
  - /games:与游戏相关的数据
  - /include:c++等程序语言的头文件与包含文件放置处
  - /libexec:某些不被一般用户常用的执行文件或脚本
  - /src:一般源码放在这里
- /etc:(系统配置文件几乎都在这个目录但只有root有权利修改,==建议不要将可执行文件放在该目录里面==)
  - /passwd:存放各个用户的信息
  - /shadow:存放个人密码
  - /group:所有组个名在这里面
  - /locale.conf:可以修改系统语言
  - /opt（必要）:这个目录在防止第三方辅助软件/opt的相关配置文件
  - /filesystems:系统指定的测试挂载文件系统类型的优先级
  - /shells:显示可以使用的shell
  - /profile.d
    - /*.sh:这里面所有的用户r权限的文件都会被/etc/profile调用,包含了操作界面的颜色、语系、别名等
  - /sysconfig
    - /network-scripts:网络配置目录
- /media: 存放**可删除的设备**
- /mnt:暂时挂载某些额外的设备
- /var：系统运行后占用硬盘容量的目录
  - /cache:应用程序本身运行过程中产生的一些缓存
  - /lib:程序本身执行过程中，需要使用到的数据文件放置的目录。此目录下各自软件要有各自的目录
    - /xfsdump
      - /inventory:xfsdump的备份记录
  - /lock：防止设备或文件同一时刻被多用户使用，使用时给该设备上锁，确保该设备只给单一软件使用（已经转移到/run/lock中）
  - /run：程序或服务启动后，将PID放置到这个目录，与/run相同，链接到/run目录
  - /mail：个人用户邮箱，也被放置到/var/spool/mail目录，通常这两个目录互为链接文件
  - /spool:放置队列数据。排队等待其他程序使用的数据，使用后会被删除
    - /cron: 计划任务数据
  - /spool
    - /news(新闻组)
  - /log：非常重要，日志文件放置的目录
    - /wtmp这个文件用来存放登录数据
- /run:系统启动后所产生的各项信息
- /tmp:一般用户或正在执行的程序暂时放置文件的地方。任何人都可以存取，建议在启动时将本目录下数据都清除
- /run或/tmp数据接口文件常用来通过soocket来进行数据沟通
- /lib:(放置的是启动时会用到的库函数,以及在/bin和/sbin下面的命令会调用的库函数)
  - /modules:放置驱动程序
    - $(uname -r)/kernel/fs
      - 例如ext4驱动就在/lib/modules/$(uname -r)/kernel/fs/ext4下
- /opt:(给第三方辅助软件放置的目录，以前的linux系统中，习惯安装在/usr/local下)
- /sbin:(很多命令是用来设置系统环境的,这些命令只有root才能设置系统里面包含了修复启动还原系统所需要的命令)
  - 某些服务器软件程序放置在/usr/sbin中.本机自行安装的软件所产生中的系统执行文件,则放置到/usr/local/sbin
- /srv:(网络服务器运行后所需要使用的数据目录)
- /home:(普通用户的家目录,~回到这个目录下的指定文件)
- /root:(root用户的家目录，root的家目录和根目录放置在同一个分区中)
- /proc:(本身是虚拟文件系统，数据都放置在内存中。系统的信息例如内核、进程信息、外接设备、网络状况，他放置的数据都在内存中)
  - filesystems:Linux已经加载的文件系统类型
- /sys:不占硬盘容量也是保存系统信息的.
