# 基础学习篇

## 第零章 计算机概论


系统参数（如网卡、显卡是否启动）记录在主板上CMOS芯片上，需要有电（故有电源）

BIOS是写死到主板上的一个内存芯片中的程序（ROM），以前是不可更改，但是现在通常是写入类似闪存或EEPROM中。

显卡与屏幕连接的格式：D-Sub (VGA端子) 模拟信号；DVI; HDMI；Display port

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

MBR，磁盘的第一个扇区，记录磁盘的重要信息；新的磁盘分区格式GPT（GUID partition table）

MBR分区表格与限制
* 主要开机记录区（Master Boot Record, MBR）：可以安装开机管理程序的地方，有446 Bytes
* 分区表(partition table)：记录整颗硬盘分区的状态，有64Bytes，所以只能记录四个分区(Primary分区或Extended分区，Extended最多只能有一个，但可以利用延伸分区继续分下去，即逻辑分区)

### BIOS与UEFI开机检测程序

* BIOS搭配MBR/GPT的开机流程
    * CMOS：记录各项硬件参数嵌入在主板上的储存器
    * BIOS：写入到主板上的一个固件，开机主动执行的固件，会认识第一个可开机的设备
    * MBR：第一个可开机设备的第一个扇区内的主要开机记录区块，内含开机管理程序
    * 开机管理程序(boot loader)：一个可读取核心文件来执行的软件
        * 提供菜单：使用者可以选择不同的开机项目
        * 载入核心文件：直接指向真正可开机的程序区段来开始操作系统
        * 转交其他loader：将开机管理功能转交给其他的loader负责
    * 核心文件：开始操作系统的功能
    * 说明：BIOS也能够从GPT格式的LBA0的与MBR相容区块读取第一阶段的开机管理程序码，如果开机管理程序能够认识GPT的话，那么也可以开机成功，否则开机失败

* UEFI BIOS 搭配GPT开机的流程
    * 也称UEFI为UEFI BIOS

## 第三章 安装CentOS7.x

## 第四章 首次登录与线上求助



* 显示的语言的更改
  * 查看：locale
  * 更改：LANG=en_US.UTF-8  （等号两端没有空格）；export LC_ALL=en_US.UTF-8
* date指定格式：date +%Y%m%d%H%M
* cal [month] [year]
* 简单计算器：bc
* 命令补全和文件补全：[tab]键
* ctrl+c：中断目前的程序；ctrl+d：键盘输入结束/exit
* 连续两个[tab][tab]的作用：文件查看，命令补全
* help与man：使用空格键即可完成翻页；输入/word进行关键字搜索（man命令）；以前用过的命令用help查看参数，否则最好通过man进行学习
* man -f = whatis/man -k = apropos
* 数据同步到硬盘：sync
* shutdown [-khrc] [time] [warning]  reboot, halt, poweroff
* 使用反斜杠`\`是命令连续到下一行
* 正确的关机步骤：
  * 谁在线：`who`
  * 网络的连线状态：`netstat -a`
  * 背景执行的程序：`ps -aux`
  * 关机相关指令：`shutdown`, `reboot`, `halt`, `poweroff`
