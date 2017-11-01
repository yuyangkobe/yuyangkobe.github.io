---
layout:     post
title:      Elementtree解析xml
subtitle:   
date:       2017-10-31
author:     Young
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - Python3
---

## 解析xml的步骤

### 获取xml文件

- 在当前路径下获取xml

``` tree = ET.ElementTree(file=文件名)  # 文件名为字符串类型```

### 获取xml根节点

- 使用elementtree中tree对象的getroot()来获得当前xml的根节点

```root = tree.getroot()```

### 获取各节点的值

- 使用**xpath**来描述所需的节点

```
<?xml version="1.0"?>
<data>
    <country name="Liechtenstein">
        <rank updated="yes">2</rank>
        <year>2008</year>
        <gdppc>141100</gdppc>
        <neighbor name="Austria" direction="E"/>
        <neighbor name="Switzerland" direction="W"/>
    </country>
    <country name="Singapore">
        <rank updated="yes">5</rank>
        <year>2011</year>
        <gdppc>59900</gdppc>
        <neighbor name="Malaysia" direction="N"/>
    </country>
    <country name="Panama">
        <rank updated="yes">69</rank>
        <year>2011</year>
        <gdppc>13600</gdppc>
        <neighbor name="Costa Rica" direction="W"/>
        <neighbor name="Colombia" direction="E"/>
    </country>
</data>
```

```
import xml.etree.ElementTree as ET

root = ET.fromstring(countrydata)

# Top-level elements
root.findall(".")

# All 'neighbor' grand-children of 'country' children of the top-level
# elements
root.findall("./country/neighbor")

# Nodes with name='Singapore' that have a 'year' child
root.findall(".//year/..[@name='Singapore']")

# 'year' nodes that are children of nodes with name='Singapore'
root.findall(".//*[@name='Singapore']/year")

# All 'neighbor' nodes that are the second child of their parent
root.findall(".//neighbor[2]")
```

#### xpath语法
语法|说明
-|-
tag|
*|
.|
//|
..|
[@attrib]|
[@attrib='value']|
[tag]|
[tag='text']|
[position]|