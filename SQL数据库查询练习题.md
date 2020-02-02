# SQL数据库查询练习题
## 题目：
> 设有一数据库，包括四个表：学生表（Student）、课程表（Course）、成绩表  （Score）以及教师信息表（Teacher) 

**表(一)Student(学生表)**

属性名|数据类型|可否为空|含义
:---:|:---:|:---:|:---:
Sno|varchar(20)|否|学号(主码)
Sname|varchar(20)|否|学生姓名
Ssex|varchar(20)|否|学生性别
Sbirthday|datetime|可|学生出生年月
Class|varchar(20)|可|学生所在班级

**表(二)Course(课程表)**

属性名|数据类型|可否为空|含义
:---:|:---:|:---:|:---:
Cno|varchar(20)|否|课程号(主码)
Cname|varchar(20)|否|课程名称
Tno|varchar(20)|否|教工编号(外码)

**表(三)Score(成绩表)**

属性名|数据类型|可否为空|含义
:---:|:---:|:---:|:---:
Sno|varchar(20)|否|学号(主码)
Cno|varchar(20)|否|课程号(外码)
Degree|Decimal|可|成绩

**表(四)Student(教师表)**

属性名|数据类型|可否为空|含义
:---:|:---:|:---:|:---:
Tno|varchar(20)|否|教工编号(主码)
Tname|varchar(20)|否|教工姓名
Tsex|varchar(20)|否|教工性别
Tbirthday|datetime|可|教工出生年月
Prof|varchar(20)|可|职称
Depart|varchar(20)|否|教工所在部门



*  1.查询Student表中的所有记录的Sname、Ssex和Class列
   
```sql
   select Sname,Ssex,Class 
   from Student;
```
*    2.查询教师所有的单位即不重复的Depart列

```sql
   select distinct Depart 
   from teacher;
```
*    3.查询Student表的所有记录

```sql
   select * 
   from Student; 
```

*    4.查询Score表中成绩在60到80之间的所有记录  
```sql     
   select * 
   from Score 
   where Degree>60 and Degree<80;
```
*    5.查询Score表中成绩为85，86或88的记录
```sql     
   select * 
   from score 
   where Degree=85 or Degree=86 or Degree=88;
```
*    6.查询Student表中“95031”班或性别为“女”的同学记录
```sql     
   select * 
   from student 
   where Class=95031 or Ssex='女';         
```
*    7.以Class降序查询Student表的所有记录
```sql     
   select * 
   from student 
   order by Class desc;     
```
*    8.以Cno升序、Degree降序查询Score表的所有记录     
```sql     
   select * 
   from score 
   order by Cno asc ,Degree desc;
```
*    9.查询“95031”班的学生人数    
```sql     
   select count(Class) as NumberofStudent 
   from student 
   where Class='95031';
```
*    10.查询Score表中的最高分的学生学号和课程号。（子查询或者排序）     
```sql     
   select Sno,Cno 
   from score 
   where Degree=(select max(Degree) from score);
```
*    11.查询每门课的平均成绩
```sql     
   select Cno,avg(Degree) 
   from score 
   group by Cno;     
```
*    12.查询Score表中至少有5名学生选修的并以3开头的课程的平均分数     
```sql     
   select Cno,avg(Degree) 
   from score 
   where Cno like '3%'group by Cno having count(Cno)>5;
```
*    13.查询分数大于70，小于90的Sno列     
```sql     
   select Sno 
   from score 
   where degree between 70 and 90;
```
*    14.查询所有学生的Sname、Cno和Degree列     
```sql     
   select Sname,Cno,Degree 
   from student 
   join score on student.Sno=score.Sno;
```
*    15.查询所有学生的Sno、Cname和Degree列
```sql     
   select Sno,Cname,Degree 
   from score 
   join course on course.Cno=score.Cno;
```
*    16.查询所有学生的Sname、Cname和Degree列
```sql     
   select Sname,Cname,Degree 
   from student 
   join score on student.Sno=score.Sno 
   join course on score.Cno=course.Cno;
```
*    17.查询“95033”班学生的平均分
```sql     
   select avg(Degree) 
   from score 
   join student on student.Sno=score.Sno 
   group by Class having Class='95033';
```
*    18.假设使用如下命令建立了一个grade表：
     create table grade(low int(3),upp int(3),rank char(1))
     insert into grade values(90,100,’A’)
     insert into grade values(80,89,’B’)
     insert into grade values(70,79,’C’)
     insert into grade values(60,69,’D’)
     insert into grade values(0,59,’E’)
     现查询所有同学的Sno、Cno和rank列
```sql     
   select Sno,Cno,`rank` 
   from grade 
   join score on score.Degree between grade.low and grade.upp;
```
*    19.查询选修“3-105”课程的成绩高于“109”号同学成绩的所有同学的记录
```sql     
   select * 
   from student,score 
   where  score.Cno='3-105'and student.Sno=Score.Sno 
   and score.Degree>(select Degree from score where Sno='109' 
   and score.Cno='3-105');
```
*    20.查询score中选学多门课程的同学中分数为非最高分成绩的记录
```sql     
   select * 
   from score as a 
   where Degree<(select max(Degree) from score as b 
   where a.Cno=b.Cno) and 
   Sno in(select Sno from score group by Sno having count(Cno)>1);
```
*    21.查询成绩高于学号为“109”、课程号为“3-105”的成绩的所有记录
```sql     
   select * 
   from student,score 
   where student.Sno=score.Sno and 
   Degree>(select Degree from score where Sno='109' and Cno='3-105');
```
*    22.查询和学号为108的同学同年出生的所有学生的Sno、Sname和Sbirthday列

```sql
   select Sno,Sname,Sbirthday 
   from student 
   where year(Sbirthday)=(select year(Sbirthday) from student where      Sno='107');
```

*  23.查询“张旭“教师任课的学生成绩
```sql     
   select Degree 
   from Score,Teacher,Course 
   where Teacher.Tname='张旭' 
   and Teacher.Tno=Course.Tno 
   and Course.Cno=Score.Cno;
```
*    24.查询选修某课程的同学人数多于5人的教师姓名
```sql
   select Tname 
   from teacher 
   where Tno in (select Tno from course 
   where Cno in (select Cno from score group by Cno having      	    count(Cno)>5));
```
*    25.查询95033班和95031班全体学生的记录
```sql
   select * 
   from student 
   where Class='95033' or Class='95031';
```
*    26.查询存在有85分以上成绩的课程Cno
```sql
   select distinct Cno 
   from score 
   where Degree>'85';
```
*    27.查询出“计算机系“教师所教课程的成绩表
```sql
   select Sno,Cno,Degree 
   from score 
   where Cno in(select Cno from course 
   where Tno in (select Tno from teacher 
   where teacher.Depart='计算机系'));
```
*    28.查询“计算机系”与“电子工程系“不同职称的教师的Tname和Prof
```sql
   select Tname,Prof 
   from Teacher a 
   where Prof not in
   (select Prof from Teacher b where a.Depart!=b.Depart);
```
*    29.查询选修编号为“3-105“课程且成绩至少高于选修编号为“3-245”的同学的Cno、Sno和  Degree,并按Degree从高到低次序排序
```sql
   select Cno,Sno,Degree 
   from Score as a 
   where (select Degree from Score as b where Cno='3-105' 
   and b.Sno=a.Sno)>=
   (select Degree from Score as c where Cno='3-245' and c.Sno=a.Sno)    order by Degree desc;
```
*   30. 查询选修编号为“3-105”且成绩高于选修编号为“3-245”课程的同学的Cno、Sno和Degree.
```sql
   select * 
   from Score as a 
   where (select Degree from Score as b where Cno='3-105' 
   and b.Sno=a.Sno)>
   (select Degree from Score as c where Cno='3-245' and c.Sno=a.Sno);
```
*    31.查询所有教师和同学的name、sex和birthday
```sql
   select Sname as name,Ssex as sex,Sbirthday as birthday 
   from student 
   union 
   select Tname,Tsex,Tbirthday 
   from teacher;
```
*    32.查询所有“女”教师和“女”同学的name、sex和birthday
```sql
   select Sname as name,Ssex as sex,Sbirthday as birthday 
   from student 
   where Ssex='女'
   union 
   select Tname,Tsex,Tbirthday 
   from teacher 
   where Tsex='女';
```
*    33.查询成绩比该课程平均成绩低的同学的成绩表
```sql
   select * 
   from score as a 
   where a.Degree<
   (select avg(Degree) from score as b where a.Cno=b.Cno);
```
*    34.查询所有任课教师的Tname和Depart
```sql
   select Tname,Depart 
   from teacher 
   where Tname in 
   (select Tname from course,score,teacher where
   teacher.Tno=course.Tno and course.Cno=score.Cno);
```
*    35.查询所有未讲课的教师的Tname和Depart
```sql
   select Tname,Depart 
   from teacher 
   where Tname not in 
   (select Tname from course,score,teacher where
   teacher.Tno=course.Tno and course.Cno=score.Cno);
```
*    36.查询至少有2名男生的班号
```sql
   select Class 
   from student group by Class 
   having (select count(Ssex) from student where Ssex='男')>1;
```
*    37.查询Student表中不姓“王”的同学记录
```sql
   select * 
   from student 
   where Sname not like '王%';
```
*    38.查询Student表中每个学生的姓名和年龄
```sql
   select Sname,2020-year(Sbirthday) 
   from student;
```
*    39.查询Student表中最大和最小的Sbirthday日期值
```sql
   select max(Sbirthday) as 最大Sbirthday,
   min(Sbirthday) as 最小 Sbirthday 
   from student;
```
*    40.以班号和年龄从大到小的顺序查询Student表中的全部记录
```sql
   select * 
   from student 
   order by Class desc,Sbirthday asc;
```
*    41.查询“男”教师及其所上的课程
```sql
   select Tname,Cname 
   from teacher as a,course as b 
   where a.Tno=b.Tno and Tsex='男';
```
*    42.查询最高分同学的Sno、Cno和Degree列
```sql
   select Sno,Cno,Degree 
   from score 
   where Degree=(select max(Degree) from score);
```
*    43.查询和“李军”同性别的所有同学的Sname
```sql
   select Sname 
   from student 
   where Ssex=(select Ssex from student where Sname='李军') 
   and Sname!='李军';
```
*    44.查询和“李军”同性别并同班的同学Sname
```sql
   select Sname 
   from student 
   where Ssex=(select Ssex from student where Sname='李军') 
   and
   Class=(select Class from student where Sname='李军') 
   and 
   Sname!='李军';
```
*    45.查询所有选修“计算机导论”课程的“男”同学的成绩表
```sql
   select Sno,Degree 
   from score 
   where Cno in (select Cno from course where Cname='计算机导论')
   and
   Sno in (select Sno from student where Ssex='男' );
```