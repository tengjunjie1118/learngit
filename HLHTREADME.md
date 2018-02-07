---
title: 互联互通监控接入
tags: 接入说明，接入简介
---


# Tomcat接入方式

### 介绍
tomcat接入主要是通过拦截器收集数据,支持tomcat manager，并且在此基础上做了扩展，支持接口访问。
### 监控指标
1. 进程状态
2. jvm内存使用率
3. 应用存活度
4. jvm垃圾回收现状

### 接入监控前后内存变化值

![enter description here][1]

![enter description here][2]

### 监控拦截原理图

。。。。。。。。。。。

### 监控接入步骤以及用到的jar包

1、将附件jar包下载下来，将.jar文件加入到tomcat下的lib文件夹里面。

2、将metrics.war放入到tomcat下的webapps文件夹里面。metrics.war是暴露监控服务的api

3、在tomcat下的conf文件夹下的web.xml中添加以下信息，放在</web-app>标签之前。

<!-- prometheus monitoring --> 

<filter>     

        <filter-name>ServletMetricsFilter</filter-name>

        <filter-class>nl.nlighten.prometheus.tomcat.TomcatServletMetricsFilter</filter-class>                         

        <async-supported>true</async-supported> 

</filter> 

<filter-mapping>

        <filter-name>ServletMetricsFilter</filter-name>

        <url-pattern>/*</url-pattern> 

</filter-mapping>

                                                            

4、最后重启tomcat即可。


## 用到的jar包
=[enter description here][3]
___



 


  [1]: ./images/%E7%AC%AC%E4%BA%8C%E5%BC%A0%E5%9B%BE_3.png "未接入监控内存"
  [2]: ./images/%E7%AC%AC%E4%B8%80%E5%BC%A0%E5%9B%BE_1.png "接入监控后内存"
  [3]: ./attachments/jar_1.rar