
# Questions about Problems and Recipes



[TB Chapter 5, Problem 1]
* Question (yxie18-stat697): There are some situations that parentheses are required to enclose the entire set of values/specifications, such as in CREATE TABLE statement or the VALUES clause in INSERT INTO statement, but sometimes parentheses are not required to 'enclose the specifications', such as the creating tables from a query. Any reasons behind these syntax rules?



[TB Chapter 5, Problem 2]
* Question (yxie18-stat697): Under what circumstances should we prefer using SET clause over VALUES cluase on inserting rows, and under what circumstances should we prefer the other way round?



[TB Chapter 5, Problem 3]
* Question (yxie18-stat697): How can I apply the PRIMARY KEY integrity constraits to conduct one of my tasks that had been done during the past weeks - to ensure than the unique id is unique and not missing?



[TB Chapter 5, Problem 4]
* Question (yxie18-stat697): What's the point of setting UNDO_POLICY option to be OPTIONAL as it would just process as if it had been set to NONE if it cannot be done reliably?



[TB Chapter 5, Problem 5]
* Question (yxie18-stat697): Under what circumstanced would we choose to set contraintS to a tables/columns first but also set the UNDO_POLICY option to NONE?



[TB Chapter 5, Problem 6]
* Question (yxie18-stat697): What's the difference between one-level name and two-level name? (Mention on Page 197)
- Answer (yxie18-stat697): Use a one-level name when the data set is in a temporary library, such as USER or WORK. Use a two-level name when the data set is in some other permanent library you have established. A two-level name consists of both the libref and the data set name. A one-level name consists of just the data set name.



[TB Chapter 5, Problem 7]
* Question (yxie18-stat697): How can I make use of integrity contraints to further improve data cleaning process of my current and future data-analysis projects?



[ddl-and-dml-sql-queries SAS Recipe]
* Question (yxie18-stat697): What good will it do to split a considerbly large number of SAS SQL queries into many small and self-contained proc sql steps?
- Answer (yxie18-stat697): Making it easier to debug and modify codes later.



[ddl-and-dml-sql-queries-imitated_with_pandas Python Recipe]
* Question (yxie18-stat697): Is it the case that all the dataframes with pandas library will be recognized as object as data types? As I tried to create a dataframe with both of the two columns to be int(), yet the result of printing dtype is still 'object'.



***



# Recipes Exploration Results



```SAS


* Recipe: ddl-and-dml-sql-queries.sas ;

proc sql;
    create table Work.tmp
    (
        column1 char(42)
        , column2 num
    );
quit;

proc sql;
    describe table Work.tmp;
quit;

proc sql;
    alter table Work.tmp
        add column3 char(42)
    ;
quit;

proc sql;
    alter table Work.tmp
        modify column1 char(54)
    ;
quit;

proc sql;
    alter table Work.tmp    
        drop column2
    ;
quitl

proc sql;
    drop table Work.tmp
    ;
quit;

proc sql;
    create table Work.iris
        like sashelp.iris
    ;
quit;

proc sql;
    select *
    from Work.iris
    ;
quit;

proc sql;
    insert into Work.iris   
        select * from sashelp.iris
    ;
quit;

proc sql;
    insert into Work.iris  
        values('Big Flower', 75, 80, 85, 90)
    ;
quit;

proc sql;
    insert into Work.iris
        (Species, SepalLength)
        values ('Big Flower', 75)
    ;
quit;

proc sql;
    update Work.iris    
        set Species = 'Big Flower'
        where SepalLength > 64
    ;
quit;

proc sql;
    delete from Work.iris
        where Species = 'Big Flower'
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
