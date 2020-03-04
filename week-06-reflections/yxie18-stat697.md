
# Questions about Problems and Recipes



[TB Chapter 23, Problem 1]
* Question (yxie18-stat697): Why is it more efficient to use sequential access for a large subset. Isn't it always more efficient to use indexed access for query? Does it have something to do with the machine memory or the way of loading?(Not sure if that was already anwsered in the book but at least not answered during Ch23 4-5)



[TB Chapter 23, Problem 2]
* Question (yxie18-stat697): When multiple indexes exist, SAS selects the one that produces the fewest qualified observations - does it mean that efficiency could be over-estimated in this case, as the judgement is based on the index that would consume least?



[TB Chapter 21, Problem 3]
* Question (yxie18-stat697): Is there any way that I can change the increments of centile from 5% to 10% or any other percentage?



[TB Chapter 9, Problem 4]
* Question (yxie18-stat697): On the %LET statement examples table on Page295, on the last row, why the variable name is 'varlist' rather than '&x'? Does it have something to do with the usage of the symbol ampersand?
- Answer (yxie18-stat697): Because on the above row, by %LET statement the char string 'varlist' is assigned to the variable x as its value. It also means that when giving a name (not the value) to a variable, referring to a macro variable is also allowed. 



[TB Chapter 9, Problem 5]
* Question (yxie18-stat697): For PROC SQL, is the quit statement also an example of step boundaries?
- Answer (yxie18-stat697): I think so.



[TB Chapter 9, Problem 6]
* Question (yxie18-stat697): Macro variables can only be character strings, what if I want to assign a numeric value to a variable that would be available in the global environment and could be changed easily?



[TB Chapter 9, Problem 7]
* Question (yxie18-stat697): Besides for macro variables, is there any other situation in writing SAS code that single quote marks and double quote marks cannot be used interchangeably?



[sas_recipe-summarize-data-using-proc-report SAS Recipe]
* Question (yxie18-stat697): For the last block of codes, where the total is calculated by adding up the value of 2nd, 3rd and 4th columns, is it actually return the total number of rows under each number of SepalLength and each kind of species? 



[sas_recipe-summarize-data-using-proc-report SAS Recipe]
* Question (yxie18-stat697): Any difference between 'computed' for PROC report and 'calculated' for PROC SQL?



[ddl-and-dml-sql-queries-imitated_with_pandas Python Recipe]
* Question (yxie18-stat697): Just tried to remove the line 'index=[]' from the statement of creating a tmp as a data frame, and it couldn't work then. Why is it so necessary to give arguments to index?



***



# Recipes Exploration Results



```SAS


* Recipe: summarize-data-using-proc-report.sas ;

proc report data=sashelp.iris(obs=3);
run;

ods exclude all;
proc report data=sashelp.iris out=Work.iris(drop=_BREAK_);
    define
        SepalLength / order;
run;
ods exclude none;

proc report data=sashelp.iris;
    columns
        Species
        N
    ;
    define Species / group;
    define N / 'Number of Irises';
run;

proc report data=sashelp.iris;
    columns
        Species
        SepalLength = SepalLength_Min
        SepalLength = SepalLength_Median
        SepalLength = SepalLength_Max
    ;
    define Species / group;
    define SepalLength_Min / min 'Minimum Sepal Length';
    define SepalLength_Median / median 'Median Sepal Length';
    define SepalLength_Max / max 'Maximum Sepal Length';
run;

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
