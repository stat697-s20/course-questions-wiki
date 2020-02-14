
# Questions about Problems and Recipes



[TB Chapter 2, Problem 1]
* Question (yxie18-stat697): Is there difference between the conditional operator IS NULL and IS MISSING?



[TB Chapter 2, Problem 2]
* Question (yxie18-stat697): As for LIKE operator, can space also be regarded as one character when using the special character % with the LIKE operator?
- Answer (yxie18-stat697): According to the example on Page 38, I think so.



[TB Chapter 2, Problem 3]
* Question (yxie18-stat697): As I have been wondering about the difference between the WHERE clause and HAVING clause, and I noticed that it's said in the TB that WHERE clause is processed before SELECT clause. Is it also a consideration when thinking about whether to put the condition statement in the WHERE clause or in the HAVING clause?



[TB Chapter 2, Problem 4]
* Question (yxie18-stat697): When using CALCULATED keyword in the FROM clause, will second pass through the whole query still happen?
- Answer (yxie18-stat697): Per my understanding on what's said on Page 60 and 61， I think data remerging won't happen under this situation.



[TB Chapter 2, Problem 5]
* Question (yxie18-stat697): As summary function, could count(*) and count(column) be used interchangably?



[TB Chapter 2, Problem 6]
* Question (yxie18-stat697): What's the difference between HAVING and WHERE clause?
- Answer (yxie18-stat697): HAVING goes with GROUP BY, WHERE goes with FROM; can use summary functions in HAVING but cannot use them with WHERE clause; need to specify the keyword CALCULATED in a WHERE clause while don't have to do it for HAVING clause.



[TB Chapter 3, Problem 7]
* Question (yxie18-stat697): What would happen, if in the Example: Technique 2 on the Page 113, the Sasuser.Staffmaster table was not assigned with different alias each time it was read?



[combine-data-at-different-grains SAS Recipe]
* Question (yxie18-stat697): Why do we have to specify the out and method in the PROC HTTP procedure?



[combine-data-at-different-grains Python Recipe]
* Question (yxie18-stat697): Why do we need to reset index for zipcode_agg_by_statename_df? Is it the same thing with appending a new row with index?



***



# Recipes Exploration Results



```SAS


* Recipe: combine-data-at-different-grains.sas ;

filename work_dir '%sysfunc(getoption(work))/us_data.sas7bdat';
proc http
        method = 'get'
        url = 'https://tinyurl.com/sashelp-us-data'
        out = work_dir
    ;
run;

proc sql number;
    select
        coalesce(A.statename, B.statename) as statename
        , A.region
        , B.number_of_zipcodes
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



```Python


# Recipe: combine-data-at-different-grains.py

import pandas
import saspy
sas = saspy.SASsession(results = 'TEXT')

us_data_df = pandas.read_sas('http://tinyurl.com/sashelp-us-data', format = 'sas7bdat', encoding = 'latin-1')

zipcode_df = sas.sasdata2dataframe(table = 'zipcode', libref = 'sashelp')
zipcode_agg_by_statename = zipcode_df.groupby('STATENAME').size()
zipcode_agg_by_statename_df = zipcode_agg_by_statename.to_frame('number_of_zipcodes').reset_index()

us_data_w_zipcode_df = us_data_df.merge(zipcode_agg_by_statename_df, how = 'outer', on = 'STATENAME')
us_data_w_zipcode_subset_df = us_data_w_zipcode_df[['STATENAME', 'REGION', 'number_of_zipcodes']]
us_data_w_zipcode_sorted_df = us_data_w_zipcode_subset_df.sort_values(by = 'number_of_zipcodes', ascending = FALSE)

print(us_data_w_zipcode_sorted_df)



```
