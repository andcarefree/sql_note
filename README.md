# sql语言练习笔记

***

### 1. limit
***limit***子句主要用来限制返回的行个数
```sql
select * from users limit 1 offset 2
select * from users limit 2,1
```
上述两条sql语句都表示返回查询结果的***第三条***记录\
主要想吐槽的是，为啥两种写法关于限制行数与偏移量的先后顺序没有一一对应\
不使用***offset***语句的话则只限制返回的记录条数

### 2. order by _ (desc)
***order by***语句根据其后跟的列名对返回的行记录进行排序\
顺序就为常规意义的顺序，若需要逆序则在列名后加***desc***
```sql
select * from users order by user_name desc 
```

### 3. group by _ (having)
***group by***语句根据其后跟的列名对该列数据相同的记录行进行分组\
然后就可以对不同的组进行select（只能select作为分组依据的字段）\
可以通过***having***对组进行过滤，就像***where***对行记录进行过滤一样
```sql
select user_age from users group by user_age
```

### 4. distinct
***distinct***语句对其后所跟的列名进行去重\
运用***group by***语句也可以达到去重的效果
```sql
select distinct user_age from users
select user_age from users group by user_age
```
上述两个语句检索的行记录应该是一样的（顺序可能不一样，没有测试过）

### 5. left join
***left join***语句是联结表的一种方式
```sql
select employees.emp_no 
from employees left join dept_manager 
on employees.emp_no = dept_manager.emp_no 
where dept_no is null
```
上述语句中，两张表通过共有字段emp_no进行联结进而组合行形成一张临时表\
***left join***会在临时表中保留其左边所有记录行（即使无法在右表中匹配共有字段，这样会将记录行中的右表字段置为空）\
接下来你就可以通过***where***对临时表中的记录行进行过滤与***select***

>上述语句也可以通过子查询实现
```sql
select emp_no
from employees
where emp_no not in (select emp_no from dept_manager)
```