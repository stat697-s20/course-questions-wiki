# Questions about Problems and Recipes



[TB Chapter 2, Problem 1]
* Question (yxie18-stat697): When joining tables, the columns in the join condition must be of the same type. Is it necessary to give a check everytime before starting a join query? As it happened to me when I was writing R codes that some variables seemed to be numeric were actually with their class being character.
- Answer (yxie18-stat697): No harm to check it out first. Using PROC CONTENTS DATA statement could be one of the options.



[TB Chapter 2, Problem 2]
* Question (yxie18-stat697): Apart from HAVING clause goes with GROUP BY clause, which means it would be applied on group data, What's the other differences on the usage of WHERE clause and HAVING clause?



[TB Chapter 2, Problem 3]
* Question (yxie18-stat697): How to use PROC IMPORT statement to import txt file into SAS?
- Answer (yxie18-stat697): Make it clear that dbms = dlm and delimiter = '09'x.



[TB Chapter 2, Problem 4]
* Question (yxie18-stat697): In what ways can I 'wisely' utilize SAS Log to help myself code better?



[TB Chapter 2, Problem 5]
* Question (yxie18-stat697): When writing LIKE clause, Can I use regular expression syntax in SAS PROC SQL?
- Answer (yxie18-stat697): Yes. Use PRXMATCH function.



[TB Chapter 2, Problem 6]
* Question (yxie18-stat697): Apart from the issue of remerge, is there any other reason against using 'CALCULATED' instead of writing subqueries?



[TB Chapter 2, Problem 7]
* Question (yxie18-stat697): It says that the count function is the only summary function that can use * as argument. Why can't I use * as the argument of sum or avg function? 



[summarize-data-using-sql SAS Recipe]
* Question (yxie18-stat697): If we have multiple columns following the GROUP BY statement, how can the order of columns listed affect the outputs?


[summarize-data-using-pandas Python Recipe]
* Question (yxie18-stat697): As for the by argument of sort_values function, why it needs to use brackets instead of parentheses for the list of names to sort by?



***



# Recipes Exploration Results



```SAS
* Recipe: summarize-data-using-sql.sas ;

proc sql outobs = 3;
    select
        *
    from
        sashelp.iris
    ;
quit;

proc sql outobs = 5 number;
    select
        *
    from
        sashelp.iris
    order by
        SepalLength
    ;
quit;

proc sql;
    select
        Species
        ,count(*) as Number_of_Irises
    from
        sashelp.iris
    group by
        Species
    ;

    select
        Species
        ,min(SepalLength) as Minimum_Sepal_Length
        ,median(SepalLength) as Median_Sepal_Length
        ,max(SepalLength) as Maximum_Sepal_Length
    from
        sashelp.iris
    group by
        Species
    ;
quit；

```



```Python
# Recipe: summarize-data-using-pandas.py

import pandas

iris = pandas.read_csv('https://tinyurl.com/stat697-iris')
iris.head(3)
iris_sorted_by_sepal_length = iris.sort_values(by=['sepal_length'])
iris_sorted_by_sepal_length.head(5)
print(iris['species'].value_counts())
print(iris.groupby('species')['sepal_length'].agg(['min','median','max']))


```
