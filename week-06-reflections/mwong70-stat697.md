
# Questions about Problems and Recipes



[Chapter 9.1 Macros Vars, Problem 1]
* Question (mwong70-stat697): What are some advantages of using a macro variable?
- Answer (mwong70-stat697): We can convert reference from text value. We can quickly 
and easily make updates since we make the change in only one place; meanwhile, the 
changes will appear throughout the program.



[summarize-data-using-proc-report Week 6 SAS Recipe]
* Question (mwong70-stat697): What does underscore mean in SAS? We used it in 
`drop=(_BREAK_)` and from last week `drop=(_:)`



[ddl-and-dml-sql Week 6 Python Recipe]
* Question (mwong70-stat697): Can we overwrite the update while deleting the 
original data? It seems to be thorough, but possibly cumbersome to write 2 lines of 
codes to update and then remove in dml.




***



# Recipes Exploration Results



```SAS


* print the first 3 rows from sashelp.iris;
proc report data=sashelp.iris(obs=3);
run;

* sort sashelp.iris by SepalLength, suppressing output with an "ODS Sandwich";
ods exclude all;
proc report data=sashelp.iris out=Work.iris(drop=_BREAK_);
    define
        SepalLength / order;

* summarize values for a single qualitative variable;
proc report data=sashelp.iris;
    columns
        Species
        N
    ;
    define Species / group;
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


import pandas
import saspy
sas = saspy.SASsession(results='TEXT')
iris = sas.sasdata2dataframe(table='iris', libref='sashelp')

# DDL example: define column information;
tmp = pandas.DataFrame(
    {
        'column1':str(),
        'column2':int()
    },
    index=[]
)

# DDL example: obtain column information;
print(tmp.dtypes)
print()

# DDL example: add column;
tmp['column3'] = pandas.Series({'column3':str()}, index=[])

# DDL example: modify column;
# There is no Python equivalent!

# DDL example: delete column;
del tmp['column2']

# DDL example: delete table;
del tmp

# DML example setup: define column information;
iris_clone = pandas.DataFrame()
for (column_name, column_type) in iris.dtypes.iteritems():
    iris_clone[column_name] = pandas.Series(name=column_name, dtype=column_type)
    
# DML example: obtain rows of data;
print(iris_clone)

# DML example: create rows of data from select query;
iris_clone = iris_clone.append(iris.copy())

# DML example: create row of data using values statement for all columns;
iris_clone = iris_clone.append(
    pandas.Series(['Big Flower',75,80,85,90], index=iris_clone.columns),
    ignore_index=True
)

# DML example: create row of data using values statement for select columns;
iris_clone = iris_clone.append(
    {
        'Species':'Big Flower',
        'SepalLength':75
    },
    ignore_index=True
)

# DML example: update rows of data;
iris_clone.loc[iris_clone['SepalLength'] > 64,'Species'] = 'Big Flower'

# DML example: delete rows of data;
iris_clone = iris_clone.loc[iris_clone['Species'] != 'Big Flower'].reset_index(drop=True)


```
