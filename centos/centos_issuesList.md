# centos_issuesList

```
记录centos各个方面比较重要的坑
```

--------------------------------------------
##yum install提示 “没有可用软件包 ***”
- 情景：这是我在执行**yum install python-pip**遇到的问题
- 原因：查阅资料以后，原来是因为CentOS官方的源有些时候滞后导致的
- 解决：

可以用fedora社区打造的EPEL(http://fedoraproject.org/wiki/EPEL)来进行安装

首先执行
```
     sudo yum -y install epel-release
```
再去执行
```
    sudo yum -y install python-pip
```
--------------------------------------------

##yum update
Linux升级命令有两个分别是yum upgrade和yum update, 这个两个命令是有区别的:
```
    # 升级所有包同时也升级软件和系统内核
    yum -y update
```
```
    # 只升级所有包，不升级软件和系统内核
    yum -y upgrade
```
- 升级前
```
    系统版本：  centos5.5
    内核版本：  2.6.18-194.el5
```
- yum -y upgrade    升级后
```
    系统版本：    centos5.7
    内核版本：  2.6.18-194.el5
```
- yum -y update    升级后
```
    系统版本：    centos5.7
    内核版本：    2.6.18-238.el5
```

--------------------------------------------

##修改nameserver 
```
    vi /etc/resolv.conf
```

--------------------------------------------





 