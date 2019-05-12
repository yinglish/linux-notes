# 菜鸟教程

Linux教程

### Linux系统启动过程

分为5个阶段：
* 内核的引导
* 运行init: init程序的类型
    * SysV: init, CentOS 5之前，配置文件： /etc/inittab
    * Upstart：init, CentOS 6, 配置文件：/etc/initab, /etc/init/*.conf
    * Systemd: systemd, CentOS 7, 配置文件：/usr/lib/systemd/system, /etc/systemd/system
* 系统初始化
* 建立终端
* 用户登录系统

#### 内核引导

通电 -> BIOS开机自检 -> BIOS中设置的启动设这启动（一般是硬盘） -> 操作系统接管硬件 -> 进入/boot目录读取内核文件

#### 运行init

init进程是所有进程的起点，init程序首先读取配置文件/etc/inittab（不同版本系统不一样）

#### 运行级别

许多程序都需要在开机时启动，Windows中叫做“服务”(service)， Linux中叫做“守护进程”(daemon)，init的一大任务就是要启动这些程序。

不同的场合需要启动不同的程序，所有分场合，分配不同的开机启动程序，及“运行级别”(runlevel)：
* 运行级别0：系统停机状态，系统默认不能设为0，否则不能正常启动
* 运行级别1：但用户工作状态，root权限，用于系统维护，禁止远程登录
* 运行级别2：多用户状态（没有NFS）
* 运行级别3：完全的多用户状态（有NFS），登录后进入控制台命令行模式
* 运行级别4：系统未使用，保留
* 运行级别5：X11控制台，登录后进入图形GUI模式
* 运行级别6：系统正常关机并重启，默认不能设为6，否则不能正常启动

#### 系统初始化

init的配置文件中，有执行脚本的程序，这个脚本位于目录/etc/rc.d中，其中的不同的文件代表不同的运行级别要执行的脚本。

#### 建立终端

rc执行完毕后，返回init，系统已基本设置好，守护进程也已经启动，init会打开6个终端，切换方式：ctrl + alt + f1 - f6

#### 用户登录

三种方式：
* 命令行
* ssh登录
* 图形界面登录

#### Linux关机

正确的关机流程：sync -> shutdown -> reboot -> halt

常用的关机指令及说明：
* sync: 数据同步到硬盘
* shutdown: 关机指令
* shutdown -h 10 'text' 10分钟后关机
* shutdown -h now 马上关机
* shutdown -h 20:24 指定时间关机
* shutdown -h +10 10分钟后关机
* shutdown -r now 立马重启
* shutdown -r +10 10分钟后重启
* reboot 重启，等同于shutdown -r now, init 6
* halt 关闭系统，等同于shutdown -h now 和poweroff, init 0

### Linux系统目录结构

查看根目录：ls /

* /bin: 存放着最经常使用的命令
* /boot: 存放启动Linux时使用的核心文件，包括连接文件和镜像文件
* /dev: Device的缩写，存放Linux的外部设备，Linux中访问设备和文件的方式时一样的
* /etc: 存放系统管理所需要的配置文件和子目录
* /home: 用户的主目录
* /lib: 存放系统最基本的动态连接共享库
* /lost+fount: 一般为空，非法关机后会存放文件
* /media: 自动识别的设备如U盘、光驱等等，识别完成后加载在此
* /mnt: 为了让用户临时加载别的文件系统，如光驱
* /opt: 主机额外安装软件拜访的目录，比如安装oracle数据库
* /proc: 虚拟目录，系统内存的映射，可以通过访问这个目录来获取系统信息，这个目录的内容不在硬盘上，而是内存中，可以直接修改里面的莫某些文件
* /root: 系统管理员主目录
* /sbin: s代表Super User，这里存放的是系统管理员使用的系统管理程序
* /selinux: Redhat/CentOS特有的目录，是一个安全机制
* /srv：存放一些服务启动后需要提取的数据
* /sys: 
* /tmp: 用来存放临时文件
* /usr: 用户的很多应用程序和文件都放在这个目录下，类似于windows的program files目录
* /usr/bin: 系统用户使用的应用程序
* /usr/sbin: 超级用户使用的比较高级的管理程序和系统守护程序
* /usr/src: 内核源代码默认的目录
* /var: 不断扩充的东西，如日志
* /run: 临时文件系统，存储系统启动以来的信息

### 忘记密码的解决办法

忘记root用户密码怎么办

进入单用户模式更改

### Linux远程登录

服务器一般在机房，需要远程登录

ssh登录，端口号默认为22

windows常用的工具有：SecureCRT, Putty, SSH Secure Shell等

### Linux文件基本属性

Linux是多用户系统，不同的用户处于不同的地位，拥有不同的权限，为了系统安全，需要对不同用户访问同一文件的权限做出限定

文件类型：
* d: 目录
* -: 文件
* l: 链接文件
* b: 装置文件里面的可供储存的接口设备
* c: 则表示为装置文件里面的串行设备，如键盘、鼠标

#### 更改文件属性

1 chgrp: 更改文件属组   chgrp [-R] 属组名  文件名

2 chown: 更改文件属主，也可以同时更改文件属组  
* chown [-R] 属主名 文件名
* chown [-R] 属主名：属组名 文件名

3 chmod: 更改文件9个属性

两种设置方法，一种是数字，一种是符号

* chmod [-R] xyz 文件或目录
* chmod [-R] o=rwx,g=rwx,o=rwx,a=rwx
* chmod a+w

### 文件与目录管理

#### 处理目录常用命令

* ls: 列出目录
    * ls [-aAdfFhilnrRSt] 目录名称
    * ls [--color={never, auto, always}] 目录名称
    * ls [--full-time] 目录名称
* cd: 切换目录
* pwd: 显示当前目录
    * [-P]显示确实路径，而不是链接路径
* mkdir: 创建一个空目录
    * -m 配置文件的权限，直接配置，不需要关心默认权限(umask)的脸色
    * -p 将所需的目录递归的创建起来
* rmdir: 删除一个空目录
    * -p 连同上一级“空”目录也一起删除
* cp: 复制文件或目录
    * cp [-adfilprsu] source destination
    * cp [options] source1 source2 source3 ... directory
* rm: 移除文件或目录
    * -[fir] 文件或目录
* mv: 移动文件与目录，或修改文件与目录的名称
    * -[fiu] source destination
    * [options] source1, source2, source3 ... directory

#### 文件内容查看

* cat
    * [-AbEnTv] 文件
* tac
* nl
    * nl [-bnw] 文件
* more
* less
* head
    * head [-n number] 文件
* tail
    * tail [-n number] 文件
    * -f 持续侦测后面所接文档，按下ctrl + c才会结束tail的侦测


### 用户和用户管理

多用户多任务分时操作系统

* 用户账号的添加、删除与修改
* 用户口令的管理
* 用户组的管理

#### 系统用户账号的管理

* useradd 选项 用户名
    * -c 指定一段注释性描述
    * -d 指定用户主目录，如果不存在，同时使用-m选项可创建
    * -g 用户组
    * -G 用户组，指定用户所属的附加组
    * -s Shell文件 指定用户的登录shell
    * -u 用户号 指定用户的用户号
* userdel 选项 用户名
    * -r 把主目录一同删除
* usermod 选项 用户名
    * -c, -d, -m, -g, -G, -s, -u, -o
* 用户口令管理：用户刚创建时没有口令，被系统锁定，必须指定指令后才可以使用
    * passwd 选项 用户名
        * -l 锁定口令，即禁用账号
        * -u 口令解锁
        * -d 使账号无口令
        * -f 强迫用户下次登录时修改口令
    * 指定空口令：passwd -d user

#### 系统用户组的管理

* groupadd 选项 用户组
    * -g GID指定新用户组的组标识号
    * -o 一般与-g选项同时使用，表示新用户组的GID可以与系统已有的GID相同
* groupdel 用户组
* groupmod 选项 用户组
    * -g
    * -o
    * -n 新用户组 将用户组的名字改为新名字
* 用户属于多个用户组时可以切换用户组：newgrp 组名

#### 与用户账号有关的系统文件

* /etc/passwd 最重要的一个文件，每个用户都有一个对应的记录行
    * 用户名：口令：用户标识号：注释性描述：主目录：登录shell
* 伪用户

* 用户组的所有相关信息都存放在/etc/group文件中

#### 批量添加用户

* 编辑文本用户文件：安装passwd文件的格式
* 以root身份执行命令/usr/sbin/newusers：newusers < users.txt
* 执行命令/usr/sbin/pwunconv
* 编辑每个用户的密码对照文件：passwd.txt
* 以root身份执行命令：/usr/sbin/chpasswd < passwd.txt>
* 确定密码敬编辑写入/etc/passwd的密码栏后：pwconv

### 磁盘管理

* df：列出文件系统的整体磁盘使用量
    * df [-ahikHTm] [目录或文件名]
* du：检查磁盘空间使用量
    * du [-ahskm] 文件或目录名称
* fdisk：用于磁盘分区
    * fdisk [-l] 装置名称
* 格式化磁盘：mkfs [-t 文件系统格式] 装置文件名

#### 磁盘检验

* fsck (file system check)用来检查和维护不一致的文件系统：fsck [-t 文件系统] [-ACay] 装置名称

#### 磁盘挂载与卸除

* mount [-t 文件系统] [-L Label名] [-o 额外选项] [-n] 装置文件名 挂在点
* umount [-fn] 装置文件名或挂载点

### vi/vim

### yum命令

yum (Yellow dog Updater, Modified)是一个在Fedora和RedHat以及SUSE中的Shell前端软件包管理器

自动从指定的服务器下载rpm包并安装，自动处理依赖关系，并且一次安装所有依赖的包

* yum [options] [command] [package ...]

#### 常用命令

* 列出所有可更新的软件清单命令：yum check-update
* 更新所有软件命令：yum update
* 仅安装指定的软件命令：yum install <package_name>
* 仅更新指定的软件命令：yum update <package_name>
* 列出所有可安装软件清单：yum list
* 删除软件包命令：yum remove <package_name>
* 查找软件包命令：yum search <package_name>
* 清除缓存命令：
    * yum clean packages
    * yum clean headers
    * yum clean oldheaders
    * yum clean, yum clean all 

#### 更改yum源

* 备份：mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
* 下载对应版本的repo文件：wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
* mv CentOS7-Base-163.repo CentOS-Base.repo
* 运行命令生成缓存：yum clean all     yum makecache

### Shell教程

既是一种命令语言，又是一种程序设计语言