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