# docker-repo

```$xslt
类似Maven的私有仓库，docker也可以搭建镜像库，可以更快的下载镜像，管理个性化镜像，这里介绍一下centos中私有仓库的搭建。
```
##下载registry镜像
```
     docker pull registry
```

##防火墙添加运行5000端口
```
     iptables -I INPUT 1 -p tcp --dport 5000 -j ACCEPT
```

##通过该镜像启动一个容器
```
    docker run -d -p 5000:5000 --privileged=true -v /opt/registry:/tmp/registry registry 
```
- 参数说明： 
> -v /opt/registry:/tmp/registry  ：默认情况下，会将仓库存放于容器内的/tmp/registry目录下，指定本地目录挂载到容器 
–privileged=true ：CentOS7中的安全模块selinux把权限禁掉了，参数给容器加特权，不加上传镜像会报权限错误(OSError:
##客户端上传镜像
- 修改/etc/sysconfig/docker（Ubuntu下配置文件地址为：/etc/init/docker.conf）
```
    OPTIONS='--insecure-registry 192.168.0.179:5000'    #CentOS 7系统
    other_args='--insecure-registry 192.168.0.179:5000' #CentOS 6系统
```
- 客户端添加私有仓库地址
```
    ADD_REGISTRY='--add-registry 192.168.0.179:5000'
```
##上传镜像至仓库
```
    docker push 192.168.1.107:5000/test1
```
##使用仓库中的镜像
```
    docker pull 192.168.1.107:5000/test1
```
##查看镜像
```
    curl -XGET http://registry:5000/v2/_catalog
    curl -XGET http://registry:5000/v2/image_name/tags/list
```



 