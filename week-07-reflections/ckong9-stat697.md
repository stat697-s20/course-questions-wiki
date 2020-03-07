
# Questions about Problems and Recipes



[SAS Textbook Chapter 8, Problem 1]
* Question (ckong9-stat697): Why we have to specifying SQL Options in SAS?
- Answer (ckong9-stat697): You can control the output results that you want to see.


[SAS Textbook Chapter 8, Problem 2]
* Question (ckong9-stat697): What are the options covered in this chapter?
- Answer (ckong9-stat697): There are INOBS, OUTBOS, DOUBLE|NODOUBLE, FLOW|NOFLOW|FLOW=n|FLOW=n m, STIMER|NOSTIMER.



[SAS Textbook Chapter 8, Problem 3]
* Question (ckong9-stat697): Why we want to test and evaluating performance in SAS?



[SAS Textbook Chapter 8, Problem 4]
* Question (ckong9-stat697): What is dictionary tables in SAS?



[SAS Textbook Chapter 8, Problem 5]
* Question (ckong9-stat697): Why we use dictionary tables in SAS?
- Answer (ckong9-stat697): We can monitor and manager SAS sessions.


[SAS Textbook Chapter 8, Problem 6]
* Question (ckong9-stat697): What are the differences in using PROC SQL dictionary.column and PROC PRINT vcolumn?



[SAS Textbook Chapter 8, Problem 7]
* Question (ckong9-stat697): Why we use LOOPS function?
- Answer (ckong9-stat697): The limit can prevent queries from consuming excessive resources.



[SAS Textbook Chapter 8, Problem 8]
* Question (ckong9-stat697): What are the use of ERRORSTOP?
- Answer (ckong9-stat697): We can make PROC SQL stop executing if it encounters an error.



[DDL and DML SQL Queries Week 6 SAS Recipe]
* Question (ckong9-stat697): What are the processing speed for the three approaches?


[DDL and DML SQL Queries Week 6 Python Recipe]
* Question (ckong9-stat697): Does SASPy allow connecting to SQL server?



***



# Recipes Exploration Results



```SAS
* Recipe: summarize-data-using-proc-report.sas ;

* original recipe;

* Example For Approach 1;

proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;


* Example For Approach 2;
proc contents order=varnum data=sashelp.iris;
run;
proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;


* Exanoke Fir Approach 3;
proc sql;
    select
        name
    from
        dictionary.columns
    where
        lowcase(libname) = 'sashelp'
    and
        lowcase(memname) = 'iris'
    ;
quit;
proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
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
