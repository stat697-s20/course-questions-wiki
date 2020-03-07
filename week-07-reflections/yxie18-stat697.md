
# Questions about Problems and Recipes



[TB Chapter 8, Problem 1]
* Question (yxie18-stat697): As per the example shown on Page 274 to reset the outobs option, instead of 'reset obs number', why the syntax in the example is 'reset obs= number'?



[TB Chapter 8, Problem 2]
* Question (yxie18-stat697): What are the differences between PROC SQL view and Sashelp view of one dictionary table?



[TB Chapter 8, Problem 3]
* Question (yxie18-stat697): What's the difference between the dictionary table stored in the sashelp library and the dictionary table stored in the sasuser library?



[TB Chapter 8, Problem 4]
* Question (yxie18-stat697): One the of the common situation is that, we use the prefix in the table names to represent the library, such as work.table1 or sashelp.iris, then how to understand the prefix of the table name dictionary.table? Does the prefix 'dictionary' represent the class of the table?



[TB Chapter 8, Problem 5]
* Question (yxie18-stat697): As per the situation discussed on Page 279, joining three large tables without meeting the join-matching conditions which would lead to the creation of a huge table, with LOOPS= option as a limit set to prevent the crazy loop from happening, what would be the output of this query then? Will the whole execution be halted, or the work finished before the loop reaches its limits would be displayed?



[TB Chapter 8, Problem 6]
* Question (yxie18-stat697): What's the SAS system option that's similar to the OUTOBS= option in PROC SQL?



[TB Chapter 8, Problem 7]
* Question (yxie18-stat697): If I choose to set STIMER option as a system option, would it also have effect on PROC SQL statements?



[obtain-column-information SAS Recipe]
* Question (yxie18-stat697): Is it correct that I can use the statement <list of columns obtained by copying/pasting> to replace all the select-and-copy-and-paste operations on the visualized table/excel sheets that shown in the lecture video?
- Answer (yxie18-stat697): I think so.



[ddl-and-dml-sql-queries-imitated_with_pandas Python Recipe]
* Question (yxie18-stat697): After adding the 3rd column, which was defined using str(), to the temporary table tmp, and deleted its 2nd column, I choose to print out tmp and its dtype again, and it showed that the dtype of the 3rd is float64. Why? Shouldn't it be character?



***



# Recipes Exploration Results



```SAS


* Recipe: obtain-column-information.sas ;

proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;


proc contents order=varnum data=sashelp.iris;
run;
proc sql;
    select
        <list of columns obtained by copying/pasting>
    from
        sashelp.iris
    ;
quit;


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


* Recipe: ddl-and-dml-sql-queries-imitated_with_pandas.py

import pandas
import saspy
sas = saspy.SASsession(results = 'TEXT')
iris = sas.sasdata2dataframe(table='iris', libref='sashelp')

tmp = pandas.DataFrame(
    {
        'column1':str(),
        'column2':int()
    },
    index=[]
)

print(tmp.dtypes)
print()

tmp['column3'] = pandas.Series({'column3':str()}, index=[])

del tmp['column2']

del tmp

iris_clone = pandas.DataFrame()
for (column_name, column_type) in iris.dtypes.iteritems():
    iris_clone[column_name] = pandas.Series(name=column_name, dtype=column_type)

print(iris_clone)

iris_clone = iris_clone.append(iris.copy())

iris_clone = iris_clone.append(
    pandas.Series(['Big Flower', 75, 80, 85, 90], index=iris_clone.columns),
    ignore_index=True
)

iris_clone = iris_clone.append(
    {
        'Species': 'Big Flower',
        'SepalLength': 75
    },
    ignore_index=True
)

iris_clone.loc[iris_clone['SepalLength'] > 64, 'Species'] = 'Big Flower'

iris_clone = iris_clone.loc[iris_clone['Species'] != 'Big Flower'].reset_index(drop = True)



```
