
# Questions about Problems and Recipes



# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (ckong9-stat697): Is it possible to have online office hours other than Saturdays?



[Course Structure Quiz, Problem 2]
* Question (ckong9-stat697): Is it good to start with reading the reference books to catch up the SAS programming technique?



[Course Structure Quiz, Problem 3]
* Question (ckong9-stat697): After revising the weekly forum/weekly reflection, is it count is 'met'?



[Course Structure Quiz, Problem 4]
* Question (ckong9-stat697): How to I share my codes on GitHub so that other classmates may able to notify and probably have some comments?



[Course Structure Quiz, Problem 5]
* Question (ckong9-stat697): Can I reply to some of the questions in the weekly reflection?


[Course Structure Quiz, Problem 6]
* Question (ckong9-stat697): What will be approximately the level of programming skills after completing all the courses achievements including a pass in final exam?



[Course Structure Quiz, Problem 7]
* Question (ckong9-stat697): How should I form a team for the team-based project?



[hello-world Week 1 SAS Recipe]
* Question (ckong9-stat697): What will be the difference of using JypyterLab SAS Kernal and SAS Studio?



[fizz-buzz Week 1 SAS Recipe]
* Question (ckong9-stat697): Compare to Python, which will be more time efficient if we are dealing with 1e9 entries instead of 100 entries with multiple looping like sampling?



***



# Recipes Exploration Results



```SAS

* Recipe: fizz-buzz.sas ;

* original recipe;
data _null_;
    do i = 1 to 100;
        if mod(i,3) = 0 then put 'Fizz';
        else if mod(i, 5) = 0 then put 'Buzz';
        else put i=;
    end;
run;

* modified to use macro variables to parametrize what's printed when;
* note the need to switch to double-quote for macro variables to render;
* modified to complete the full requirement of FizzBuzz;
%let mod1 = 3;
%let mod1msg = Fizz;
%let mod2 = 5;
%let mod2msg = Buzz;
%let mod3 = 15;
%let mod3msg = Fizzbuzz;
data _null_;
    do i = 1 to 100;
        if mod(i,&mod3) = 0 then put "&mod3msg.";
            else if mod(i,&mod1) = 0 then put "&mod1msg.";
            else if mod(i,&mod2) = 0 then put "&mod2msg.";
        else put i=;
    end;
run;



```



```Python


# Recipe: fizz-buzz.py

# original recipe
for i in range(1,101):
    if i % 3 == 0: print('Fizz')
    elif i % 5 == 0: print('Buzz')
    else: print('i=',i)

# modified to fully solve complete Fizz Buzz problem described at
# https://blog.codinghorror.com/why-cant-programmers-program/
# modified with using global variables for easier editing in the future
mod1 = 15
mod1msg = 'Fizzbuzz'
mod2 = 3
mod2msg = 'Fizz'
mod3 = 5
mod3msg = 'Buzz'
for i in range(1,101):
    if i % mod1 == 0: print(mod1msg)
    elif i % mod2 == 0: print(mod2msg)
    elif i % mod3 == 0: print(mod3msg)
    else: print('i=',i)



```
