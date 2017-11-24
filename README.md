# 消息转发接口文档
## 目录
* 1、消息请求 
  * 1.1 消息转发邮箱或者Ihaier
    * 1.1.1 消息转发邮箱
    * 1.1.2 消息转发Ihaier
    
### 1. 消息请求
消息请求底层是http协议，采用rest风格url作为服务提供。主要包括当前消息转发给邮箱还是Ihaier。

### 1.1 当前消息请求
提供当前正在发生的消息转发接口。

### 1.1.1 当前消息请求转发邮箱
当前告警信息转发邮箱，具体请求格式如下：
 
```
//subject:消息主题,targets:目标工号（可以多个),content:消息内容，messageType：消息类型(1表示既发送邮箱也发送Ihaier,2表示只发送邮箱，3表示只发送Ihaier)
POST api/notify/message
{
     subject: 某某系统告警
     targets:a0006476
     content:内存告警
     messageType:2
 }
```
返回数据格式：

```
  {   
     data：String  //返回的数据
     code:0/1 ,//执行结果编码，目前只有0成功，1失败
     msg:string //服务器返回的提示信息，一般在访问失败时给出。
     level：none //错误级别，一般会在访问失败时给出。
     isSuccess:bool(true/false),//表示是否成功
  }
```
### 1.1.2 当前消息请求转发Ihaier
当前告警信息转发Ihaier，具体请求格式如下：
```
//subject:消息主题,targets:目标工号（可以多个),content:消息内容，messageType：消息类型(1表示既发送邮箱也发送Ihaier,2表示只发送邮箱，3表示只发送Ihaier)
POST api/notify/message
{
     subject: 某某系统告警
     targets:a0006476
     content:内存告警
     messageType:1
 }
```
返回数据格式：

```
    {   
     data：String  //返回的数据
     code:0/1 ,//执行结果编码，目前只有0成功，1失败
     msg:string //服务器返回的提示信息，一般在访问失败时给出。
     level：none //错误级别，一般会在访问失败时给出。
     isSuccess:bool(true/false),//表示是否成功
  }
```
 
 
