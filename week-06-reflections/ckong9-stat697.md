
# Questions about Problems and Recipes



[SAS Textbook Chapter 23, Problem 1]
* Question (ckong9-stat697): What are the difference between using PROC PRINT and PROC SQL in generating detailed report?
- Answer (ckong9-stat697): Generally, PROC PRINT uses fewer resources than PROC SQL.



[SAS Textbook Chapter 23, Problem 2]
* Question (ckong9-stat697): What comparing functions can we use to summarize data?
- Answer (ckong9-stat697): We can use PROC MEANS, PROC SUMMARY, PROC REPORT, PROC TABULATE, or PROC SQL and DATA step with PROC SORT.



[SAS Textbook Chapter 23, Problem 3]
* Question (ckong9-stat697): What is the use of NWAY option in PROC MEANS?



[SAS Textbook Chapter 9, Problem 4]
* Question (ckong9-stat697): What does SAS marco variables do?
- Answer (ckong9-stat697): It can substitute text in the SAS program. (Like assigning values variables in other programming languages)



[SAS Textbook Chapter 9, Problem 5]
* Question (ckong9-stat697): What automatic marco variables we can apply in SAS program?
- Answer (ckong9-stat697): Examples like Date, Time, day of the week, types of operation system, version of SAS used etc.



[SAS Textbook Chapter 9, Problem 6]
* Question (ckong9-stat697): What are the advantages of displaying marco variable values in SAS Log?



[SAS Online Training, Problem 7]
* Question (ckong9-stat697): What is natural join?
- Answer (ckong9-stat697): It automatically selects columns from each table to use in determining matching rows.



[SAS Online Training, Problem 8]
* Question (ckong9-stat697): How to use reflexive joins?



[DDL and DML SQL Queries Week 6 SAS Recipe]
* Question (ckong9-stat697): What are the advantages of using define in SAS?


[DDL and DML SQL Queries Week 6 Python Recipe]
* Question (ckong9-stat697): What is the data type after using panda.DataFrame?



***



# Recipes Exploration Results



```SAS
* Recipe: summarize-data-using-proc-report.sas ;

* original recipe;

* print the first 3 rows from sashelp.iris;
proc report data=sashelp.iris(obs=3);
run;

*sort sashelp.iris by SepalLength, suppressing output with an "ODS Sandwich";
ods exclude all;
proc report data=sashelp.iris out=Work.iris(drop=_BREAK_);
    define
        SepalLength / order;
run;
ods exclude none;

* summarize values for a single qualitative variable;
proc report data=sashelp.iris;
    columns
        Species
        name
    ;
    define Species / group
    define N / "Number of Irises";
run;

* summarize values for a single quantitative variable;
proc report data=sashelp.iris;
    columns
        Species
        SepalLength = SepalLength_Min
        SepalLength = SepalLength_Median
        SepalLength = SepalLength_Max
    ;
    define Species / group;
    define SepalLength_Min / min "Minimum Sepal Length";
    define SepalLength_Median / median "Median Sepal Length";
    define SepalLength_Max / max "Maximum Sepal Length";
run;

* summarize values for two qualitative variables using a two-way table;
proc report data=sashelp.iris;
    columns
        SepalLength
        Species
        Total
    ;
    define SepalLength / group;
    define Species / across;
    define Total / computed;

    compute Total;
        Total = sum(_c2_, _c3_, _c4_);
    endcomp;

    rbreak after / summarize;
run;
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
