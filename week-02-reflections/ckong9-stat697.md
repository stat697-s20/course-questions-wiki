# Questions about Problems and Recipes



[SAS Online Training, Problem 1]
* Question (ckong9-stat697): What will be the major difference between PROC SQL and SQL itself?
- Answer (ckong-stat697): In PROC SQL it does not implement COMMIT, ROLLBACK and GRANT because SAS itself is not designed primarily as a database management system. These three commands are mainly use for editing/managing the database content which in PROC SQL does not require to have.



[SAS Online Training, Problem 2]
* Question (ckong9-stat697): How SAS convert time value, date value and datetime value to human readable value?



[SAS Online Training, Problem 3]
* Question (ckong9-stat697): How to exclude to rows with missing values?
- Answer (ckong9-stat697): We can first use "WHERE col-name IS NULL" or "WHERE col-name IS NOT NULL". Also, we can use "WHERE col-name IS MISSING" or "WHERE col-name IS NOT MISSING" to exclude the missing value.



[SAS Online Training, Problem 4]
* Question (ckong9-stat697): How to classify values into more human understandable wording like the classification of obesity in terms of BMI?
- Answer (ckong9-stat697): We can use "CASE ... WHEN" to set condition for different label. We can also use the calculated value to find a more accurate of classification since the calculation of BMI involves both the height and weight of a person.



[SAS Textbook, Problem 5]
* Question (ckong9-stat697): How to we find names starting with specific characters or having specific characters?
- Answer (ckong9-stat697): We can use LIKE operators where "_" and "%" can be used to represents any single character and any sequence of zero or more characters respectively. Hence, we can easily find names, for example start with 'A', or ends with 'son'.



[SAS Textbook, Problem 6]
* Question (ckong9-stat697): Why the basic PROC SQL step for creating a table from a query result must follow "SELECT", "FROM", "WHERE", "GROUP BY", "ORDER BY"?



[SAS Textbook, Problem 7]
* Question (ckong9-stat697): What does the function "VALIDATE" use for?



[SAS Textbook, Problem 8]
* Question (ckong9-stat697): What are the types of subqueries?
- Answer (ckong9-stat697): There are two types of subqueries, noncorrelated and correlated.




[Summarize Data using SQL Week 2 SAS Recipe]
* Question (ckong9-stat697): What should we do if we would like to classify the sepal length into categories like "Long", "Average", "Short" etc?


[Summarize Data using Panda Week 2 Recipe]
* Question (ckong9-stat697): In Python, using the function "iris.head(3)", is the python process all the data rows and print the first three, or it will stop immediately after process the first three rows?



***



# Recipes Exploration Results



```SAS
* Recipe: summarize-data-using-sql.sas ;

* original recipe;

* immitating proc print;
proc sql outobs=3;
	select *
	from sashelp.iris
	;
quit;

* immitating proc sort and proc print;
proc sql outobs=5 number;
	select *
	from sashelp.iris
	order by SepalLength
	;
quit;

proc sql;
* immitating proc freq;
	select Species, count(*) as Number_of_Irises
	from sashelp.iris
	group by Species
	;
	* immitating proc means;
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
quit;

```



```Python
# Recipe: summarize-data-using-panda.py

# original recipe

import pandas

iris = pandas.read_csv('https://tinyurl.com/stat697-iris')

#print the first 3 rows from the iris dataset
iris.head(3)

#print the first 5 rows of iris dataset after sorting by sepal_length
iris_sorted_by_sepal_length = iris.sort_values(by=['sepal_length'])
iris_sorted_by_sepal_length.head(5)

#summarize values for qualitative and quantitative variables

#print frequency of each species in iris dataset
print(iris['species'].value_counts(5))

#print median of speal_length by species in iris dataset
print(iris.groupby('species')['sepal_length'].agg(['min','median','max']))

```
