
# Questions about Problems and Recipes



[SAS Textbook Chapter 2, Problem 1]
* Question (ckong9-stat697): What do we need to aware of when using the function COUNT ?
- Answer (ckong9-stat697): The function COUNT only counts with values. It will ignore missing values.



[SAS Textbook Chapter 2, Problem 2]
* Question (ckong9-stat697): How can we count uniqle values using function COUNT?
- Answer (ckong9-stat697): We can use COUNT(DISTINCT <columnname>) to count.


[SAS Textbook Chapter 2, Problem 3]
* Question (ckong9-stat697): What is the use of ANY operator in subquery?
- Answer (ckong9-stat697): It selects the values that pass the comparison test with any of the values that are returned by the subquery.



[SAS Textbook Chapter 3, Problem 4]
* Question (ckong9-stat697): What are the advantages of using PROC SQL join features other than do it manually?



[SAS Textbook Chapter 3, Problem 5]
* Question (ckong9-stat697): How many types of outer joins in PROC SQL?
- Answer (ckong9-stat697): There are three types, left, right and full join.



[SAS Textbook Chapter 3, Problem 6]
* Question (ckong9-stat697): How to use the function COALESCE?
- Answer (ckong9-stat697): It can be included in the SELECT clause that  produce the same result as a DATA step matchmerge.



[SAS Online Training, Problem 7]
* Question (ckong9-stat697): What will be the difference of using Set Operator and a Join when handling multiple datasets?



[SAS Online Training, Problem 8]
* Question (ckong9-stat697): What is the difference between using UNION and INTERSECT/EXCEPT?
- Answer (ckong9-stat697): The UNION operator first combines results sets, then removes duplicate rows. INTERSECT/EXCEPT remove duplicate rows first, and then combine result sets.



[Combine Data at Different Grains Week 4 SAS Recipe]
* Question (ckong9-stat697): How will the performance different if we use set operator instead of using join function?


[Combine Data at Different Grains Week 4 Python Recipe]
* Question (ckong9-stat697): Why we have to define the encoding style when loading data?



***



# Recipes Exploration Results



```SAS
* Recipe: combine-data-at-different-grains.sas ;

* original recipe;

filename work_dir "sysfunc(getoption(work))/us_data.sas7bat";
proc http
        method="get"
        url="https://tinyurl.com/sashelp-us-data"
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
                    ,count(*) as number_of_zipcodes
                from 
                    sashelp.number_of_zipcodes
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



```Python
# Recipe: combine-data-at-different-grains.py

# original recipe

import pandas
import saspy
sas = saspy.SASsession(results='Text')

us_data_df = pandas.read_sas('https://tinyurl.com/sashelp-us-data', format='sas7bdat', encoding='latin-1)

zipcode_df = sas.sasdata2dataframe(table='zipcode', libref='sashelp')
zipcode_agg_by_statename = zipcode_df.groupby('STATENAME').size()
zipcode_agg_by_statename_df = zipcode_agg_by_statename.to_frame('number_of_zipcodes').reset_index()

us_data_w_zipcode_df = us_data_df.merge(zipcode_agg_by_statename_df, now='outer', on='STATENAME')
us_data_w_zipcode_subset_df = us_data_w_zipcode_df[['STATENAME', 'REGION', 'number_of_zipcodes']]
us_data_w_zipcode_sorted_df = us_data_w_zipcode_subset_df.sort_values(by='number_of_zipcodes', ascending=False)

print(us_data_w_zipcode_sorted_df)


```
