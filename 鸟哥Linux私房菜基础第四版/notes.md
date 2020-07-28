# 基础学习篇

## 第零章 计算机概论

五大组成部分：输入、输出、控制器、逻辑运算单元和内存

CPU架构：
* 精简指令集：Reduced Instruction Set Computer, RISC
  * 甲骨文 （Oracle） 公司的 SPARC 系列
  * IBM 公司的 Power Architecture （包括 PowerPC） 系列
  * （ARM Holdings） 的 ARM CPU 系列
* 复杂指令集：Complex Instruction Set Computer, CISC
  * 主要有AMD、Intel、VIA等的x86架构的CPU（为何成为x86架构：最早的那颗Intel发展出来的CPU代号称为8086）

常用计算单位：
  * 容量：用二进制
  * 速度：用十进制
  * 硬盘厂商标识可能是十进制，系统识别是二进制，导致不一样

常用的个人电脑主板架构（物理结构，以Intel为例）
  * 北桥：负责链接速度较快的CPU、内存与显卡接口等元件（大多将北桥内存控制器整合到 CPU 封装当中了）
  * 南桥：负责连接速度较慢的设备接口， 包括硬盘、USB、网卡等等 
  * CPU:
  * 显卡：
  * 网卡：          
  * 内存

CPU工作频率：
  * 外频
  * 倍频
  * 超频：现在的CPU可以根据使用情况自动进行频率变动

内存：
  * DRAM
  * SRAM

系统参数（如网卡、显卡是否启动）记录在主板上CMOS芯片上，需要有电（故有电源）

BIOS是写死到主板上的一个内存芯片中的程序（ROM），以前是不可更改，但是现在通常是写入类似闪存或EEPROM中。

显卡与屏幕连接的格式：D-Sub (VGA端子) 模拟信号；DVI; HDMI; Display port

#### 硬盘与存储设备

存储设备：硬盘、软盘、MO、CD、DVD、磁带机、U盘（闪存）、蓝光光驱、SAN、NAS

传输接口
* SATA接口：已取代了IDE接口
* SAS接口：
* USB接口：
* 固态硬盘：

## 第一章 Linux是什么与如何学习

查看内核版本相关信息：
* uname 
    * -a: 打印所有信息
    * -r: 打印核心的发布信息

## 第二章 主机规划与磁盘分区

显卡相关接口：VGA, DVI, HDMI, DP

磁盘分区：
* 磁盘的第一个扇区，记录磁盘的重要信息（MBR方式）；
  * MBR (Master Boot Record, MBR): 可以安装开机管理程序的地方，有446 Bytes
  * 分区表 (partition table)：记录整颗硬盘分区的状态，有64Bytes，所以只能记录四个分区(Primary分区或Extended分区，Extended最多只能有一个，但可以利用延伸分区继续分下去，即逻辑分区)
* GPT(GUID partition table): 新的磁盘分区格式
  * 磁盘扇区不再仅仅是512Bytes，可高达4K，使用逻辑区块位址(Logical Block Address, LBA)，默认是512B，使用34个LBA记录分区信息，磁盘最后也有33个用作备份。
  * LBA0: MBR相容区块，与MBR类似，只不过分区表的位置仅放入了一个特殊的标志


### BIOS与UEFI开机检测程序

* BIOS搭配MBR/GPT的开机流程
    * CMOS：记录各项硬件参数嵌入在主板上的储存器
    * BIOS：写入到主板上的一个固件，开机主动执行的固件，会认识第一个可开机的设备
    * MBR：第一个可开机设备的第一个扇区内的主要开机记录区块，内含开机管理程序
    * 开机管理程序(boot loader)：一个可读取核心文件来执行的软件
        * 提供菜单：使用者可以选择不同的开机项目
        * 载入核心文件：直接指向真正可开机的程序区段来开始操作系统
        * 转交其他loader：将开机管理功能转交给其他的loader负责
        * 开机管理程序既可以安装在MBR区，也可以安装在每个分区的boot sector
    * 核心文件：开始操作系统的功能
    * 说明：BIOS也能够从GPT格式的LBA0的与MBR相容区块读取第一阶段的开机管理程序码，如果开机管理程序能够认识GPT的话，那么也可以开机成功，否则开机失败

* UEFI BIOS 搭配GPT开机的流程
  * UEFI 主要是想要取代 BIOS 这个固件界面
  * 也称UEFI为UEFI BIOS

## 第三章 安装CentOS7.x

## 第四章 首次登录与线上求助

* ctrl + alt + F2 ~ F6: 命令行登录tty2 ~tty6终端机
* ctrl + alt + F1：图形接口桌面

命令行下：startx  启动窗口界面

指令的下达方式：command [-option] parameter1 parameter2 ...
* 指令太长时，可以通过\来连续到下一行
* 选项之前通常会带 - 号，使用完整全名时，会带有 -- 号
* 显示的语言的更改
  * 查看：locale
  * 更改：LANG=en_US.UTF-8  （等号两端没有空格）；export LC_ALL=en_US.UTF-8
* date指定格式：date +%Y%m%d%H%M
* cal [month] [year]
* 简单计算器：bc
* 命令补全和文件补全：[tab]键
* ctrl+c：中断目前的程序；ctrl+d：键盘输入结束/exit
* 连续两个[tab][tab]的作用：文件查看，命令补全
* [Shift] + [Page Up]/[Page Down]上下翻页
* help与man：使用空格键即可完成翻页；输入/word进行关键字搜索（man命令）；以前用过的命令用help查看参数，否则最好通过man进行学习
* man -f [指令名] = whatis [指令名]      man -k [man文档中包含的名称] = apropos [man文档中包含的名称]
* 数据同步到硬盘：sync
* shutdown [-khrc] [time] [warning]  reboot, halt, poweroff
* 使用反斜杠`\`是命令连续到下一行
* 正确的关机步骤：
  * 谁在线：`who`
  * 网络的连线状态：`netstat -a`
  * 背景执行的程序：`ps -aux`
  * 同步数据：`sync`
  * 关机相关指令：`shutdown`, `reboot`, `halt`, `poweroff`, `systemctl`

## 第五章 Linux的文件权限与目录配置

### 5.1 使用者与群组

* 拥有者、组、其他人
* /etc/passwd, /etc/shadow, /etc/group

### 5.2 文件权限概念

* [权限][链接][拥有者][群组][文件大小][修改日期][文件名]
* 权限：
  * 第一个字符：
    * d: 目录
    * -: 文件
    * l: 链接文件
    * b: 设备文件中可供存储的周边设备
    * c: 设备文件中的序列埠设备，如键盘、鼠标
* 链接：表示有多少文件名链接到此节点
* 文件夹的权限注意：如果只有读的权限，那么用户不能打开这个文件夹
* 无论文件权限为何，默认root都可以存取
* chgrp: 改变文件所属群组 chgrp [-R] 组名  目录名/文件名
* chown: 改变文件拥有者 chown [-R] 用户名[:组名]  文件或目录
* chmod: 改变文件的权限，SUID, SGID, SBIT等等特性  
  * chmod xyz 文件或目录  
  * chmod u=rwx, go=rx 文件或目录  等号两边无空格
  * chmod u+x 文件或目录
* 复制会复制执行者的属性与权限
* 权限对于文件
  * r：可读取文件内容
  * w：可以编辑、新增或者修改文件内容，单不包含删除
  * x：该文件具有被系统执行的权限
* 权限对于目录
  * r：具有读取目录结构清单的权限，如可以用ls显示目录的内容列表
  * w：具有改动该目录结构清单的权限，即
    * 创建新的文件与目录
    * 删除已经存在的文件与目录（不论该文件的权限为何）
    * 将已存在的文件或目录进行更名
    * 搬移该目录内的文件、目录位置
  * x：代表使用者能否进行该目录成为工作目录

### 5.3 Linux目录配置

* usr：unix software resource
* 查看linux核心版本：uname -r
* 查看操作系统的位数：uname -m
* 查看操作系统信息
  * 先安装：yum install redhat-lsb
  * 查看：lsb_release -a

## 第六章 Linux文件与目录

### 6.1 目录与路径

* 特殊的目录
  * .：代表此层目录
  * ..：代表上层目录
  * -：代表前一个工作目录
  * ~：代表“目前使用者身份”所在的主文件夹
  * ~account：代表account这个使用者的主文件夹
* 根目录中.和..是同一个目录
* 目录操作常用命令
  * cd：变换目录
  * pwd：显示目前的目录 [-P]显示出真正的路径，而不是链接路径
  * mkdir：创建一个新的目录 -p：递归创建  -m：设置权限
  * rmdir：删除一个空的目录 [-p]
  * rm: 删除文件及非空目录
* 环境变量
  * echo $PATH
  * PATH="${PATH}:/root"

### 6.2 文件与目录管理

ls常用选项
* -a：全部的文件，连同隐藏文件
* -d：仅列出目录本身，不列出目录内的文件数据
* -l：长数据串行出，包含文件的属性与权限等等

cp [options] source1 source2 source3 ... directory
* -a: 相当于 -dr --preserve=all
* -d: 若来源文件为链接文件的属性，则复制链接文件属性而非文件本身
* -f:
* -i: 若目标文件存在时，在覆盖时会先询问动作的进行
* -l:
* -p: 连同文件的属性一起复制过去
* -r: 递归持续复制，用于目录的复制行为
* -s: 复制成为符号链接文件
* -u:
* --preserve=all
* 使用时
  * 是否需要完整的保留来源文件的信息
  * 来源文件是否为链接文件
  * 来源文件是否为特殊的文件，如FIFO, socket
  * 来源文件是否为目录

rm [-fir] 文件或目录

* -f: 就是force的意思
* -i: 互动模式，在删除前会询问
* -r: 递归删除
* \rm -r /tmp/etc: 在指令前加反斜杠，可以忽略掉alias的指定选项

mv [options] source1 source2 ... directory

* -f: fource
* -i: 交互式
* -u: 若目标文件已经存在，且source比较新，才会更新
* 使用mv修改名称
* 新增命令rename

basename

dirname

### 6.3 文件内容查阅

* cat: 从第一行显示文件内容
* tac：从最后一行开始显示文件内容
* nl：显示的时候输出行号
* more：一页一页的显示
  * space：向下翻页
  * Enter：下翻一行
  * /字串：向下搜寻“字串”
  * :f : 立刻显示出文件名以及目录
  * q：代表立刻离开more
* less：与more类似，可以往前翻页
* head：只看头几行
  * head [-n number] 文件
* tail：只看尾几行
* od：以二进制的方式读取文件内容
* 关于文件的三个时间
  * mtime：modification time, 文件的内容数据改变时
  * ctime: status time, 文件状态改变时
  * atime: access time, 文件的内容被取用时
* touch [-acdmt] 文件
  * -a: 仅修订access time
  * -c: 仅修改文件时间，若不存在则不修改
  * -d: 后面可以接欲修订的时间
  * -m：仅修改mtime
  * -t: 

### 6.4 文件与目录的默认权限与隐藏权限

umask/umask -S, 查看默认权限，数字显示的是被拿掉的权限，但文件默认都没有执行权限

* 例如如果umask是002，则(root用户默认的umask拿掉的权限较多，默认值是0022)
  * 创建文件时：(-rw-rw-rw-) - (-----w--w-) ==> -rw-r-r-
  * 创建目录时：(drwxrwxrwx) - (d----w--w-) ==> drwxr-xr-x

设置文件隐藏属性 chattr [+-=] [ASacdistu] 文件或目录名称

* +: 增加一个特殊参数，其余参数不变
* -: 减去一个特殊参数，其余原本参数不变
* =: 设置一定，且仅有后面接的参数
* -a: 当设置a之后，这个文件将只能增加数据，不能删除也不能修改数据，只有root能设置这个属性
* -i: 让一个文件不能被删除，改名，设置链接也无法写入或新增数据

显示文件隐藏属性  lsattr [-adR] 文件或目录
* -a: 将隐藏文件的属性也显示出来
* -d: 如果接的是目录，仅列出目录本身的属性而非目录内的文件
* -R: 联通子目录的数据也一并列出来

Set UID (SUID)：当s这个标志出现在文件拥有者的x权限上时，例如的/usr/bin/passwd，这个权限拥有的功能：
* SUID仅对二进制程序有效（不能用在shell script上）
* 执行者对于该程序需要具有x的可执行权限
* 本权限仅在执行该程序的过程中有效
* 执行者将具有该程序拥有者的权限

Set GID (SGID)：当s标志出现在群组的x时则称为Set GID , SGID权限
* 对于文件：
  * SGID对二进制程序有用
  * 执行者对于该文件来说，需要具备x的权限
  * 执行者在执行过程中将会获得该程序群组的支持
* 对于目录：
  * 使用者若对于此目录有r和x的权限，该使用者能够进入此目录
  * 使用者在此目录下的有效群组将会变成该目录的群组
  * 用途：若使用者在此目录下具有w权限，则使用者所创建的新文件，该新文件的群组与此目录的群组相同

Sticky Bit

只对目录有效，作用：
* 当使用者对于此目录具有w，x权限时
* 当使用者在该目录下创建文件或目录时，仅有自己与root才有权力删除该文件

SUID/SGID/SBIT 权限设置
* 在之前三个数字的基础上加上一个数字
  * 4为SUID
  * 2为SGID
  * 1为SBIT
* 符号法处理：如u+s

观察文件类型  file


### 6.5 指令与文件的搜索

which [-a] command
* history是bash内置指令，无法通过which找到

whereis [-bmsu] 文件或目录

locate [-ir] keyword，数据库默认一天更新一次，可用命令updatedb进行更新

find [PATH] [option] [action]


## 第七章 Linux磁盘与文件系统管理

### 7.1 认识Linux文件系统

* 磁盘分区的两种格式：MBR（限制较多）何GPT（限制较少）两种格式
* 传统：一个分区只能被格式化为一个文件系统；新技术的应用，一个分区可以格式化为多个文件系统，多个分区也能合并为一个文件系统，故一个可被挂载的数据为一个文件系统而不是一个分区
* superblock, inode, block
  * superblock: 记录文件系统的整体信息，包括inode与block的总量、使用量、剩余量 
  * inode: 存放权限与属性，一个文件占用一个inode，同时记录此文件的数据所在的block号码
  * data block: 记录文件实际数据，若文件太大时，会占用多个block
    * block的大小与数量在格式化完就不能够再改变了（除非重新格式化）
    * 每个block内最多只能够放置一个文件的数据
    * 如果文件大于block的大小，则一个文件会占用多个block数量
    * 若文件小于block，则该block的剩余容量就不能够再被使用了

  Block大小 | 1KB | 2KB | 4KB
  ---| ---| ---|---
  最大单一文件限制|16GB|256G|2TB
  最大文件系统总容量|2TB|8TB|16TB

* 索引式文件系统(ext)
* 链式文件系统(FAT，常用于U盘)（重组会加快读写速度）
* 目录的保存
* inode 本身并不记录文件名，文件名的记录是在目录的block中

* 挂载点的意义
  * 将文件系统与目录树结合的动作我们称为“挂载”

### 7.2 文件系统的简单操作

* df：列出文件系统的整体磁盘使用量
  * df [-ahikHTm] [目录或文件名]
* du: 评估文件系统的磁盘使用量（用于估计目录所占容量）
  * du [-ahskm] 文件或目录名称
* Hard Link
  * 通过文件系统的inode链接来产生新文件名，而不是产生新文件（多个文件名对应到相同的一个inode号码）
  * 只是在某个目录下新增一笔文件名链接到某inode号码的关联记录而已
  * 不能跨filesystem
  * 不能link目录
* Symbolic Link
  * 创建一个独立的文件，而这个文件会让数据的读取指向其link的那个文件的文件名（当源文件被删除之后，symbolic link的文件会打开不了）
* ln [-sf] 来源文件 目标文件
  * -s: symbolic link, 不加参数则默认是hard link
  * -r: 如果目标文件存在时，将目标文件移除后再创建

### 7.3 磁盘的分区、格式化、检验与挂载

* lsblk: 列出系统上所有磁盘列表
  * lsblk [-dfimpt] [device]
* blkid: 列出设备的UUID等参数
* parted: 列出磁盘的分区表类型与分区信息
* 磁盘分区：fdisk/gdisk
  * gdisk 设备名称
  * fdisk 设备名称
* 磁盘格式化：
  * xfs文件系统：mkfs.xfs
  * ext4文件系统：mkfs.ext4
  * 其他文件系统：mkfs
* 文件系统检验
  * xfs_repair
  * fsck.ext4
* 文件系统挂载与卸载
  * 单一文件系统不应该被重复挂载在不同的挂载点（目录）中
  * 单一目录不应该重复挂载多个文件系统
  * 要作为挂载点的目录，应该为空目录
  * mount 

### 7.4 设置开机挂载

### 7.5 创建swap分区

## 第八章 文件与文件系统的压缩、打包与备份

### 8.1 压缩文件的用途与技术

### 8.2 Linux系统常见的压缩指令

扩展名|压缩程序
---|---
*.Z | compress程序压缩的文件
*.zip | zip程序压缩的文件
*.gz | gzip程序压缩的文件
*.bz2 | bzip2程序压缩的文件
*.xz | xz程序压缩的文件
*.tar | tar程序打包的数据，并没有压缩
*.tar.gz | tar程序打包的文件，并经过gzip压缩
*.tar.bz2 | tar程序打包的文件，并经过bzip2压缩
*.tar.xz | tar程序打包的文件，并经过xz的压缩

* gzip [-cdtv#] 文件名; zcat/zmore/zless 文件名.gz
* bzip2 [-cdkzv#] 文件名; bzcat 文件名.bz2
* xz [-dtlkc#] 文件名; xcat 文件名.xz

### 8.3 打包指令

* 打包与压缩：tar [-z|-j|-J] [cv] [-f 待创建的新文件名] filename...
  * tar -zcv -f etc.tar.gz /etc
* 查看文件名：tar [-z|-j|-J] [tv] [-f 既有的tar文件名] 
* 解压缩：tar [-z|-j|-J] [xv] [-f 既有的tar文件名] [-C 目录]
  * tar -zxv -f etc.tar.gz -C /tmp
* 仅解开单一文件：tar -jxv -f *.tar.bz2 待解开文件名
* 打包某目录，但不包含某文件：tar -jcv -f /root/system.tar.bz2 --exclude=/root/etc* --exclude=/root/system.tar.bz2 /etc /root

### 8.4 XFS文件系统备份

CentOS默认是XFS文件系统，其备份可以通过xfsdump和xfsrestore两个工具实现

### 8.5 光盘写入工具

* mkisofs：创建镜像文件
* cdrecord：光盘烧录工具

### 8.6 其他常见的压缩与备份工具

* dd if="input_file" of="output_file" bs="block_size" count="number"
* cpio：

## 第九章 vim程序编辑器

### 9.1 vi与vim

### 9.2 vi的使用

* 一般指令模式
  * 以vi打开文件后的默认模式，可以移动光标、删除字符或删除整行，也可以复制、粘贴
* 编辑模式
  * 在一般指令模式中是，通过“i, I, o, O, a, A, r, R”进入编辑模式，“ESC”退出编辑模式
* 命令行模式
  * 在一般指令模式中输入“: / ?”任意一个进入命令行模式
* .swap文件的处理，根据提示来即可

### 9.3 vim的额外功能

### 9.4 其他vim使用注意事项

## 第十章 认识与学习BASH

### 10.1 认识BASH这个Shell

* 只要能够操作应用程序的接口都能够称之为shell
* 系统合法的shell与/etc/shells
* bash的优点
  * 命令编辑能力(history)
  * 命令与文件补全功能（tab）
  * 命令别名设置功能(alias)
  * 工作控制、前景背景控制(job control, foreground, background)
  * 程序化脚本
  * 通用字符(Wildcard)
  * 
* type [-tpa] name
  * -t:
    * file: 表示为外部指令
    * alias: 
    * buildin
  * -p:
  * -a:

* ctrl + u/ ctrl + k：分别是从光标处向前删除指令串及向后删除指令串
* ctrl + a/ ctrl + e: 分别是让光标移动到整个指令串的最前面或最后面

### 10.2 Shell的变量功能

* 变量的取用与设置
  * echo：echo $variable, 如echo $PATH
  * 设置变量：=, 如myname=YIN
  * 变量设置规则：
    * 变量与变量内容以一个等号连接
    * 等号两边不能有空格
    * 变量内容若有空格需要使用引号
      * 双引号内的特殊字符，如$，保有原本特性，
      * 单引号内的特殊字符仅为一般字符
    * 可使用"\"转义特殊字符为普通字符
    * 反单引号"`"和$引用变量等
    * 扩增变量内容时，可用"$变量名称"或"${变量}"累加内容，如："PATH=$PATH:/home/bin"，或"PATH=${PATH}:/home/bin"，或'PATH="${PATH}:/home/bin'
    * 导出变量为环境变量："export PATH"
    * 取消变量：unset 变量名
* env: 查看环境变量
  * HOME:
  * SHELL
  * HISTSIZE
  * MALL
  * PATH
  * LANG
  * RANDOM
* set：查看所有变量，包括环境变量和bash中的变量
* export：将自定义变量转化为环境变量
* read [-pt] variable：从用户输入设置变量内容
* declare/type [-aixr] variable：声明一个变量
* array：读取方式$var[index]
* ulimit
* 删除变量内容
  * ${variable#/*local/bin:}等
* 取代变量内容
  * ${variable/old/new}

### 10.3 命令别名与历史命令

* alias: alias lm='ls -al | more'
* unalias
* history 
  * history n：显示最近n个记录
  * history -c：将目前shell中的所有history删除
  * ...
  * !number：执行第几条命令
  * !command：搜索command开头的指令并执行
  * !!：执行上一个命令

### 10.4 Bash Shell的操作环境

* 一般的指令执行顺序
  * 以相对/绝对路径执行指令
  * 由alias找到该指令执行
  * 由bash内置的builtin指令执行
  * 通过$PATH这个变量的顺序搜寻到的指令执行
* type -a [command]：查看命令的执行顺序
* bash的环境变量配置文件
  * login shell: 打开终端进行登录流程后的shell，/etc/profile ~/.bash_profile ~/.bash_login  ~/.profile
    * source 配置文件或文件名：读取文件，使得配置生效
  * non-login shell：不需要登录流程获取的shell（如在shell中再开的子shell）
    * ~/.bashrc
  * bash默认组合键
    * ctrl + c: 终止目前的命令
    * ctrl + d: 输入结束（EOF）
    * ctrl + m: enter
    * ctrl + s: 暂停屏幕输入
    * ctrl + q: 恢复屏幕输入
    * ctrl + u: 删除整列命令
    * ctrl + z: “暂停”目前命令
  
### 10.5 数据流重导向

* 1>  >
* 1>> >>
* 2> > 
* 2>> >>
* /dev/null重定向至此的数据会被删掉
* 标准与错误均重定向到一个文件：find /home -name .bashrc > list 2>&1
* 命令执行的判断依据
  * cmd; cmd：不考虑指令相关性的连续指令下达
  * cmd1 && cmd2：若cmd1执行完毕且正确($?=0)则开始执行cmd2
  * cmd1 || cmd2：若cmd1执行完毕且正确($?=0)则cmd2不执行
  * 逻辑判断：cmd1 && cmd2 || cmd3

### 10.5 管线命令(pipe)

* 管线命令：能够接受standard input的数据的命令
* 管线命令仅会处理stard output，忽略standard error output
* cut：按行处理信息
  * cut -d '分隔字符' -f fields
  * cut -c 字符区间
* grep：按行处理信息
  * grep [-acinv] [--color=auto] '搜索字符串' 文件名称
* 排序命令
  * sort [-fbMnrtuk] [file or stdin]
    * cat /etc/passwd | cat -t ':' -k 3 (-n)
  * uniq [-ic]
    * last | cut -d ' ' -f 1 | sort | uniq -c
  * wc [-lwn]
* 双重导向：tee
  * tee [-a] file
    * last | tee last.list | cut -d ' ' -f1
* 字符转换命令
  * tr [-ds] SET1
    * last | tr '[a-z]' '[A-Z]'
  * col [-xb]
  * join [-ti12] file1 file2
    * join -t ':' -1 4 /etc/passwd -2 3 /etc/group | head -n 3
  * paste [-d] file1 file2
    * paste /etc/passwd /etc/shadow
  * expand：将[tab]键转换为空格：expand [-t] file
* split
  * split [-bl] file PREFIX
  * cd /tmp; split -b 300k /etc/services services
  * cat services* >> servicesbak
  * ls -al / | split -l 10 - lsroot
* xargs：参数替换  xargs [-0epn] command
* -的用途
  * mkdir /tmp/homeback
  * tar -cvf - /home | tar -xvf - -C /tmp/homeback

## 第十一章 正则表达式与文件格式化处理

### 11.2 基础正则表达式

* 特殊符号与含义
  * [:alnum:]：代表英文大小写字符及数字，亦即 0-9, A-Z, a-z
  * [:alpha:]：代表任何英文大小写字符，亦即 A-Z, a-z
  * [:blank:]：代表空白键与 [Tab] 按键两者
  * [:cntrl:]：代表键盘上面的控制按键，亦即包括 CR, LF, Tab, Del.. 等等
  * [:digit:]：代表数字而已，亦即 0-9
  * [:graph:]：除了空白字符 （空白键与 [Tab] 按键） 外的其他所有按键
  * [:lower:]：代表小写字符，亦即 a-z
  * [:print:]：代表任何可以被打印出来的字符
  * [:punct:]：代表标点符号 （punctuation symbol），亦即：" ' ? ! ; : # $...
  * [:upper:]：代表标点符号 （punctuation symbol），亦即：" ' ? ! ; : # $...
  * [:space:]：代表标点符号 （punctuation symbol），亦即：" ' ? ! ; : # $...
  * [:xdigit:]：代表 16 进位的数字类型，因此包括： 0-9, A-F, a-f 的数字与字符
* grep [-A] [-B] [--color=auto] '搜索字符串' filename

|RE字符|意义与范例|
|-|-|
|^word|意义：待搜寻的字串（word）在行首！ grep -n '^#' regular_express.txt|
|word$|意义：待搜寻的字串（word）在行尾！ grep -n '!$' regular_express.txt
|.|意义：代表“一定有一个任意字符”的字符！
|\\|意义：跳脱字符，将特殊符号的特殊意义去除！
|*|意义：重复零个到无穷多个的前一个 RE 字符
[list]|意义：字符集合的 RE 字符，里面列出想要撷取的字符！
[n1-n2]|意义：字符集合的 RE 字符，里面列出想要撷取的字符范围！
[^list]|意义：字符集合的 RE 字符，里面列出不要的字串或范围！
\{n,m\}|意义：连续 n 到 m 个的“前一个 RE 字符”意义：若为 \{n\} 则是连续 n 个的前一个 RE 字符，

* sed [-nefr] [动作]
  * 动作说明：[n1, [n2]]function
    * a: 新增
    * c: 取代
    * d: 删除
    * i: 插入
    * p: 打印
    * s: 取代
  * nl /etc/passwd | sed '2,5d'
  * nl /etc/passwd | sed '2a Drink tea or ...\
  drink tea
  * nl /etc/passed | sed '2,5c No 2-5 number'
  * cat /etc/man_db.conf | grep 'MAN' | sed 's/#.*$//g'
  * sed -i 's/\.$/\!/g' file.txt

### 11.3 延伸正则表达式

* egrep/ grep -E

RE字符|意义
-|-
+|意义：重复“一个或一个以上”的前一个 RE 字符
?|意义：“零个或一个”的前一个 RE 字符
\||意义：用或（ or ）的方式找出数个字串
()|意义：找出“群组”字串
()+|意义：多个重复群组的判别

### 11.4 文件格式化与相关处理

* printf
* awk：数据处理工具，比较倾向于一行当中分成数个“字
段”来处理
  * awk '条件类型1{动作1} 条件类型2{动作2} ...' filename
  * awk的内置变量(引用时不需要在前面加$)
    * NF: 每一行 （$0） 拥有的字段总数
    * NR: 目前 awk 所处理的是“第几行”数据
    * FS: 目前的分隔字符，默认是空白键
  * awk的逻辑运算字符
    * >
    * <
    * \>=
    * <=
    * ==
    * ！=
  * cat /etc/passwd | awk 'BEGIN {FS=":"} $3 < 10 {print $1 "\t" $3}'
  * cat pay.txt | \
  \> awk 'NR==1{printf "%10s %10s %10s %10s %10s\n",$1,$2,$3,$4,"Total" }
  \> NR>=2{total = $2 + $3 + $4
  \> printf "%10s %10d %10d %10d %10.2f\n", $1, $2, $3, $4, total}'
    * 在 {} 内的动作，如果有需要多个指令辅助时，可利用分号“;”间隔，或者直接以
[Enter] 按键来隔开每个指令
    * 与 bash shell 的变量不同，在 awk 当中，变量可以直接使用，不需加上 $ 符号
* diff [-bBi] from-file to-file
  * 以行为单位
  * 一般是用在 ASCII 纯文本文件
  * 通常是用在同一的文件（或软件）的新旧版本差异上
* cmp [-l] file1 file2
  * 主要利用“字节”单位去比对
* patch 
  * diff -Naur passwd.old passwd.new > passwd.patch
  * patch -p0 < passwd.patch
  * patch -R -p0 < passwd.patch
* pr

## 第十二章 学习Shell Scripts

### 12.1 什么是Shell Scripts

* shell script:
  * 指令的执行是从上而下、从左而右的分析与执行
  * 指令、选项与参数间的多个空白都会被忽略掉
  * 空白行也将被忽略掉，并且 [tab] 按键所推开的空白同样视为空白键
  *  如果读取到一个 Enter 符号 （CR） ，就尝试开始执行该行 （或该串） 命令
  * 至于如果一行的内容太多，则可以使用“ \[Enter] ”来延伸至下一行
  * “ # ”可做为注解！任何加在 # 后面的数据将全部被视为注解文字而被忽略
* shell script的执行方式：
  * 直接指令下达（文件需要具备可执行权限）
  * 以bash程序来执行（如：sh demo.sh）
* shell script文件说明
  * 第1行：#!/bin/bash
  * 添加注释说明程序功能
  * 添加注释作为更改记录
  * 设置环境变量并导出，如PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin  （下一行）export PATH
  * 程序返回值，如 exit 0

### 12.2 简单shell练习

* read指令使用：read -p "demo" variable
* echo -e的作用
* 推荐方式：var=$((运算内容))
* script执行方式的差异
  * 直接执行脚本（通过路径，或bash）：使用一个新的bash执行，执行换后会退出，各项变量或动作不会传回到父程序中
  * source 脚本：在父程序中执行，故变量还在

### 12.3 善用判断式

* test指令: test -f ${filename} && filetype="regular file"
  * test常用标志与意义
* 判断符号[]：[ -z "${HOME}" ] ; echo $?
  * 中括号内的内容用空格隔开
  * 括号内的变量最好用双引号、
  * 常数用单引号或双引号
* 默认变量：
  * $0: /path/to/scriptname 
  * $1: opt1
  * $2: opt2
  * $3: opt3
  * $#：输入参数的个数
  * $@: 代表所有的参数,""$1", "$2", ..."
  * $*: 代表""$1"c"$2"c..."
  * shift命令


### 12.4 条件判断式

if [条件判断式]; then
  当条件判断式成立时，执行
elif [...]; then
  ...
fi


case $变量名称 in
  "第一个变量内容")
  程序段
  ;;
  "第二个变量内容")
  程序段
  ;;
  *)
  程序段
  exit 1
  ;;
esac


function fname() {
  程序段
}

### 12.5 循环

while [ condition ]
do
 程序段
done

until [ condition ]
do 
  程序段
done

for var in con1 con2 con3 ...
do 
  程序段
done

for ((初始值; 限制值; 执行步阶))
do
  程序段
done

### 12.6 shell script的追踪与debug

sh [-nvx] scripts.sh
* -n: 不要执行script，仅查询语法的问题
* -v：再执行script前，先将scripts的内容输出到屏幕上
* -x：将使用到的script内容显示到屏幕上

## 第十二章 Linux账号管理与ACL权限设置

### 13.1 Linux账号与群组

使用者识别码：UID  GID
* /etc/passwd  /etc/group文件中有记录，与账号对应，实际计算机是以UID与GID区分的
* id 账号名   查看账号对应的使用者识别码信息

/etc/passwd文件结构
* 一行代表一个账号
* 有很多诸如bin之类的系统账号，不要动
* 账号名称:密码(x):UID:GID:使用者信息说明:主文件夹:Shell

/etc/shodow文件结构
* 账号名称:密码:最近更改密码时间:密码不可更改时长:密码需要重新变更的时长:密码需要变更前多久提醒:密码过期后的宽限时间:账号失效日期:保留

修改密码
* root用户通过passwd修改一般用户密码
* root密码的修改

查询密码的hash算法：authconfig --test | grep hashing

群组相关：

* /etc/group:  群组名称:群组密码:GID:此群组支持的账号名称
* groups: 查看支持的群组与有效群组
* newgrp: 有效群组的切换
* root用户通过usermod将其他用户加入群组
* 群组管理员  /etc/gshadow   群组名称:密码栏:群组管理员账号:该群组支持的所属账号

### 13.2 账号管理

新增与移除用户

* useradd [-u UID] [-g 初始群组] [-G 次要群组] [-mM] [-c 说明栏] [-d 主文件夹绝对路径] [-s shell] 使用者账号名
* passwd [--stdin] [账号名称]
* chage [-ldEImMW] [账号名]   (密码参数显示功能)
* usermod [-cdegGlsuLU] [username]  (调整用户信息)
* userdel [-r] [username]
* id
* chsh [ls]

新增与移除群组

* groupadd [-g gid] [-r] 群组名称
* groupmod [-g gid] [-n group_name] 群组名
* groupdel [groupname]
* gpasswd groupname

### 13.3 主机的精细权限规划：ACL的使用

ACL：Access Control List

提供针对传统owner, group, others的read, write, execute的权限之外的更细致的权限控制，可针对单一使用者，单一文件或目录来进行r, w, x的权限规范

* 使用者：可以针对使用者来设置权限
* 群组：针对群组为对象来设置权限
* 默认属性：还可以针对在该项目下创建新文件/目录时，规范新数据的默认权限

* setfacl -[-bkRd] [{-m|-x} acl参数] 目标文件名
  * 指定用户权限设置：seftacl -m u:vbird1:rx acl_test1
  * 单一群组设置：seftacl -m g:mygroup1:rx acl_test1
  * 有效权限设置：setfacl -m m:r acl_test1  (针对mask的设置)
  * 设置ACL权限继承：setfacl -m d:u:myuser1:rx 目录名
* getfacl filename

### 13.4 使用者身份切换

* su [-lm] [-c 指令] [username]
* sudo [-b] [-u 新使用者账号]
* 使用visudo修改/etc/sudoers文件给其他用户添加sudo权限
  * vbird1 ALL=(ALL) ALL  (使用者账号  登录者的来源主机=(可切换的身份) 可下达的指令)
  * 设置免密使用sudo：vbird1 ALL=(ALL)  NOPASSWD: ALL

### 13.5 使用者的特殊shell与PAM模块

有些账号是不能通过shell或bash进行登录的，如系统账号，在/etc/passwd文件中，其登录时的shell项为/sbin/nologin

linux中账号的权限管理是由PAM模块提供的，可自行调用该接口完成一些功能

### 13.6 Linux主机上的使用者信息传递

查询使用者：w, who, last, lastlog

与使用者对谈：write, mesg, wall, mail

### 13.7 CentOS环境下大量创建账号的方法

账号相关的检查工具：pwck, pwconv, pwunconv, chpasswd

批量创建账号的例子

