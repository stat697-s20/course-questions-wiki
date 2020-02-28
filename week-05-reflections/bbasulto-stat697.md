
# Questions about Problems and Recipes

[Course Materials Question 1] 
* Question (bbasulto-stat697): What kind of numeric does the Specified Data Type DOUBLE PRECISION refer to (what kind of number)?
- Answer (bbasulto-stat697): 
	
[Course Materials Question 2] 
* Question (bbasulto-stat697): What is the difference between DESCRIBE TABLE and PROC CONTENTS?
- Answer (bbasulto-stat697): The DESCRIBE TABLE function will generate a message in the SAS log that contain column definitions even if it was created using a DATA step, while the PROC CONTENTS function will list both a table's columns and column attributes in the SAS report.
	
[Course Materials Question 3] 
* Question (bbasulto-stat697): In the initial CREATE TABLE function can you only create/define the table in the statement?
- Answer (bbasulto-stat697): No, you can use query clauses within the CREATE TABLE statement, but no report will be generated and only an output is generated.
	
[Course Materials Question 4] 
* Question (bbasulto-stat697): Can I rearrange the order of the columns when generating my new table?
- Answer (bbasulto-stat697): 

[Course Materials Question 5] 
* Question (bbasulto-stat697): Can the MODIFY clause be used to change a column's input from character to numeric?
- Answer (bbasulto-stat697): No, once the table is created you have to drop the column from the table and readd it again using the data type you need.

[Course Materials Question 6] 
* Question (bbasulto-stat697): Can a column's name be changed using an ALTER statement?
- Answer (bbasulto-stat697): No, you must either use a PROC DATA with RENAME statement or the "RENAME=" option.

[Course Materials Question 7] 
* Question (bbasulto-stat697): After you're done working with a table and use the DROP TABLE statement, do you still have your analysis generated using the table or is that also lost?
- Answer (bbasulto-stat697): 

***



# Recipes Exploration Results



```SAS

* DDL example: define column information;
proc sql;
    create table Work.tmp
    (
        column1 char(42)
       ,column2 num
    );
quit;

* DDL example: obtain column information;
proc sql;
    describe table Work.tmp;
quit;

* DDL example: add column;
proc sql;
    alter table Work.tmp
        add column3 char(42)
    ;
quit;

* DDL example: modify column;
proc sql;
    alter table Work.tmp
        modify column1 char(45)
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
quit;

* DML example: create rows of data from select query;
proc sql;
    insert into Work.iris
        select * from sashelp.iris;
quit;

* DML example: create row of data using values statement for all columns;
proc sql;
    insert into Work.iris
        values('Big Flower',75,80,85,90)
    ;
quit;

* DML example: create row of data using values statement for select columns;
proc sql;
    insert into Work.iris
        (Species,SepalLength)
        values('Big Flower',75)
    ;
quit;

* DML example: update rows of data;
proc sql;
    update Work.iris
        set Species='Big Flower'
        where SepalLength > 64
    ;
quit;

* DML example: delete rows of data;
proc sql;
    delete from Work.iris
        where Species='Big Flower'
    ;
quit;

```

[SAS_recipe Question]
* Question (bbasulto-stat697): In one portion of the example we create the table such that it containes rows with the values 75,80,85,90, but is it possible to also only give ask to rows that contain values with a certain range of values?
- Answer (bbasulto-stat697): 


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
print() #print an extra blank line

# DDL example: add column;
tmp['column3'] = pandas.Series({'column3':str()}, index=[])

# DDL example: modify column;
#There is no Python equivaqlent

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
[Python_recipe Question]
* Question (bbasulto-stat697): What is the blank index function doing in the initial DDL add column statement?
- Answer (bbasulto-stat697): 
