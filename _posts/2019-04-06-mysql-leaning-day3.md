---
layout: post
title: Mysql打卡第三天
date: 2019-04-07 16:00:00  
categories: DataWhale/Mysql
---

<h1>任务四</h1>
<h2>初始化环境</h2>
![](/static/img/20190406/01.png)
<h2>作业1:各部门工资最高的员工</h2>
![](/static/img/20190406/02.png)

<h2>作业2:换座位</h2>
如果学生人数是奇数，则不需要改变最后一个同学的座位。
因为把答案作为初始数据导入了，所以最终结果与答案不符。
这里用到了自联表及IFNULL函数(给空值赋予默认值的函数)

`select a.id, ifnull(b.student,a.student) student from seat a left join seat b on ( b.Id=a.Id+1 and a.Id%2=1) or (b.Id=a.Id-1 and a.Id%2=0) ;`

![](/static/img/20190406/03.png)

<h2>作业3:分数排名</h2>
![](/static/img/20190406/05.png)
![](/static/img/20190406/04.png)

<h1>任务四</h1>
<h2>初始化环境</h2>
建表语句：

`create table Users
(
id bigint auto_increment PRIMARY KEY,
Banned varchar(3),
Role ENUM('client','driver','partner')
)`

`create table Trips
(
id bigint auto_increment PRIMARY key,
Client_Id bigint,
Driver_Id BIGINT,
City_Id BIGINT,
Status Enum('completed', 'cancelled_by_driver','cancelled_by_client')
)`

重命名主键

`alter table Users change id Users_Id bigint;`

![](/static/img/20190406/06.png)
<h2>作业1：行程和用户</h2>
查询2013年10月1日 至 2013年10月3日 期间非禁止用户的取消率、

`select Request_at,FORMAT(count( if (Status<>'Completed', true,null))/count(1),2) as 'Cancellation Rate' from Trips  
join Users on client_id=users_id 
where Banned='NO' 
GROUP BY Request_at
`

![](/static/img/20190406/07.png)

<h2>作业2：各部门前3高工资的员工</h2>

`select Name as Department, Employee, Salary from (
select NAME as Employee, Salary, DepartmentId,row_number() over(partition by DepartmentId order by salary desc) as rownum
 from Employee
) a
join Department on id=a.DepartmentId
where a.rownum<4`

![](/static/img/20190406/08.png)

<h2>作业2：分数排名 </h2>
实现排名功能，但是排名是连续的

`SELECT Score,@curRank :=@curRank+1 AS 'Rank'
FROM score,(select @curRank :=0) q
ORDER BY Score DESC`

![](/static/img/20190406/09.png)

实现排名功能，但是排名是非连续的

`SELECT Score,
case when @preRank=Score then @curRank
         when @preRank :=Score then @curRank :=@curRank+1
end as 'Rank'
FROM score,(select @curRank :=0, @preRank :=NULL) q
ORDER BY Score DESC`

![](/static/img/20190406/10.png)

<h1>总结</h1>



<h1>参考资料</h1>
[mysql开窗函数](https://blog.csdn.net/qq_30505673/article/details/88661037#DENSE_RANK_104)

[Rank排名查询](https://blog.csdn.net/justry_deng/article/details/80597916)

