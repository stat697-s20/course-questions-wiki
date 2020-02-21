
# Questions about Problems and Recipes


[DDL DML SQL SAS Recipe, Problem 1]
* Question (mwong70-stat697): Why do we use proc sql and quit; at each example? Can't we just combine the code and separately run it in kernel?


[DDL DML SQL Python Recipe, Problem 2]
* Question (mwong70-stat697): Why does ( and { have different auto-spacing in JupyterLab?


[DDL DML SQL Python Recipe, Problem 3]
* Question (mwong70-stat697): Why does double indexing using [ [' '] ] works here, but when it's about quotation marks, python is so particular?


***


# Recipes Exploration Results


```SAS
/* Approach: Use DDL and DML SQL queries.
DDL Recipes: */
/* DDL example: define column information for a table; */
proc sql;
    create table Work.tmp as
    (
         column1 char(42)
        ,column2 num
    );
quit;

/* DDL example: obtain column information for a table; */
proc sql; 
    describe table Work.tmp; * describe table <table name>
quit;
    
/* DDL example: add new column information for a table; */
proc sql;
    alter table Work.tmp
        add column3 char(42)
    ;
quit;

/* DDL example: modify column information for a table; */
proc sql;
    alter table Work.tmp
        modify column1 char(54)
    ;
quit;

/* DDL example: delete column information for a table; */
proc sql;
    alter table Work.tmp
        drop column2
    ;
quit;

/* DDL example: delete entire table; */
proc sql;
    drop table Work.tmp;
quit;


/* DML Recipes:
DML example setup: define column information; */
proc sql;
    create table Work.iris
        like sashelp.iris
    ;
quit;

/* DML example: obtain rows of data from a table; */
proc sql;
    select *
        from Work.iris
    ;
quit;

/* DML example: create rows of data in a table using a select query; */
proc sql;
    insert into Work.iris
        select * 
            from sashelp.iris
    ;
quit;

/* DML example: create rows of data in a table using value statement, giving 
tuples of */
proc sql;
    insert into Work.iris
        values('Big Flower',75,80,85,90)
    ;
quit;

/* DML example: create rows of data in a table using value statement, giving 
tuples of values for specified columns, with values in all other columns set to 
missing for the new rows being created; */
proc sql;
    insert into Work.iris
        (Species,SepalLength)
        values('Big Flower',75)
    ;
quit;

/* DML example: update rows of data in a table; */
proc sql;
    update Work.iris
        set Species='Big Flower'
        where SepalLength > 64
    ;
quit;

/* DML example: delete rows of data in a table; */
proc sql;
    delete from Work.iris
        where Species='Big Flower'
    ;
quit;


/*
Notes:
(1) These examples illustrate the eight main queries available in proc sql, 
along with their possible variations. These are also the 8 main queries defined 
in most SQL-based relational database management systems (RDBMSes).


(2) The first four queries (create-table, describe-table, alter-table, and 
drop-table) are used as so-called data-definition language (DDL), meaning they 
define, obtain, or modify column information in a table, or delete a table 
entirely.


(3) The output of a describe-table query is sometimes called the 
"DDL for the table" since it's what would be put into a create-table query to 
create a new table with the same column properties but no rows of data.


(4) However, note that when specifying the column type in a create-table query, 
SAS only supports character columns and numeric columns, even through most 
RDBMSes allow for many other possible column types in order to allow the size of 
data on disk to be minimized as much as possible (e.g., a list for MySQL is 
available at https://dev.mysql.com/doc/refman/8.0/en/data-types.html). This is 
because Base SAS only supports character and numeric types; e.g., even date and 
time values are really just numeric values with formatting applied to them.


(5) On the other hand, the last four queries (select, insert-into, update, and 
delete-from) are used as so-called data-manipulation language (DML), meaning 
they obtain, create, modify, or delete the rows of data in a table.


(6) Together, these eight queries are the basic toolkit for database 
administration, and it's not uncommon for database-maintenance records to be 
given as a sequence of queries since the code itself specifies exact steps with 
more precision and fewer characters that a paragraph of text.


(7) In addition, it's also common for data to be distributed as text files with 
the extension .sql and with file contents consisting of one or more create-table 
queries followed by many insert-into queries with values statements used to 
create tables row-by-row. Such files are typically larger in size than CSV 
files, but they also remove any ambiguity about the data types for columns, 
allowing a table of data from one RDBMS to be exactly moved or copied to another 
RDBMS.
*/

```


```Python
# Approach: Use DDL and DML SQL pandas operations.
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