---
title: "Servlet笔记"
tags: [ "Servlet" , "Note" , "HTML5" , "CSS" , "JavaScript" ]
date: 2023-12-23
description: "在学习Servlet遇到的Bug和相关知识"
slug: "servlet-note"
---

# 解决html和js中文乱码问题
在web.xml中添加以下代码：
```xml
<jsp-config>
    <jsp-property-group>
        <url-pattern>*.html</url-pattern>
        <page-encoding>UTF-8</page-encoding>
    </jsp-property-group>
    
    <jsp-property-group>
        <url-pattern>*.js</url-pattern>
        <page-encoding>UTF-8</page-encoding>
    </jsp-property-group>
</jsp-config>
```

# MVC三层架构
## 1. 表现层（View）
负责接收用户请求，向用户输出响应结果，通常采用Servlet或JSP实现。
## 2. 业务层（Model）
负责业务逻辑处理，通常采用JavaBean实现。
## 3. 数据访问层（Conntroller）
负责与数据库进行交互，包括数据库连接、SQL语句执行、数据封装等，通常采用JDBC或ORM实现。