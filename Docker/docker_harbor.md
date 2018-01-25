# docker_harbor

```
Harbor 是 Vmwar 公司开源的 企业级的 Docker Registry 管理项目

它主要 提供 Dcoker Registry 管理UI，可基于角色访问控制, AD/LDAP 集成，日志审核等功能，完全的支持中文。

Harbor 的所有组件都在 Dcoker 中部署，所以 Harbor 可使用 Docker Compose 快速部署。

注： 由于 Harbor 是基于 Docker Registry V2 版本，所以 docker 版本必须 > = 1.10.0 docker-compose >= 1.6.0

开源项目地址：https://github.com/vmware/harbor
```

###harbor安装
- 下载harbor
>https://github.com/vmware/harbor/releases
- harbor需要安装docker和docker-compose才能使用
```
yum install python-pip

pip install --upgrade pip

pip install docker-compose
```
- 安装online版本的harbor
```
wget https://github.com/vmware/harbor/releases/download/v1.1.2/harbor-online-installer-v1.1.2.tgz
```
- 解压
```
tar xvf harbor-online-installer-v1.1.2.tgz
```
- 修改配置[harbor.cfg]
```
hostname:服务器的名称，如果访问UI和注册服务，需要通过这个。可以是IP地址(192.168.0.209)，或者是完整的域名（reg.youdomain.com）。不要使用localhost或者127.0.0.1，因为服务需要被其他的机器访问。
db_password:mysql数据的密码。
```
- 执行
```
sudo ./prepare

docker-compose up -d
```







 