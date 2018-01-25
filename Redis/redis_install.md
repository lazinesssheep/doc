# redis-install

```$xslt
install
```

##Window 下安装
 - 下载地址
 ```$xslt
        - Redis：        https://github.com/MicrosoftArchive/redis/releases （Redis-x64-3.2.100.zip）
        - RedisClient：  http://rj.baidu.com/soft/detail/29740.html?ald
        - FastoRedis：   https://sourceforge.net/projects/fastoredis/files/
```
 - 解压文件夹
 ```$xslt
        - redis.windows.conf    是redis的配置文件
        - redis-server.exe      服务器端
        - redis-cli             命令行客户端
        - redis-benchmark：     Redis性能测试工具，测试Redis在你的系统及你的配置下的读写性能
 ```
 - cmd 窗口进入此文件夹（发现只有cmd窗口可以操作）
 ```
        - 执行 redis-server.exe redis.windows.conf
 ```
 - redis相关配置
  ```$xslt
         - port         端口号，例如6379
         - bind         实例绑定的访问地址127.0.0.1
         - requirepass  访问的密码
         - maxheap      记得把这个配置节点打开，否者redis 服务无法启动。例如maxheap 1024000000
         - timeout      请求超时时间
         - logfile      log文件位置
         - databases    开启数据库的数量
         - dbfilename   数据快照文件名（只是文件名，不包括目录）
 ```
  - 连接服务 
  ```$xslt
         - 执行  redis-cli.exe -h 127.0.0.1 -p 6379
         - 参数分别为host、port,如果设置了密码，则必须要加上-a 123456,123456为登录密码。否则会提示没有权限登录系统
 ```
  - 环境变量设置(提示redis-server.exe找不到时的解决办法)
  ```$xslt
         - REDIS_HOME   F:\Redis-x64-3.2.100
         - Path         REDIS_HOME 
```
##Linux 下安装

 