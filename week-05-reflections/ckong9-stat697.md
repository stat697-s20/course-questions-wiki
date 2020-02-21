
# Questions about Problems and Recipes



[SAS Textbook Chapter 5, Problem 1]
* Question (ckong9-stat697): How to create table in PROC SQL?
- Answer (ckong9-stat697): We use CREATE TABLE statement to create tables and use DESCRIBE TABLE statement to show the information about the table in the log.



[SAS Textbook Chapter 5, Problem 2]
* Question (ckong9-stat697): How can we make a new table with same structure of the existing table?
- Answer (ckong9-stat697): We can use LIKE clause to specifies which table's structure we like to copy.



[SAS Textbook Chapter 5, Problem 3]
* Question (ckong9-stat697): What are the difference in SET and VALUES clauses when adding data to existing table?



[SAS Textbook Chapter 5, Problem 4]
* Question (ckong9-stat697): How to update values in existing table?
- Answer (ckong9-stat697): We can use UPDATE statement to update the values of the rows.



[SAS Textbook Chapter 5, Problem 5]
* Question (ckong9-stat697): How can we combine all adding, dropping and modifying column commands into one single statement?
- Answer (ckong9-stat697): We can use ALTER TABLE to perform all tasks at once.



[SAS Online Training, Problem 6]
* Question (ckong9-stat697): What are the ways to connect database from SAS?
- Answer (ckong9-stat697): There are two, SQL Pass-Through and LIBNAME Statement.



[SAS Online Training, Problem 7]
* Question (ckong9-stat697): Why it is better to disconnect from ther database after obtaining the data in SQL Pass-Through?



[SAS Online Training, Problem 8]
* Question (ckong9-stat697): What is the advantage of using LIBNAME Statement?
- Answer (ckong9-stat697): It can translate PROC SQL to native DBMS SQL so that you don't need to learn multiple SQL style.



[DDL and DML SQL Queries Week 5 SAS Recipe]
* Question (ckong9-stat697): What are the differences between drop and delete in PROC SQL?



[DDL and DML SQL Queries Week 5 Python Recipe]
* Question (ckong9-stat697): Using Python, how can we modify the values in some rows?



***



# Recipes Exploration Results



```SAS
* Recipe: ddl-and-dml-sql-queries.sas ;

* original recipe;

* DDL example: define column information;
proc sql;
    create table Work.tmp
    (
         column1 char(42)
        ,column2 num
    );
quit;

* DDL example: obtain column information;
proc sql:
    secribe table Work.tmp;
quit;

* DDL example: add column;
proc sql;
    alter table Work.tmp
        add column3 char(42)
    ;
quit;

* DDL example: delete column;
proc sql;
    alter table Work.tmp
        drop column2
    ;
quit;

* DDL example: delete table;
proc sql;
    drop table Work.tmp;
quit;

* DML example setup: define column information;
proc sql;
    create table Work.iris
        like sashelp.iris
    ;
quit;

* DML example: obtain rows of data;
proc sql;
    select * from Work.iris;
    ;
quit;

* DML example: create row of data using values statement for all columns;
proc sql;
    insert into Work.iris 
        values('Big Flower', 75, 80, 85, 90)
    ;
quit;

* DML example: create row of data using values statement for select columns;
proc sql;
    insert into Work.iris
        (Species, SepalLength)
        values('Big Flower', 75)
    ;
quit;

* DML example: update rows of data;
proc sql;
    update Work.iris
        set Species='Big Flower'
        where SepalLength > 64
    ;
quit;

* DML example: delete rows of data
proc sql;
    delete from Work.iris
        where Species='Big Flower'
    ;
quit;
```



```Python
# Recipe: ddl-and-dml-sql-queries-imitated_with_pandas.py

# original recipe

import pandas
import saspy
sas = saspy.SASsession(result='TEXT')
iris = sas.sasdata2dataframe(table='iris', libref='sashelp')

# DDL example: define column information
tmp = pandas.DataFrame(
    {
        'column1'=str()
        'column2'=int()
    },
    index=[]
)

# DDL example: obtain column information
print(tmp.dtypes)
print() # print an extra blank line

# DDL example: add column
tmp['column3'] = pandas.Series({'column3':str()}, index=[])

# DDL example: modify column
# There is no Python equivlent!

# DDL example: delete column
del tmp['column2']

# DDl example: delete table
del tmp

# DML example setup: define column information
iris_clone = pandas.DataFrame()
for (column_name, column_type) in iris.dtypes.iteritems():
    iris_clone[column_name] = pandas.Series(name=column_name, dtype=column_type)

# DML example: obtain rows of data
print(iris_clone)

# DML example: create rows of data from select query
iris_clone = iris_clone.append(iris.copy())

# DML example: create row of data using values statement for all columns
iris_clone = iris_clone.append(
    pandas.Series(['Big Flower', 75, 80, 85, 90], index=iris_clone.columns),
    ignore_index=True
)

# DML example: create row of data using values statement for select columns
iris_clone = iris_clone.append(
    {
        'Species':'Big Flower',
        'SepalLength':75
    },
    ignore_index=True
)

# DML example: update rows of data
iris_clone.loc[iris_clone['SepalLength'] > 64, 'Species'] = 'Big Flower'

# DML example: delete rows of data
iris_clone = iris_clone.loc[iris_clone['Species'] != 'Big Flower'].reset_index(drop=True)

```

