
# Questions about Problems and Recipes



* Question (mwong70-stat697): How would you describe what a FizzBuzz algorithm looks like, in any language :-) ?

&dash; Answer (mwong70-stat697): 
```R
if n % 15 then print('FizzBuzz');
elif n % 3 then print('Fizz');
elif n % 5 then print('Buzz');
else n
```


* Question (mwong70-stat697): What lessons did you take from Joel Grus's article, "Fizz Buzz in Tensorflow"? 

&dash; Answer (mwong70-stat697): Be able to identify the interview question, and write a succinct code that is clear and yield an effective output. Optionally, pick up some humor book.



* Question (mwong70-stat697): Which words and phrases were confusing from Jeff Atwood's article, "Why Can't Programmers.. Program?" 
    
&dash; Answer (mwong70-stat697):
    
1. recursive def. problem-solving method by calling a function by itself. 
2. "can't program their way out of a paper bag" -- an idiom for "one's way out of a paper bag" meaning: one is incompetent or unable to do something basic.
3. chasm def. dissension.
4. lest def. to avoid the risk of.
5. Vertigo refers to a software company that works on UX solutions, some clients include Microsoft, Silverlight.
6. flame-out def. a complete or conspicuous failure.



* Question (mwong70-stat697): How many achievements are there for this class?

&dash; Answer (mwong70-stat697): 5.



* Question (mwong70-stat697): Where can I find the estimated hours needed to complete tasks for this class?

&dash; Answer (mwong70-stat697): Refer to Activities and Assignment Maps on Blackboard.



* Question (mwong70-stat697): How can I find information about formatting for GitHub?

&dash; Answer (mwong70-stat697): Refer to https://guides.github.com/features/mastering-markdown/.



* Question (mwong70-stat697): Why do some entry level jobs require a certification?

&dash; Answer (mwong70-stat697): It's a mean for the industry to assess the candidate's technical qualification.



***



# Recipes Exploration Results



```SAS


data _null_;
    do i = 1 to 100;
        if mod(i, 15) = 0 then put 'FizzBuzz';
        else if mod(i, 3) = 0 then put 'Fizz';
        else if mod(i, 5) = 0 then put 'Buzz';
        else put i=;
    end;
run;



```



```Python


for i in range(1, 101):
if i % 15 == 0: print('FizzBuzz')
elif i % 3 == 0: print('Fizz')
elif i % 5 == 0: print('Buzz')
else: print('i=', i)a



```
