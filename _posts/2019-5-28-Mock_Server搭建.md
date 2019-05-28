---
layout:     post
title:      Moco工具使用
subtitle:   Mock Server搭建
date:       2019-05-28
author:     Young
header-img: img/post-bg-os-metro.jpg
catalog: true
tags:
    - 测试
    - 测试环境
    - Mock
---

## 背景

在研发阶段，会出现需要调用外部网络接口的需求。 若此时外部网络接口还未开发或未开发完成，则下游便会出现等待。 此时如果下游想要并行开发自己部分的代码，则可以考虑采用MockServer的方式来构造一个测试服务器来帮助自己进行下游开发。

## MockServer介绍

[MockServer](http://mock-server.com/)旨在通过模拟 HTTP和HTTPS系统（如Web服务或Web站点）来简化集成测试，并通过允许团队针对不完整或不稳定的服务进行开发来解耦开发团队。

### 简化测试

MockServer通过隔离被测系统以确保测试可靠运行并且仅在存在真正错误时失败的有效机制。这样的机制避免了由于无关的外部变化（例如：网络故障或者服务器被重新启动/重新部署）而导致测试失败的情况。 简化了测试场景。 

### 解耦开发团队

MockServer允许团队针对不完整或不稳定的服务来展开开发，以达到对开发团队任务的解耦。

- 如果API或服务尚未完全开发，MockServer可以用来模拟API，这样任何使用该服务的团队都可以开始工作而不会被延迟。
- 如果API或服务不稳定或不可靠，MockServer可以起到隔离的作用。 

### 使用场景

访问一个接口login，返回一个特定的数据


## 环境搭建

1. 安装java

下载路径：[https://www.java.com/zh_CN/download/windows-64bit.jsp](https://www.java.com/zh_CN/download/windows-64bit.jsp)

2. 下载Moco的jar包

Moco：[https://github.com/dreamhead/moco](https://github.com/dreamhead/moco)

3. 在jar包目录下新建`settings.json`，输入以下内容
```
[
    {
        "include" : "TestAPI/TestAPI.json"
    }
]
```

4. 在jar包目录下新建目录`TestAPI`，输入以下内容
```
[
  {
    "request" :
    {
      "uri" : "/login",
      "method" : "get",
      "queries" :
        {
         "username" : "admin",
         "password" : "123456"
        }
    },
    "response" :
    {
    	"file" : "./TestAPI/TestAPI_response.json"
    }
  }
]
```

5. 在TestAPI目录下新建`TestAPI_response.json`，输入以下内容
```
[
  {
  	"status":"登陆成功"
  }
]
```

6. 打开终端，定位到jar包目录，命令行输入
```
java -jar moco.jar start -p 8888 -g settings.json
```

7. 打开浏览器，输入`127.0.0.1:8888/login`，点击回车后浏览器返回
```
[
  {
  	"status":"登陆成功"
  }
]
```










