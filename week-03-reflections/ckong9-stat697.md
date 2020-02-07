
# Questions about Problems and Recipes



[SAS Textbook Chapter 3&4, Problem 1]
* Question (ckong9-stat697): How often we combine the tables vertically or horizontally when using PROC SQL?



[SAS Textbook Chapter 3, Problem 2]
* Question (ckong9-stat697): Can tables without matching rows be combined horizontally?



[SAS Textbook Chapter 3, Problem 3]
* Question (ckong9-stat697): How can we join specific tables together in PROC SQL?
- Answer (ckong9-stat697): We can use FROM <table-1>, <table-2>, <table-3> ... to join tables together.



[SAS Textbook Chapter 4, Problem 4]
* Question (ckong9-stat697): What set operators can we use in joining table vertically using PROC SQL?
- Answer (ckong9-stat697): We can use EXCEPT, INTERSECT, UNION, OUTER UNION to join tables. OUTER UNION is to join tables that does not overlay columns.



[SAS Textbook Chapter 4, Problem 5]
* Question (ckong9-stat697): What is the use of using CORR?
- Answer (ckong9-stat697): It is to overlay the columns with a common name. The effect is combining columns with the same name to reduce the number of column.



[SAS Online Training Problem 6]
* Question (ckong9-stat697): What is the advantages of using subquery in PROC SQL?
- Answer (ckong9-stat697): We can include multiple queries within a same query. Meaning that it can make the program more dynamic.



[SAS Online Training, Problem 7]
* Question (ckong9-stat697): Why we use in-line view in PROC SQL?
- Answer (ckong9-stat697): We can avoid frequent access to tables, especially when the tables are large. Also, it prevents others from viewing the data they shouldn't be able to read.



[SAS Online Training, Problem 8]
* Question (ckong9-stat697): What is the use of creating marco variables?



[Basic Dry Programming Pattern Week 3 SAS Recipe]
* Question (ckong9-stat697): Can we include marco in a marco? Can we use if-else statement to determine which 

[Basic Dry Programming Pattern Week 3 SAS Recipe]
* Question (ckong9-stat697): Can we use if-else statement to determine which marco to use? (For example different situation use different marco.)

[Basic Dry Programming Pattern Week 3 Python Recipe]
* Question (ckong9-stat697): Will it take longer using SAS Marco in Python if we have to handle large data set?



***



# Recipes Exploration Results



```SAS
* Recipe: basic-dry-programming-pattern.sas ;

* original recipe;

options mprint;
%marco splitDatasetAndPrintMeans;
    %let species1 = Setosa;
    %let species2 = Versicolor
    %let species3 = Virginica;
    %put _user_;
    %put;

    %do i = 1 %to 3;
        %let currentSpecies = &&species&i.; /*Forward rescan rule*/
        %put &=currentSpecies.;
        data iris_&currentSpecies.;
            set sashelp.iris;
            if species = "&currentSpecies.";
        run;
        proc means n nmiss min q1 median q3 maxdec=1;
        run;
    &end;
%mend;
%splitDatasetAndPrintMeans

```



```Python
# Recipe: basic-dry-programming-pattern.py

# original recipe

import saspy
sas = saspy.SASsession(results='TEXT')

sas_code_fragment = '''
    data iris_%s;
        set sashelp.iris;
        if species = "%s"
    run;
    proc means n nmiss min q1 median q3 max maxdec=1;
    run;
'''

for column_name in ['Setosa', 'Versicolor', 'Virginica']:
    sas_submit_return_value = sas.submit(
        sas_code_fragment % (column_name, column_name)
    )
    print(sas_submit_return_value['LST'])

```
