
# Questions about Problems and Recipes

[Course Materials Question 1] 
* Question (bbasulto-stat697): What is the difference between PROC PRINT and PROC SQL?
- Answer (bbasulto-stat697): While both commands can calculate column sums, PROC SQL can calculate row statistics as well as manipulate data and create a new dataset in the same step.
	
[Course Materials Question 2] 
* Question (bbasulto-stat697): Is there a set dataset size that you can use as a rule of thumb to use to determine which type of summerization method will be best or is it more based on how many variables in your dataset you want to use in your summary?
- Answer (bbasulto-stat697): 
	
[Course Materials Question 3] 
* Question (bbasulto-stat697): Which procedure or step should you use to summarize a dataset and group by ONE variable?
- Answer (bbasulto-stat697): The most efficient method is to use a DATA step with a BY group processing statement
	
[Course Materials Question 4] 
* Question (bbasulto-stat697): When using the macro variable %let to define a variable for your program, do you need to add it to every PROC or DATA step?
- Answer (bbasulto-stat697): No, the macro variable %let is a global statement.

[Course Materials Question 5] 
* Question (bbasulto-stat697): Can the macro variable %let be used to calculate a value for your variable?
- Answer (bbasulto-stat697): No, the macro variable %let can not be used for mathematical statements/expressions.

[Course Materials Question 6] 
* Question (bbasulto-stat697): What does it mean when the SAS log contains an error like "* + % ;"?
- Answer (bbasulto-stat697): 

[Course Materials Question 7] 
* Question (bbasulto-stat697): When setting multiple macro variables in a row, can you seperate them and or list them in the output to make them easier to read?
- Answer (bbasulto-stat697): 

***



# Recipes Exploration Results



```SAS
* Examples;

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
        species
        N
    ;
    define Species / group;
    define N / "Number of Species";
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

[SAS_recipe Question]
* Question (bbasulto-stat697): For the last example in the recipe, are we able to use the _c2_. _c3_, and _c4_ labels since we have already defined the column names under "Columns"?
- Answer (bbasulto-stat697):


```Python


[place your Python recipe explorations here, and delete this line]



```
