# ss

```
centos上需要下载国外的文件，也需要翻墙，下面介绍一下如何在centos中使用代理。
```

## 安装组件
和服务器端安装步骤一样
```
yum groupinstall "Development Tools"  
yum install m2crypto python-setuptools  
easy_install pip  
pip install shadowsocks  
```

## 配置服务器参数
```
vi /etc/shadowsocks.json
```
```
{  
 "server": "0.0.0.0",  
 "server_port": 7777,  
 "password": "pwd",  
 "method": "aes-256-cfb",  
 "local_address":"127.0.0.1",  
 "local_port":1080  
 }
```
>注意上面的配置文件，如果你是服务端提供代理的，server的值需要写0.0.0.0 
 如果你是使用代理的客户端，server值需要服务器ip。

## 服务端启动ss服务器命令 
```
ssserver -c /etc/shadowsocks.json  
```
```
sslocal  -c /etc/shadowsocks.json 
```

## 安装privoxy
至此，我们的ss服务已经正常启动，下面要做的就是需要将全局http代理转发到socks5代理。
```
yum install epel-release  
yum install -y privoxy  
//删除多安装的无用repo  
rm /etc/yum.repos.d/epel-testing.repo  
```
- 修改文件
```
vi /etc/privoxy/config 
```
- 增加
```
forward-socks5t   /               127.0.0.1:1080 .  
```
- 然后搜索listen-address，取消注释的ip地址，或者直接新加下面的信息： 
```
listen-address  127.0.0.1:8118  
```
- 完事之后，vim ~/.bashrc，加入下面的内容 
```
export http_proxy=http://127.0.0.1:8118  
export https_proxy=http://127.0.0.1:8118  
export ftp_proxy=http://127.0.0.1:8118  
```
- 然后执行
```
source ~/bashrc
```
- 最后重启privoxy即可 
```
systemctl restart privoxy.serivce 
```
- 测试一下
```
curl www.google.com
```
- 注意如果需要，我们可以完全关闭防火墙或者仅仅对指定端口开放即可
```
firewall-cmd --zone=public --add-port=8888/tcp --permanent  
systemctl restart firewalld.service 
```
>当然，如果我们想让maven下载编译的时候也支持代理是需要配置的,否则默认是不会使用的,
找到conf/settings.xml文件取消注释稍作修改即可：
```
<proxy>    
  <id>optional</id>    
  <active>true</active>    
  <protocol>http</protocol>    
  <username></username>    
  <password></password>    
  <host>127.0.0.1</host>    
  <port>8087</port>    
  <nonProxyHosts>localhost|127.0.0.1</nonProxyHosts>    
</proxy>   
```
 