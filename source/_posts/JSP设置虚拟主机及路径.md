---
title: Jsp设置虚拟主机及路径
date: 2020-01-14 18:15:37
tags: [Java,杂项]
categories: [计算机基础,Java,Jsp]
toc: true
copyright: true
description:

---

<meta name="referrer" content="no-referrer" />  

<!--more-->

# Jsp设置虚拟主机及路径

Jsp项目默认存储路径在Tomcat的webapps路径下，通过自己新建文件夹，内部建立WEB-INF书写web.xml的方式，来访问项目的主页。

那我们有没有什么方式可以切换默认的路径呢？

我们有两种方式

## 0x01 设置虚拟路径

在conf目录下找到server.xml,找到Host,在末尾追加如下内容：

```xml
<Context docBase="项目的绝对路径" path="项目的相对路径" />
```

或者在Tomcat下的conf下的Catalina中新建：

```
项目名.xml
```

把刚才的内容抄一遍就可以了。

## 0x02 设置虚拟主机

有时做项目我们不想通过localhost:8080来访问，此时我们就需要在本地做一个域名解析器。

第一步：找到server.xml

第二步：再新建一个Host：

```xml
<Host appBase="webapps" name="www.test.com"> 
          <Context docBase="" path ="/" /> 
</Host>
```

appBase：写项目的绝对路径

name：写你自定义的域名

docBase：写项目的绝对路径

path：写 / 即可

```xml
<Connector port="80" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```

更改默认端口为 80

第三步：配置server.xml中的Engine

把defaultHost改成刚刚自己设置的域名

第四步：配置host文件

在这个路径下 C:\Windows\System32\drivers\etc

存在一个host文件

配置如下内容：

```
127.0.0.1 www.test.com
```

