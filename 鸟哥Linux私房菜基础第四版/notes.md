# 基础学习篇

## 第零章 计算机概论


系统参数（如网卡、显卡是否启动）记录在主板上CMOS芯片上，需要点电（故有电源）

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
