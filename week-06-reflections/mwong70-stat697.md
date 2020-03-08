# Questions about Problems and Recipes



[SAS SQL Essential Lesson 3, Problem 1]
* Question (mwong70-stat697): What are 3 types of joins in this lesson?
- Answer (mwong70-stat697): inner (AND), (left/right/full) outer, and complex.

SELECT col_name1, col_name2s
    FROM sq.smallcustomer inner join sq.smalltransaction
    ON smallcustomer.AccountID = smalltransaction.AccountID;
QUIT;



[SAS SQL Essential Lesson 3, Problem 2]
* Question (mwong70-stat697): Why do we perform join?
- Answer (mwong70-stat697): To create horizontal join and create new columns. We
sort by the primary key.
 


[SAS SQL Essential Lesson 3, Problem 3]
* Question (mwong70-stat697): What’s a Cartesian product? What kind of properties
does it have that we need to make two tables a Cartesian product?
- Answer (mwong70-stat697): Something that must have matching IDs. Example:
PROC SQL number;
    SELECT *
    FROM sq.smallcustomer, sq.smalltransaction;
QUIT;



[SAS SQL Essential Lesson 3, Problem 4]
* Question (mwong70-stat697): Can we join other types of data besides tables and
columns?



[SAS Certification Prep Guide 4th Edition Chapter 9, Problem 5]
* Question (mwong70-stat697): What’s a macro variable? Why is it important?
- Answer (mwong70-stat697): Don’t know what it is, but an example is literal 
string. It can be useful for text and variable, but it is limited to 65k length.



[SAS Certification Prep Guide 4th Edition Chapter 23, Problem 6]
* Question (mwong70-stat697): List the procedures covered in this section.
- Answer (mwong70-stat697): means, summary, tabulate, report



[SAS Certification Prep Guide 4th Edition Chapter 23, Problem 7]
* Question (mwong70-stat697): What’s a Cartesian product? What kind of properties
- Answer (mwong70-stat697): Something that must have matching IDs. Example:



***



# Recipes Exploration Results



```SAS
* Recipe: summarize-data-using-proc-report.sas;

* print the first 3 rows from sashelp.iris;
proc report data=sashelp.iris(obs=3);
run;

* sort sashelp.iris by SepalLength, suppressing output with an "ODS Sandwich";
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
run; /* wish I could omit empty obs., code worked */
```


```Python
# Recipe: ddl-and-dml-sql-queries-imitated_with_pandas.py
import pandas
import saspy
sas = saspy.SASsession(results='TEXT')
iris = sas.sasdata2dataframe(table='iris', libref='sashelp')

# DDL example: define column information
tmp = pandas.DataFrame(    # create a temporary table 
    # so not to alter raw
    {
        'column1':str(),
        'column2':int()
    },
    index=[]
)

# DDL example: obtain column information
print(tmp.dtypes)
print() # print an extra blank line

# DDL example: add column
tmp['column3'] = pandas.Series({'column3':str()}, index=[])

# DDL example: modify column
# There is no Python equivalent!

# DDL example: delete column
del tmp['column2'] # removes column2 per tempore

# DDL example: delete table
del tmp

# DML example setup: define column information
iris_clone = pandas.DataFrame()
for (column_name, column_type) in iris.dtypes.iteritems();
    iris_clone[column_name = pandas.Series(name=column_name, dtype=column_name)]

# DML example: obtain rows of data
print(iris_clone)

# DML example: create rows of data from select query
iris_clone = iris_clone.append(iris.copy())

# DML example: create row of data using values statement for all columns
iris_clone = iris_clone.append(
    pandas.Series(['Big Flower',75,80,85,90], index = iris_clone.columns),
    ignore_index=True
)

# DML example: create row of data using values statement for select columns
iris_clone = iris_clone.append(
    {
        'Species':'Big Flower',
        'SepalLength':75
    },
    ignore_index=True
) # Error: Statement is not valid or out of proper order

# DML example: update rows of data
iris_clone.loc[iris_clone['SepalLength'] > 64, 'Species'] = 'Big Flower'
# identify if column has numeric value > 64 in column SepalLength

# DML example: delete rows of data
iris_clone = iris_clone.loc[iris_clone['Species'] != 'Big Flower'].reset_index(drop=True)
```
