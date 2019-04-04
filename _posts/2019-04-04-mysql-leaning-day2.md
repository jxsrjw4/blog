---
layout: post
title: Mysql打卡第二天
date: 2019-04-04 21:00:00  
categories: DataWhale/Mysql
---

<h1>任务三</h1>
<h2>初始化环境</h2>
主键int设置自增长：AUTO_INCREMENT primary key
![](/static/img/20190404/01.png)
<h2>作业1:计算课程学生数</h2>
编写一个 SQL 查询，列出所有超过或等于5名学生的课,学生在每个课中不应被重复计算.
![](/static/img/20190404/02.png)
1、先用distinct过滤重复数据
2、按课程分组(group by class)
3、设置分组个数大于等于5(having count(1)>=5)
<h2>作业2：交换工资</h2>
![](/static/img/20190404/03.png)


<h1>任务四</h1>
<h2>初始化环境</h2>
![](/static/img/20190404/04.png)
<h2>作业1：组合两张表</h2>
![](/static/img/20190404/05.png)

<h2>作业2：删除重复的邮箱</h2>
![](/static/img/20190404/06.png)

<h1>总结</h1>
1.sql语句需要以分号结尾


<h1>参考资料</h1>
[mysql列交换与行交换](https://www.cnblogs.com/foreverYoungCoder/p/9449312.html)

[Docker重置mysql](https://blog.csdn.net/Yg854879464/article/details/82263554)

