
# Questions about Problems and Recipes

[Course Materials Question 1] 
* Question (bbasulto-stat697): For commands like "IS MISSING" and "IS NULL" where one is a SAS enhancment and the other is an ANSI standard, is it better to be in the habbit of using the command that is an ANSI standard so that it's easier to work with various SQL software?
- Answer (bbasulto-stat697): 
	
[Course Materials Question 2] 
* Question (bbasulto-stat697): Does the sounds like operator (=*) just select words that start with the same letter and contain any letters in the sounds like statement?
- Answer (bbasulto-stat697):
	
[Course Materials Question 3] 
* Question (bbasulto-stat697): What is the difference between Inner Join and Outer Join?
- Answer (bbasulto-stat697): Inner Join combines only matching rows accross all tables while Outer combines all rows in all tables whether they match or not.
	
[Course Materials Question 4] 
* Question (bbasulto-stat697): What are the variations of the Outer Join function?
- Answer (bbasulto-stat697): Left Join combines all rows from the left table and the matching ones from the right. Right Join combines all rows from the right table and the matching ones from the left. Full Join combines all rows regardless of whether or not they match. 

[Course Materials Question 5] 
* Question (bbasulto-stat697): Where in the PROC SQL statement does the in-line view go?
- Answer (bbasulto-stat697): In-line views are a nested query that is specified in the FROM clause of the outer query. In-line views are only temporary.

[Course Materials Question 6] 
* Question (bbasulto-stat697): How many tables can an inner join combine at once?
- Answer (bbasulto-stat697): An inner join can combine upto 256 tables or views at once.

[Course Materials Question 7] 
* Question (bbasulto-stat697): What is the benefit of an Aliase?
- Answer (bbasulto-stat697): An aliase allows you to temporarily shorten the name of a table and make it easier to work with.



***



# Recipes Exploration Results



```SAS

filename work_dir "%sysfunc(getoption(work))//us_data.sas7bdat";
proc http
        method="get"
        url="http://tinyurl.com/sashelp-us-data"
        out=work_dir
    ;
run;

proc sql number;
    select
        coalesce(A.statename, B.statename) as statename
        ,A.region
        ,B.number_of_zipcodes
    from
        work.us_data as A
        full join
        (
            select
                statename
                , count(*) as number_of_zipcodes
            from
                sashelp.zipcode
            group by
                statename
        ) as B
        on
            A.statename = B.statename
    order by
        number_of_zipcodes desc
    ;
quit;


```
[SAS_recipe Question]
* Question (bbasulto-stat697): How do you access the explorer files when using the new / SAS Universtiy version of Jupyter?
- Answer (bbasulto-stat697):


```Python

import pandas
import saspy
sas = saspy.SASsession(results='TEXT')

us_data_df = pandas.read_sas ('http://tinyurl.com/sashelp-us-data', format = 'sas7bdat', encoding='latin-1')

zipcode_df = sas.sasdata2dataframe(table='zipcode', libref='sashelp')
zipcode_agg_by_statename = zipcode_df.groupby('STATENAME').size()
zipcode_agg_by_statename_df = zipcode_agg_by_statename.to_frame('number_of_zipcodes').reset_index()

us_data_w_zipcode_df = us_data_df.merge(zipcode_agg_by_statename_df, how='outer', on='STATENAME')
us_data_w_zipcode_subset_df = us_data_w_zipcode_df[['STATENAME', 'REGION', 'number_of_zipcodes']]
us_data_w_zipcode_sorted_df =us_data_w_zipcode_subset_df.sort_values(by='number_of_zipcodes', ascending=False)

print(us_data_w_zipcode_sorted_df)


```
[Python_recipe Question]
* Question (bbasulto-stat697): Are "True" / "False" statements case sensitive in Python?
- Answer (bbasulto-stat697): Yes

