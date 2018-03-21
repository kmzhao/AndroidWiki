## MySql入门02

### 一，表与表之间的关系
#### 1.1  1---多 or  多---1 的关系
* 实例： 国家--城市  班级--学生  黄上--妃子
* 主外键关系描述一对多的关系：

          alter table 从表 add constraint foreign key(从表外键) references 主键(主表主键)
