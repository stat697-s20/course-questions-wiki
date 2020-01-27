
# Questions about Problems and Recipes



[Course Materials Question 1]

	•	Question (sbanairajaraman-stat697):How to get A?
	•	Answer (sbanairajaraman-stat697): A course grade of A is the highest and it can be achieved by completing all the achievements?

[Course Materials Question 2]

	•	Question (sbanairajaraman-stat697): How will we receive grading and feedback on our work?
	•	Answer (sbanairajaraman-stat697): Feedback is given through Slack through DM from the instructor.

[Course Materials Question 3]

	•	Question (sbanairajaraman-stat697): How to clarify our questions?
	•	Answer (sbanairajaraman-stat697): In the #q-and-a-and-a channel in Slack or DM to instructor.

[Course Materials Question 4]

	•	Question (sbanairajaraman-stat697): Other than reporting typos or lack of clarity in course materials, are there any other ways to earn extra credit?
	•	Answer (sbanairajaraman-stat697): Extra credit can also be earned by contributing to Weekly Reflections after the week 7 deadline.

[Course Materials Question 5]

	•	Question (sbanairajaraman-stat697): What material and format should we expect on the Final Exam?
	•	Answer (sbanairajaraman-stat697): The final exam will be a multiple choice exam and will cover material covered in the course textbook, Weekly Reflections, the example "standard exam questions" on proc sql, and course GitHub repos.

[Course Materials Question 6]

	•	Question (sbanairajaraman-stat697): Can completing more than the minimum required to earn an achievement be applied to missed points needed to order another achievement?
	•	Answer (sbanairajaraman-stat697):

[Course Materials Question 7]

	•	Question (sbanairajaraman-stat697): Are Weekly Reflections also a tool for us to build and share our study guides for the final?
	•	Answer (sbanairajaraman-stat697):



***



# Recipes Exploration Results

[SAS_recipe-fizz-buzz] 

```SAS


data _null_;
    do i=1 to 100;
        if mod(i,5) == 0 put 'Fizz'
        else if mod(i,3) == 0 put 'Buzz'
        else put i=
run;



```
[SAS_recipe-fizz-buzz Question]

	•	Question (sbanairajaraman-stat697):what is data null?
	•	Answer (sbanairajaraman-stat697): Null is a keyword in SAS and it indicates "nothing". In this example we are not using any data sets and we are practising the usage of Loop, mod function and if elseif else conditional branching.
  

[Python_recipe-fizz-buzz]

```Python


for i in range(1,100):
    if i % 3 == 0: print ('Fizz')
    elif i % 5 == 0: print ('Buzz')
    else: print ('i=',i)
 



```
[Python_recipe-fizz-buzz Question]


	•	Question (sbanairajaraman-stat697): what does range function do in python?
	•	Answer (sbanairajaraman-stat697): In this case, it assigns a range of value from 1 to 100 to the loop variable i. For loop will run for the loop variable i from 1 to 100.  
  
