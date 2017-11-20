---
layout:     post
title:      HTTP & Web Servers
subtitle:   udacity课程学习
date:       2017-11-18
author:     Young
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - Http协议
    - 计算机网络
    - udacity
---

# Class1. Requests & Responses

## Introduction

### 环境要求

#### 需要用到linux系统
[在win10上如何安装linux](https://msdn.microsoft.com/en-us/commandline/wsl/install-win10)

#### python3
在linux系统中，python可能装了两个版本。terminal中的python命令一般指python2，而python3指的python3。这里需要加以区分。

#### Git
通过git去得课程的源码。

#### Nmap
Nmap（网络映射器）是一款用于网络发现和安全审计的网络安全工具，它是自由软件。软件名字Nmap是Network Mapper的简称。通常情况下，Nmap用于：
	- 列举网络主机清单
	- 管理服务升级调度
	- 监控主机
	- 服务运行状况

Nmap可以检测目标主机是否在线、端口开放情况、侦测运行的服务类型及版本信息、侦测操作系统与设备类型等信息。 它是网络管理员必用的软件之一，用以评估网络系统安全。
Nmap 是不少黑客及脚本小孩爱用的工具 。系统管理员可以利用Nmap来探测工作环境中未经批准使用的服务器，黑客通常会利用Nmap来搜集目标电脑的网络设定，从而计划攻击的方法。
Nmap通常用在信息搜集阶段，用于搜集目标机主机的基本状态信息。扫描结果可以作为漏洞扫描、漏洞利用和权限提升阶段的输入。例如，业界流行的漏洞扫描工具Nessus与漏洞利用工具Metasploit都支持导入Nmap的XML格式结果，而Metasploit框架内也集成了Nmap工具（支持Metasploit直接扫描）。
Nmap不仅可以用于扫描单个主机，也可以适用于扫描大规模的计算机网络（例如，扫描英特网上数万台计算机，从中找出感兴趣的主机和服务）。

- Nmap 基本语法
```
nmap [ <扫描类型> ...] [ <选项> ] { <扫描目标说明> }
```

- 全面进攻性扫描（包括各种主机发现、端口扫描、版本扫描、OS扫描及默认脚本扫描）:
```
nmap -A -v targetip
```

- Ping扫描:
```
nmap -sn -v targetip
```

- 快速端口扫描:
```
nmap -F -v targetip
```

- 版本扫描:
```
nmap -sV -v targetip 
```

- 操作系统扫描:
```
nmap -O -v targetip
```

#### 服务器和客户端的简单交互示例
![服务器和客户端的简单交互示例](/img/in_post/HTTP-WebServer_pic/01.png)

## Your first web server
An HTTP transaction always involves a client and a server. You're using an HTTP client right now — your web browser. Your browser sends HTTP requests to web servers, and servers send responses back to your browser. Displaying a simple web page can involve dozens of requests — for the HTML page itself, for images or other media, and for additional data that the page needs.

HTTP was originally created to serve hypertext documents, but today is used for much more. As a user of the web, you're using HTTP all the time.

**Notice**：Applications that you use in a web browser, and mobile services, are both likely to use HTTP. But low-level network tests such as `ping` do not.

A lot of smartphone apps use HTTP under the hood to send requests and receive data. Web browsers are just the most common — and complicated — user interface for web technology. But browsers are not the only web client around. HTTP is powerful and widely supported in software, so it's a common choice for programs that need to talk to each other across the network, even if they don't look anything like a web browser.

### Exercise: Running your first web server
So what about the other end, the web server? Well, it turns out that a web server can actually be a lot simpler than a browser. Browsers have all this user interface and animation and graphics stuff going on. A server just needs to do one thing: handle incoming requests.

The Python `http.server` module can run a built-in web server on your computer. It's not a web app you'd publish to the world; it's a demonstration of Python's HTTP abilities. We'll be referring to this as the demo server in this lesson.

So, let's get started with the demo web servicesver.

Open up a terminal; `cd` to a directory that has some files in it — maybe a directory containing some text files, HTML files, or images — then run `python3 -m http.server 8000` in your terminal

#### Running your first web server
![Running your first web server](/img/in_post/HTTP-WebServer_pic/02.png)

And that's the Python demo web server, running on your own computer. It serves up files on your local disk so you can look at them in your browser.

This may not seem like much of a big deal — after all, if you just wanted to access files on your local computer in your browser, you could use `file://` URIs. But the demo server is actually a web server. If you have another computer on the same local network, you could use it to access files served up by this server.

When you put `localhost:8000` in your browser, your browser sends an HTTP request to the Python program you're running. That program responds with a piece of data, which your browser presents to you. In this case, it's showing you a directory listing as a piece of HTML. Use your browser's developer tools to look at the HTML that it sends.

**Note**: If you have a file called `index.html` in that directory, you'll see the contents of that file in your browser instead of the directory listing. Move that file somewhere else and reload the page, and you will see the directory listing like the one above.

![have a file called index.html](/img/in_post/HTTP-WebServer_pic/03.png)

**404** is the HTTP status code for "Not Found". On Highway 101, not far from the Udacity office in Mountain View, there's a sign that tells the distance to Los Angeles. As it happens, it's 404 miles from Mountain View to Los Angeles, so the sign says **Los Angeles 404**. And so, every web programmer in Silicon Valley has probably heard the "Los Angeles Not Found" joke at least once.

#### What's a server anyway?
A server is just a program that accepts connections from other programs on the network.

When you start a server program, it waits for clients to connect to it — like the demo server waiting for your web browser to ask it for a page. Then when a connection comes in, the server runs a piece of code — like calling a function — to handle each incoming connection. A connection in this sense is like a phone call: it's a channel through which the client and server can talk to each other. Web clients send requests over these connections, and servers send responses back.

Take a look in the terminal where you ran the demo server. You'll see a server log with an entry for each request your browser sent:
```
Serving HTTP on 0.0.0.0 port 8000 ...
127.0.0.1 - - [03/Oct/2016 13:47:35] "GET / HTTP/1.1" 200 -
127.0.0.1 - - [03/Oct/2016 13:47:36] "GET / HTTP/1.1" 200 -
127.0.0.1 - - [03/Oct/2016 13:48:06] "GET /falafelosofhy.png HTTP/1.1" 200 -
127.0.0.1 - - [03/Oct/2016 13:49:23] code 404, message File not found
127.0.0.1 - - [03/Oct/2016 13:49:23] "GET /NotExistyFile HTTP/1.1" 404 -
```

Hey wow, what is all this stuff? There are some dates and times in there, but what's `GET / HTTP/1.1`, or for that matter `127.0.0.1`? And what's that `200` doing over there?

How do these things relate to the web address you put into your browser? Let's take a look at that next.

## Parts of a URI

## Hostnames and ports

### Hostnames

A full HTTP or HTTPS URI includes the hostname of the web server, like `www.udacity.com` or `www.un.int` or `www.cheeseboardcollective.coop` (my favorite pizza place in the world, in Berkeley CA). A hostname in a URI can also be an IP address: for instance, if you put [http://216.58.194.174/](http://216.58.194.174/) in your browser, you'll end up at Google.

**note:** Why is it called a hostname? In network terminology, a host is a computer on the network; one that could host services.