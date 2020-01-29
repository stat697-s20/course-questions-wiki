
# Questions about Problems and Recipes

[Course Materials Question 1] 
* Question (bbasulto-stat697):Is it possible to get an A+ if you complete more than the minimum required to earn the achievements?
- Answer (bbasulto-stat697): A course grade of A is the highest that can be achievemented accourding to the University Catelog.
	
[Course Materials Question 2] 
* Question (bbasulto-stat697): How will we receive grading and feedback on our work?
- Answer (bbasulto-stat697): Feedback is given through Slack through both DM for personal progress and class feedback is given in the appropriate channel.
	
[Course Materials Question 3] 
* Question (bbasulto-stat697): Where do we subit our found typos or lack of clarity in course materials for extra credit?
- Answer (bbasulto-stat697): In the #q-and-a-and-a channel in Slack.
	
[Course Materials Question 4] 
* Question (bbasulto-stat697): Other than reporting typos or lack of clarity in course materials, are there any other ways to earn extra credit?
- Answer (bbasulto-stat697): Extra credit can also be earned by contributing to Weekly Reflections after the week 7 deadline.

[Course Materials Question 5] 
* Question (bbasulto-stat697): What material and format should we expect on the Final Exam?
- Answer (bbasulto-stat697): The final exam will be a multiple choice exam and will cover material covered in the course textbook, Weekly Reflections, the example "standard exam questions" on proc sql, and course GitHub repos.

[Course Materials Question 6] 
* Question (bbasulto-stat697): Can completing more than the minimum required to earn an achievement be applied to missed points needed to order another achievement?
- Answer (bbasulto-stat697):

[Course Materials Question 7] 
* Question (bbasulto-stat697): Are Weekly Reflections also a tool for us to build and share our study guides for the final?
- Answer (bbasulto-stat697):


***

# Recipes Exploration Results



```SAS

[SAS_recipe-fizz-buzz] 

data _null_;
    do i = 1 to 100;
        if mod(i,3) = 0 then put 'Fizz';
        else if mod(i,5) = 0 then put 'Buzz';
        else put i=;
    end;
run;


[SAS_recipe-fizz-buzz Question]
* Question (bbasulto-stat697): What types of situations is the data _null_ step used in SAS? 
- Answer (bbasulto-stat697): The data _null_ step is most usefull when you want to perform computations, create macro variables, manipulate txt files, and for debugging.

```

```Python

[Python_recipe-fizz-buzz]

for i in range(1,101):
    if i % 3 == 0: print('Fizz')
    elif 1 % 5 == 0: print('Buzz')
    else: print('i=',i)

[Python_recipe-fizz-buzz Question]
* Question (bbasulto-stat697): Why do we set the range in the Python recipe to be (1,101) instead of (1, 100) like the SAS recipe?
- Answer (bbasulto-stat697): Because the range in Python is exclusive, unlike SAS which is inclusive. 



```
