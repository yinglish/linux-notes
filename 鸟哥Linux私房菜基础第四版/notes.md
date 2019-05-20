# 基础学习篇

## 第零章 计算机概论

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
