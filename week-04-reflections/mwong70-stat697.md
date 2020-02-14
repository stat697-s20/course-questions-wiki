
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (mwong70-stat697): Which functions were used in this session?
- Answer (mwong70-stat697): coalesce, join, distinct



[Course Structure Quiz, Problem 2]
* Question (mwong70-stat697): What research question do we want ot answer in this lesson? 
- Answer (mwong70-stat697): We want to know how to join tables and deal with duplicates.



[Course Structure Quiz, Problem 3]
* Question (mwong70-stat697): What information can we gather by combining data at different grains? 
- Answer (mwong70-stat697): How many tables or aliases, and the number of columns that we joined.



[Course Structure Quiz, Problem 4]
* Question (mwong70-stat697): How does SAS deal with missing data in coalesce function?
- Answer (mwong70-stat697): Coalesce function will skip the missing data.



[Course Structure Quiz, Problem 5]
* Question (mwong70-stat697): How do we remove duplicates?
- Answer (mwong70-stat697): The distinct function is used to remove duplicated uniqueID.



[Course Structure Quiz, Problem 6]
* Question (mwong70-stat697): Can we inner join binary numbers and logical TRUE/FALSE in the same column?
- Answer (mwong70-stat697): 



[Course Structure Quiz, Problem 7]
* Question (mwong70-stat697): What's the difference between outer and inner join?
- Answer (mwong70-stat697): 



[grain Week 4 SAS Recipe]
* Question (mwong70-stat697): What is grain?
- Grain is level of aggregation before joining with finer data.



[grain Week 4 SAS Recipe]
* Question (mwong70-stat697): Why do we use the coalesce function?
- Coalesce function ensures to list all uniqueID after joining data, but it skips the missing data.




***



# Recipes Exploration Results



```SAS
*Recipe: grain.sas

filename work_dir "%sysfunc(getoption(work))/us_data.sas7bdat";
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
        ,A.division
        ,B.number_of_zipcodes
    from
        work.us_data as A
        full join
        (
            select
                statename
                ,count(*) as number_of_zipcodes format comma12.
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
# Recipe: grain.py

import pandas
import saspy
sas = saspy.SASsession(results='TEXT')

us_data_df = pandas.read_sas('https://tinyurl.com/sashelp-us-data', format='sas7bdat', encoding='latin-1')

zipcode_df = sas.sasdata2dataframe(table='zipcode', libredf='sashelp')
zipcode_agg_by_statename = zipcode_df.groupby('STATENAME').size()
zipcode_agg_by_statename_df = zipcode_agg_by_statename.to_frame('number_of_zipcodes').reset_index()

us_data_w_zipcode_df = us_data_df.merge(zipcode_agg_by_statename_df, how='outer', on='STATENAME')
us_data_w_zipcode_subset_df = us_data_w_zipcode_df[['STATENAME','REGION','number_of_zipcodes']]
us_data_w_zipcode_sorted_df = us_data_w_zipcode_subset_df.sort_values(by='number_of_zipcodes', ascending=False)

print(us_data_w_zipcode_sorted_df)




```
