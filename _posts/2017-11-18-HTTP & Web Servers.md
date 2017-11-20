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

# Introduction
## 环境要求

1. 需要用到linux系统
[在win10上如何安装linux](https://msdn.microsoft.com/en-us/commandline/wsl/install-win10)

2. python3
在linux系统中，python可能装了两个版本。terminal中的python命令一般指python2，而python3指的python3。这里需要加以区分。

3. Git
通过git去得课程的源码。

4. Nmap

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
'''
nmap [ <扫描类型> ...] [ <选项> ] { <扫描目标说明> }
'''

- 全面进攻性扫描（包括各种主机发现、端口扫描、版本扫描、OS扫描及默认脚本扫描）:
'''
nmap -A -v targetip
'''

- Ping扫描:
'''
nmap -sn -v targetip
'''

- 快速端口扫描:
'''
nmap -F -v targetip
'''

- 版本扫描:
'''
nmap -sV -v targetip 
'''

- 操作系统扫描:
'''
nmap -O -v targetip
'''

5. 服务器和客户端的简单交互示例
![服务器和客户端的简单交互示例](img/in_post/HTTP-WebServer_pic/01.png)

# Your first web server
# Parts of a URI
# Hostnames and ports
## Hostnames
A full HTTP or HTTPS URI includes the hostname of the web server, like **www.udacity.com** or **www.un.int** or **www.cheeseboardcollective.coop** (my favorite pizza place in the world, in Berkeley CA). A hostname in a URI can also be an IP address: for instance, if you put [http://216.58.194.174/](http://216.58.194.174/) in your browser, you'll end up at Google.
'''
Why is it called a hostname? In network terminology, a host is a computer on the network; one that could host services.
'''