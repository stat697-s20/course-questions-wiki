
# Questions about Problems and Recipes



[Course Materials Question 1] 
* Question (bbasulto-stat697): Why don't you need a semicolon after each statement line when usuing PROC SQL? 
- Answer (bbasulto-stat697): 
	
[Course Materials Question 2] 
* Question (bbasulto-stat697): Various different R packages (like tidyr) have 'cheat sheets' available online with examples of each command, do those exist for SAS SQL?
- Answer (bbasulto-stat697): I was only able to find one here that was not created by SAS (https://intellipaat.com/mediaFiles/2019/02/SQL-Basic-Cheat-Sheet-1.png) , but it's not as helpful as the ones for R.
	
[Course Materials Question 3] 
* Question (bbasulto-stat697): What is the command 'as' used for in SAS? 
- Answer (bbasulto-stat697): The keyword AS is used to assign the desired name to the column you are creating.
	
[Course Materials Question 4] 
* Question (bbasulto-stat697): How do you preview your data in SAS SQL?
- Answer (bbasulto-stat697): By setting 'outobs=' to a small managable number (i.e. 3 or 5) your output will have all columns for the number of rows or observations specified.

[Course Materials Question 5] 
* Question (bbasulto-stat697): How do you combine more than one table to make one?
- Answer (bbasulto-stat697): By selecting all data tables in the SELECT command along with desired column(s), and again selecting the data tables again in the FROM statement.

[Course Materials Question 6] 
* Question (bbasulto-stat697): What does the function count(*) return?
- Answer (bbasulto-stat697): It returns the total number of rows in a group or in a table.

[Course Materials Question 7] 
* Question (bbasulto-stat697): What does the funtion count(column_name) return?
- Answer (bbasulto-stat697): It returns the count of all nonmissing entries in the column specified.



***



# Recipes Exploration Results



```SAS


[SAS_recipe] 

* immitating proc print;

proc sql outobs=3;
    select *
    from sashelp.iris
    ;
quit;



* example of immitating proc sort and proc print - also adds column of row numbers;

proc sql outobs=5 number;
    select *
    from sashelp.iris
    order by SepalLength
    ;
quit;


* will count and group by values of species - immitating proc freq - did not req a quit command - as is an alias command that will give the result of a calculation;
proc sql;
    select Species, count(*) as Number_of_Irises
    from sashelp.iris
    group by Species
    ;
    *immitating proc means;
    select
         Species
        ,min(SepalLength) as Minumum_Sepal_Length
        ,median(SepalLength) as Median_Sepal_Length
        ,max(SepalLength) as Maximum_Sepal_Length
    from
        sashelp.iris
    group by 
        Species
    ;
quit;



[SAS_recipe]
* Question (bbasulto-stat697): If SAS SQL is limited by your memory, does that effect the reliability or accuracy of your output results?
- Answer (bbasulto-stat697): 



```



```Python


[Python_recipe]

# calls package 'pandas' that contains tools needed for analysis
import pandas
# reads data into python
iris = pandas.read_csv('http://tinyurl.com/stat697-iris')

#print the first 3 rows from the iris dataset
iris.head(3)

#print the first 5 rows of iris dataset after sorting by sepal_length
iris_sorted_by_sepal_length = iris.sort_values(by=['sepal_length'])
iris_sorted_by_sepal_length.head(5)

#summarize values for qualitative and quantitative variables

#print freq of each species in iris dataset
print(iris['species'].value_counts())

#print median of sepal_length by species in iris dataset
print(iris.groupby('species')['sepal_length'].agg(['min', 'median', 'max']))


[Python_recipe]
* Question (bbasulto-stat697): What is a panda?
- Answer (bbasulto-stat697):  Pandas are an open source package developed for Python that contains tool for data analysis and manipulation. 




```
