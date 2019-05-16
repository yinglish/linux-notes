# linux命令记录

## CentOS对外开发端口

比如在虚拟机中启动了服务，在宿主机上无法访问，有时候原因是没有开放对应的端口，需要在虚拟机中开放对应的端口

* 查看对外开放的端口状态
    * 查询已开放的端口：netstat -anp
    * 查询指定端口的开放情况：firewall-cmd --query-port=80/tcp
* 查看防火墙状态
    * 查看防火墙状态：systemctl status firewalld
    * 开启防火墙：systemctl start firewalld
    * 关闭防火墙：systemctl stop firewalld
    * 开启防火墙：service firewalld start
    * 遇到无法开启：先：systemctl unmask firewalld.service 后：systemctl start firewalld.service
* 对外开放端口
    * 添加指定需要开放的端口：firewall-cmd --add-port=123/tcp --permanent
    * 重载入添加的端口：firewall-cmd --reload
    * firewall-cmd --query-port=123/tcp
* 移除指定端口：firewall-cmd --permanent --remove-port=123/tcp