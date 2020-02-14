
# Questions about Problems and Recipes



[TB Chapter 3, Problem 1]
* Question (yxie18-stat697): what's the difference between the terms cartesian product, full join, outer join and outer union?



[TB Chapter 3, Problem 2]
* Question (yxie18-stat697): As for WHERE clause, is there any difference between using 'AND' operation to link together two or more expressions, and just using comma?



[TB Chapter 3, Problem 3]
* Question (yxie18-stat697): As for the comparison between Date Step Match-Merge statement and PROC SQL Inner Join statement on Page 101, if the rows need to be sorted out by columns other than x, how to rewrite the Data Step statement?



[TB Chapter 3, Problem 4]
* Question (yxie18-stat697): What's the difference between subquery and in-line view?
- Answer (yxie18-stat697): One is used in WHERE clause and one is used in FROM clause.



[TB Chapter 4, Problem 5]
* Question (yxie18-stat697): When using ALL and CORR operator together with a EXCEPT operator for two tables with some matching values, is it the case that one matching value from the latter table can be used for only eliminating one value from the former table?
- Answer (yxie18-stat697): I think so.



[TB Chapter 4, Problem 6]
* Question (yxie18-stat697): The usage of ALL and CORR operator simultaneouly is quite tricky. Under what kind of reality circumstances would we need to use them together?



[TB Chapter 4, Problem 7]
* Question (yxie18-stat697): Can I understand that, when ALL and CORR are combined with each other, the point of ALL operator is "duplicates are allowed" and the point of CORR operator is "only the columns with same names are displayed"?



[basic-dry-programming-pattern SAS Recipe]
* Question (yxie18-stat697): What's implicit array? What's the difference between implicit array and explicit array? Any guidance on which one to choose under various circumstances.
- Answer (yxie18-stat697): Actually SAS recommends to stick with the explicitly subscripted arrays. This article could help: https://sasnrd.com/sas-array-implicit-explicit/



[basic-dry-programming-pattern SAS Recipe]
* Question (yxie18-stat697): Any examples and illustration on the forward re-scan rule?
- Answer (yxie18-stat697): This piece of article could help: https://www.koerup.dk/Cert/0202/020203/020203.html



[basic-dry-programming-pattern-with-saspy Python Recipe]
* Question (yxie18-stat697): In the Line 14 of the recipe, why it's sas_code_fragment % (column_name, column_name) rather than sas_code_fragment % (column_name). In a word, why two arguments are needed here?


***



# Recipes Exploration Results



```SAS


* Recipe: basic-dry-programming-pattern.sas ;

options mprint;
%macro splitDatasetAndPrintMeans;
    %let species1 = Setosa;
    %let species2 = Versicolor;
    %let species3 = Virginica;
    %put _user_;
    %put;
    
    %do i = 1 %to 3;
        %let currentSpecies = &&species&i.;
        %put &=currentSpecies.;
        data iris_&currentSpecies.;
            set sashelp.iris;
            if species = '&currentSpecies.';
        run;
        proc means n nmiss min q1 median q3 max maxdec = 1;
        run;
    %end;
%mend;
%splitDatasetAndPrintMeans



```



```Python


# Recipe: basic-dry-programming-pattern-with-saspy.py

import saspy
sas = saspy.SASsession(results = 'TEXT')

sas_code_fragment = '''
    data iris_%s;
        set sashelp.iris;
        if species = '%s';
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
