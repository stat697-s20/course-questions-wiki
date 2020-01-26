
# Questions about Problems and Recipes



[fizz-buzz Week 1 SAS Recipe]
* Question (yxie18-stat697): what if I don't want to see the 'i =' part in the result, i.e. I just want to see the numbers and the words 'Fizz' and 'Buzz'?
- Answer (yxie18-stat697): Just change the 5th line of code from 'else put i=;' to 'else put i;'



[fizz-buzz Week 1 SAS Recipe]
* Question (yxie18-stat697): How to prevent myself from getting confused between Python, R and SAS language grammar? As they are kind of similar to each other. 



[fizz-buzz Week 1 SAS Recipe]
* Question (yxie18-stat697): When I am on the 2nd level indentation, how to go back to the 1st level indentation in SAS JupyterLab? I am used to using tab button to indent to the right and backspace to indent to the left, but it doesn't work in SAS.
- Answer (yxie18-stat697): Just change the indentation setting on 'settings' -> 'Text Editor Indentation' from space to tab.



[fizz-buzz Week 1 SAS Recipe]
* Question (yxie18-stat697): What does it mean to type data _null_ in the 1st line?
- Answer (yxie18-stat697): When the _NULL_ keyword is usedm no data set is created on disk, thus it could be used for executing step codes.



[Course Structure Quiz, Problem 3]
* Question (yxie18-stat697): Will it be better if students can discuss over their reflection questions over the post forum?



[Course Structure Quiz, Problem 5]
* Question (yxie18-stat697): Why there is a final exam rather than the overal evluation of the course project? (I suppose there would be a course project).



[Course Structure Quiz, Problem 6]
* Question (yxie18-stat697): Talking about team-based problem solving, is there any measurement to prevent free-riders?



***



# Recipes Exploration Results



```SAS


data _null_;
	do i = 1 to 100;
		if mod(i,3) = 0 then put 'Fizz';
		else if mod(i, 5) = 0 then put 'Buzz';
        else put i;
	end;
run;



```



```Python


for i in range(1,101):
	if i%3 == 0: print('Fizz')
	elif i%5 ==0 : print('Buzz')
	else: print('i=', i)



```
