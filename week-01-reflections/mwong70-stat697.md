
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (mwong70-stat697): What are the 5 types of achievements can be acquired in this class? 
- Answer (mwong70-stat697): Initial Setup Achievement; Reading for Breadth Achievement; Reading for Depth Achievemnet; Team-based Problem Solving Achievement; and, Building General Knowledge Achievement.



[Course Structure Quiz, Problem 2]
* Question (mwong70-stat697): What does growth mindset means, in the purposes of this class?  
- Answer (mwong70-stat697): Embracing challenge, persistence, development through trial and error, learning from constructive feedback and critcism, and inspiration from others' success.



[Course Structure Quiz, Problem 3]
* Question (mwong70-stat697): Name the textbook. 
- Answer (mwong70-stat697): SAS Certification Prep Guide: Advanced Programming for SAS 9, 4th Edition (2014).



[Course Structure Quiz, Problem 4]
* Question (mwong70-stat697): What steps can a professional programmer take to continue sharpen their technical skills? 
- Answer (mwong70-stat697): Keeping up with current discipline-specific trends, and applying familiar concepts in real-world contexts.



[Course Structure Quiz, Problem 5]
* Question (mwong70-stat697): What values can be gained through working on the Team-based Problem Solving Achievement? 
- Answer (mwong70-stat697): Collaboration, innovation, and problem solving skills.



[SAS Recipe FizzBuzz, Problem 6]
* Question (mwong70-stat697): What are components used in this code?
- Answer (mwong70-stat697): loops, variables, conditional branching, and modulo.



[Python Recipe FizzBuzz, Problem 7]
* Question (mwong70-stat697): Why does the code start from 1 but stops at 101?



[Fizz-buzz-in-tensorflow, Problem 8]
* Question (mwong70-stat697): Do technical interviews ask for specific advanced codes like in tensorflow, can it be in any form that solve the problem, or does it require to cater to the position. 



[Week 1 Walkthrough, Problem 9]
* Question (mwong70-stat697): What is 'elif'?
- Answer (mwong70-stat697): An abbreviation of "else if".



***



# Recipes Exploration Results



```SAS
*******************************************************************************;
* SAS Recipe: fizz-buzz ;
*******************************************************************************;

/*
Scenario: Solve a simplified version of the FizzBuzz Challenge

Approach: Use a null data step and business logic to write to the log
*/

/*Example; */

data _null_;
    do i = 1 to 100;
        if mod(i,15) = 0 then put 'FizzBuzz';
        else if mod(i, 3) = 0 then put 'Fizz';
        else if mod(i, 5) = 0 then put 'Buzz';
        else put i=;
    end;
run;

```



```Python
###############################################################################
# Python Recipe: fizz-buzz
###############################################################################

# Scenario: Solve a simplified version of the FizzBuzz Challenge

# Approach: Use print statements and business logic to write to the console

# Example:

for i in range(1,101):
    if i % 3 == 0: print('Fizz')
    elif i % 5 == 0: print('Buzz')
    else: print('i=',i)

```
