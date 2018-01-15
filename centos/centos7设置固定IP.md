## CentOS7 设置局域网固定IP

- 我的问题
>在VirtualBox中新装的centos7竟然不能自动联网，修改“/etc/sysconfig/network-scripts/ifcfg-enp0s3”中的ONBOOT=yes之后，
 可以上网，但是内网地址竟然是10.0.2.15，主机都不好连，尝试固定IP。
- 其他原因
>在局域网内PC通常都是采用自动获取IP的方式从路由器拿到局域网IP的，每次PC启动后分配到的局域网IP都不一定相同。
 但是出于某些特殊的需求，例如要在局域网内做端口映射，需要将PC设置成使用固定的局域网IP，即使PC重启了，
 其局域网IP仍然不变。在Windows下这个设置的过程很简单。那么在Linux下该如何设置呢？
- 下面以CentOS7为例，介绍下Linux系统设置局域网固定IP的方法。

###  设置IP、子网掩码和网关
同样是编辑“/etc/sysconfig/network-scripts/ifcfg-enp0s3”,在文件末尾加入以下3行：
```
IPADDR=192.168.2.106
NETMASK=255.255.252.0
GATEWAY=192.168.1.1
```

### 设置开机启动网络
继续修改/etc/sysconfig/network-scripts/ifcfg-p4p1文件，将 ONBOOT 选项改为yes：
```
ONBOOT=yes
```

### 设置NameServer
用文本编辑器打开 /etc/resolve.cnf 文件，将其中内容用##注释掉，增加以下行：
```
nameserver 192.168.1.1
```
_注：_
_如果PC已经通过自动获取IP的方式能够上网，那么 /etc/resolve.cnf 文件中已经是正确的配置了，因此不需要修改。但是如果设置固定IP后发现不能上网，应该检查下该文件中nameserver设置是否正确。_

### 重启网络
打开终端，输入以下命令重启网络：
```
sudo service network restart
```

###  测试网络
如果可以 ping 通，说明网络已经通了，可以正常上网了。
```
ping www.baidu.com
```
_注：
上述设置过程中的 IPADDR (IP地址)、NETMASK (子网掩码)、GATEWAY （网关）可以在设置前通过 ifconfig 命令查询。_