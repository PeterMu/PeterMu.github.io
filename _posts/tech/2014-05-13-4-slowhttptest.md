---
layout: post
title: (转)Slow HTTP Denial Of Service Attack 
description: 缓慢的HTTP POST DoS攻击依赖于HTTP协议的事实,通过设计,将每次发送数据包的一部分。如果一个HTTP请求是不完整的,或者如果转移率非常低,服务器保持其资源忙等待其余的数据。如果服务器保持太多的资源忙,HTTP服务器将拒绝其它的请求服务。这个工具就是通过发送缓慢HTTP请求,让目标HTTP服务器处于忙碌状态(也可以这样理解，当post请求时，指定一个非常大的content-length,然后以很低的速度发包）。
category: tech
---

缓慢的HTTP POST DoS攻击依赖于HTTP协议的事实,通过设计,将每次发送数据包的一部分。如果一个HTTP请求是不完整的,或者如果转移率非常低,服务器保持其资源忙等待其余的数据。如果服务器保持太多的资源忙,HTTP服务器将拒绝其它的请求服务。这个工具就是通过发送缓慢HTTP请求,让目标HTTP服务器处于忙碌状态(也可以这样理解，当post请求时，指定一个非常大的content-length,然后以很低的速度发包）。

## 1.测试使用工具 :slowhttptest

可配置选项的完整列表如下:

1. -a 开始值范围说明符用于范围头测试

1. -b 将字节限制的范围说明符用于范围头测试

1. -c的连接数限制为65539

1. -d proxy host:port用于指导所有流量通过web代理

1. -e proxy host:port端口用于指导只有探针交通通过web代理

1. -h,B,R或x指定减缓在头部分或在消息体,- R 允许范围检验,使慢读测试- x

1. -g生成统计数据在CSV和HTML格式,模式是缓慢的xxx。csv / html,其中xxx是时间和日期

1. -i seconds秒间隔跟踪数据在几秒钟内,每个连接

1. -k管道因子次数重复请求在同一连接慢读测试如果服务器支持HTTP管道内衬。

1. -l在几秒钟内，秒测试时间

1. -n秒间隔从接收缓冲区读取操作

1. -o文件定义输出文件路径和/或名称,如果指定有效- g

1. -p秒超时等待HTTP响应在探头连接后,服务器被认为是不可访问的

1. -r seconds连接速度

1. -s字节值的内容长度标题详细说明,如果指定- b

1. -t verb自定义

1. -u URL目标URL,相同的格式键入浏览器,e.g https://host[:port]/

1. -v level冗长等级0 - 4的日志

1. -w字节范围广告的窗口大小会选择从

1. -x字节最大长度的跟踪数据结束

1. -y字节范围广告的窗口大小会选择从

1. -z字节从接收缓冲区读取字节与单一的read()操作


## 2. 案例说明

```java
slowhttptest -c 1000 -B -g -o my_body_stats -i 110 -r 200 -s 8192 -t FAKEVERB -u http://mysite -x 10 -p 3
```
    
效果很明显，网页打开明显变慢

## 3. 解决措施

对web服务器的http头部传输的最大许可时间进行限制，修改成最大许可时间为20秒。

1. 统计每个TCP连接的时长并计算单位时间内通过的报文数量即可做精确识别。一个TCP连接中，HTTP报文太少和报文太多都是不正常的，过少可能是慢速连接攻击，过多可能是使用HTTP 1.1协议进行deHTTP Flood攻击，在一个TCP连接中发送多个HTTP请求。

1. 限制HTTP头部传输的最大许可时间。超过指定时间HTTP Header还没有传输完成，直接判定源IP地址为慢速连接攻击，中断连接并加入黑名单。

转自[牛磊的博客-Slow HTTP Denial Of Service Attack](http://helloeveryone.blog.51cto.com/6171143/1241809)
