
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 2]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 3]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 4]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 5]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 6]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 7]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 8]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 9]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[Course Structure Quiz, Problem 10]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[      Week 4 SAS Recipe]
* Question (mwong70-stat697): 
- Answer (mwong70-stat697):



[      Week 4 SAS Recipe]
* Question (mwong70-stat697): Is there a way to display the "Window" option menu or log window?




***



# Recipes Exploration Results



```SAS
* Recipe: basic-dry-programming-pattern ;

* original recipe;
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
            if species = "&currentSpecies.";
        run;
        proc means n nmiss min q1 median q3 maxdec=1;
        run;
    %end;
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
        st sashelp.iris;
        if species = "%s";
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
