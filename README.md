# 消息转发接口文档
## 目录
* 1、消息请求 
  * 1.1 消息转发邮箱或者Ihaier
    * 1.1.1 消息转发邮箱
    * 1.1.2 消息转发Ihaier
    * 1.1.3 消息既转发Ihaier又转发邮箱
* 2、整体测试请求 
  * 2.1 整体测试流程 
    * 2.1.1 向Kafka发送消息  
    * 2.1.2 得到告警信息列表
  
### 1. 消息请求
消息请求底层是http协议，采用rest风格url作为服务提供。主要包括当前消息转发给邮箱还是Ihaier。

### 1.1 当前消息请求
提供当前正在发生的消息转发接口。

### 1.1.1 当前消息请求转发邮箱
当前告警信息转发邮箱，具体请求格式如下：
 
```
//subject:消息主题,targets:目标工号,content:消息内容，messageType：消息类型(1表示既发送邮箱也发送Ihaier,2表示只发送邮箱，3表示只发送Ihaier)，async参数表示消息是同步发送还是异步发送，0代表同步发送，1代表异步发送。
POST api/notify/message?async=0
{
     "id":"1111111",
     "subject":"告警测试",
     "targets":["01463841","01430948"],
     "content":"内存告警",
     "messageType":"2
 }
```
返回数据格式：

```
  {   
     data："成功发送邮件！"  //返回的数据
     code:0,//执行结果编码，目前只有0成功，1失败
     msg:"请求成功", //服务器返回的提示信息
     level："none", //错误级别
     isSuccess:true //表示成功
  }
  或者
  {
    "data": null,//返回的数据
    "code": 1,//执行结果编码，目前只有0成功，1失败
    "msg": "异常信息",//服务器返回的提示信息，一般在访问失败时给出。
    "level": "none",//错误级别
    "isSuccess": false //表示失败
}
```
### 1.1.2 当前消息请求转发Ihaier
当前告警信息转发Ihaier，具体请求格式如下：
```
//subject:消息主题,targets:目标工号,content:消息内容，messageType：消息类型(1表示既发送邮箱也发送Ihaier,2表示只发送邮箱，3表示只发送Ihaier)，async参数表示消息是同步发送还是异步发送，0代表同步发送，1代表异步发送。
POST api/notify/message?async=0
{
     "id":"1111111",
     "subject":"告警测试",
     "targets":["01463841","01430948"],
     "content":"内存告警",
     "messageType":"3
 }
```
返回数据格式：

```
  {   
     data："send success！",  //返回的数据
     code:0,//执行结果编码，目前只有0成功，1失败
     msg:"请求成功", //服务器返回的提示信息
     level："none", //错误级别
     isSuccess:true//表示发送成功
  }
  或者
  {
    "data": null,//返回的数据
    "code": 1,//执行结果编码，目前只有0成功，1失败
    "msg": "异常信息",//服务器返回的提示信息
    "level": "none",//错误级别
    "isSuccess": false//表示发送成功
  }
```
### 1.1.3 当前消息既转发Ihaier又转发邮箱
当前告警信息同时发送邮箱和Ihaier，具体请求格式如下：
```
//subject:消息主题,targets:目标工号,content:消息内容，messageType：消息类型(1表示既发送邮箱也发送Ihaier,2表示只发送邮箱，3表示只发送Ihaier)，async参数表示消息是同步发送还是异步发送，0代表同步发送，1代表异步发送。
POST api/notify/message?async=0
{
     "id":"1111111", 
     "subject":"告警测试",
     "targets":["01463841","01430948"],
     "content":"内存告警",
     "messageType":"1
 }
```
返回数据格式：

```
  {   
     data："同时发送邮件和ihaier成功！",  //返回的数据
     code:0,//执行结果编码，目前只有0成功，1失败
     msg:"请求成功", //服务器返回的提示信息
     level："none", //错误级别
     isSuccess:true//表示发送成功
  }
  或者
  {
    "data": "发送消息失败！",//返回的数据
    "code": 1,//执行结果编码，目前只有0成功，1失败
    "msg": "异常信息",//服务器返回的提示信息
    "level": "none",//错误级别
    "isSuccess": false//表示发送成功
  }
```
### 2. 整体测试请求
整体测试请求底层是http协议，采用rest风格url作为服务提供。主要包括当前向Kafka消息和查询告警列表。

### 2.1 整体测试流程
整体测试是先向kafka发送一条告警信息，然后调用查询接口查询信息是否能显示。

### 2.1.1 向Kafka发送消息
向kafka发送消息，具体请求格式如下：
 
```
//type:消息类型,topic:消息主题,timestamp:时间戳（long类型的），host:ip地址，instance:实例，project:项目名称，up:0代表告警，1代表消除告警。
POST api/notify/send
{
    "type":"webapp",
    "topic":"webapp",
    "timestamp":1512632966,
    "host":"127.0.0.1",
    "instance":"unittest",
    "entity":{
        "app":"unittest",
        "project":"TEST",
        "topic":"webapp"
    },
    "data":{
        "up":0
    }
}
```
返回数据格式：

```
  {   
     data："成功发送kafka消息！"  //返回的数据
     code:0,//执行结果编码，目前只有0成功，1失败
     msg:"请求成功", //服务器返回的提示信息
     level："none", //错误级别
     isSuccess:true //表示成功
  }
  或者
  {
    "data": null,//返回的数据
    "code": 1,//执行结果编码，目前只有0成功，1失败
    "msg": "异常信息",//服务器返回的提示信息，一般在访问失败时给出。
    "level": "none",//错误级别
    "isSuccess": false //表示失败
}
```

