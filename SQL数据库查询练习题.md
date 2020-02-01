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
