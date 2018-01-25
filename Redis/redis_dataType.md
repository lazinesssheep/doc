# redis-datatype
```$xslt
Redis支持五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)。
```

#### String（字符串）
 - 使用
 ```$xslt
        SET hello "world"   //设置 key value
        OK
        GET hello           //获取 key
        "world"
```
 - 注意
 ```$xslt
        1. 一个键最大能存储512MB
        2. 可以包含任何数据。比如jpg图片或者序列化的对象
```
#### Hash（哈希）
 - 单独设置 - key filed value
```$xslt
        hset person name zhangsan    //设置姓名
        1
        hset person age 20           //设置年龄
        1
        hgetall person               //获取所有数据
        name
        zhangsan
        age
        20
        hkeys person                 //获取所有的key
        name
        age
        hvals person                 //获取所有的value
        zhangsan
        20
```
 - 批量设置 - key filed value filed value filed value ......
```$xslt
        hmset person name zhangsan age 20
        OK
        hgetall person
        name
        zhangsan
        age
        20
```
 - 删除 
 ```$xslt
    hdel
```
####总结
```$xslt
    1. 永远只有一个键，一个值，这个键永远都是字符串对象
```