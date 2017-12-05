---
layout:     post
title:      newjira+excel+powerBI实现缺陷动态分析
subtitle:   
date:       2017-12-05
author:     Young
header-img: img/post-bg-debug.png
catalog: true
tags:
    - 缺陷分析
---

### 难关痛

作为测试版本负责人，常用的分析维度包括：bug产生原因，bug有效率，bug优先级，bug在各模块的分布，bug的引入阶段，bug报告人，bug在提交时间上的分布，bug新增原有占比……
在分析bug的时候，你是否出现过这些让人头痛不已的时刻。

- 场景1：版本做完，需要对版本bug进行分析时耗时很长。从数据采集，到数据加工，到分析结论，往往需要针对上述的每个维度均进行单独分析，重复性高，且需要在多个excel间频繁切换，心力憔悴。
- 场景2：在分析维度大于等于2个时，分析起来就很吃力了。通常的做法是在newjira中通过JQL来过滤自己想要的bug列表，再通过导出统计图来导出每个单一维度的饼图或二维的表格，或者通过导出excel来对已经过滤后的数据进行二次加工。
- 场景3：由于测试具有一定的主观性，故每个版本负责人在进行缺陷分析的时候都有自己的一套思路。但这样会导致在回顾过去某个版本的bug分析报告时，由于内容碎片化较为严重，或不是自己熟悉的分析套路，导致其他人很难快速对该版本按自己的思路进行分析理解。

### 成果展示

接下来会展示如何利用newjira+excel+powerBI来实现bug动态分析与分析模型建模，从而解决上述难关痛。
先看最终的效果图


- 场景1：如何能在一个页面里进行各个维度的bug可视化分析

![场景1](/img/in_post/powerBI_pic/场景1.gif)


- 场景2：如何能同时查看某个测试执行人的bug优先级分布和所测bug的模块分布

![场景2](/img/in_post/powerBI_pic/场景2.gif)


- 场景3：如何快速用自己的缺陷分析模板分析版本
在newjira中导出对应版本所有bug的excel（注意：需要导出所有节点），只需将新版本的bug文件命名为构造模板的excel文件名即可
![场景3](/img/in_post/powerBI_pic/场景3.gif)

### 准备环境

1. Excel2007以后版本

2. powerBI（下载路径：[https://go.microsoft.com/fwlink/?LinkId=521662&clcid=0x409](https://go.microsoft.com/fwlink/?LinkId=521662&clcid=0x409)）

### 操作步骤

- 步骤1：在newjira新建版本bug过滤器，导出模式选择Better Excel（All fields），如下图所示
![导出excel按钮](/img/in_post/powerBI_pic/导出excel按钮.png)

- 步骤2：打开导出的excel文件后会发现其为锁定状态，解除状态后再次保存并命名为：bug列表.xls

- 步骤3：打开powerBI，点击开始->获取数据，类别选择excel->连接->选择导出的excel

- 步骤4：构造模型，和excel中画图的操作一致。可在单一或多个页签中放置一种多种类型的图

- 步骤5：保存模型

### 优点

1.	让测试从分析的准备过程中解脱出来，专注于分析本身，并可形成自己的缺陷分析模型。

2.	时间缩短，短时间内就能得到自己想要的信息。

3.	学习成本低，只要会excel中的画图，就可以上手使用。
