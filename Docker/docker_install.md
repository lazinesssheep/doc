# docker-install

```$xslt
install
```
##增加docker用户
```
     sudo groupadd docker
     sudo useradd -g docker docker
```

##增加centos7 的国内源
```
     wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
     yum makecache
```
##更新系统
```
    sudo yum update
```
##安装docker
```
    yum install docker
```
##启动docker
```
    (1)启动，systemctl start docker.service
    (2)开机启动，systemctl enable docker.service
    (3)帮助，docker --help
    (4)概要信息，docker info
    (5)镜像查看，docker images
    (6)容器查看，即进程查看，docker ps -a
```



 