
# Questions about Problems and Recipes


[FizzBuzz, no particular source]

* Question (mwong70-stat697): How would you describe what a FizzBuzz algorithm looks like, in any language :-) ? (Rationale: This brainstorming step should help the code-writing process.) [Note: I have reasons to believe this is partly python because of the conditional `elif`, but it makes sense to me when I write it down on a piece of paper. It's the first step how I write a code. The first step would be assigning mod( , 15) because that will supercede the smaller mod values and therefore assign "FizzBuzz" instead of Fizz or Buzz for the multiples of 15.] 

- Answer (mwong70-stat697): 
`if n % 15 then print('FizzBuzz'); 
elif n % 3 then print('Fizz');
elif n % 5 then print('Buzz');
else n`


["Fizz Buzz in Tensorflow" by Joel Grus]

* Question (mwong70-stat697): What lessons do you take from Joel Grus's article, "Fizz Buzz in Tensorflow"? (Rationale: I don't think TensorFlow work in this case since 21==21 and 100=='Fizz' showed that the output failed.) [Note: I am unsure if this article was meant to be a satire or fiction. Statisticians have a good sense of humor.]

- Answer (mwong70-stat697): Be able to identify the interview question, and write a succinct code that is clear and yield an effective output. Optionally, pick up some humor book.


["Why Can't Programmers.. Program?" by Jeff Atwood]

* Question (mwong70-stat697): Which words and phrases were confusing from Jeff Atwood's article, "Why Can't Programmers.. Program?" (Rationale: Knowing technical vocabulary will help understanding the article more in-depth.) [Note: This is important for reading comprehension.]

- Answer (mwong70-stat697):
1. recursive def. problem-solving method by calling a function by itself.
2. "can't program their way out of a paper bag" -- an idiom for "one's way out of a paper bag" meaning: one is incompetent or unable to do something basic.
3. chasm def. dissension.
4. lest def. to avoid the risk of.
5. Vertigo refers to a software company that works on UX solutions, some clients include Microsoft, Silverlight.
6. flame-out def. a complete or conspicuous failure.


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


***


# Recipes Exploration Results


```Python
for i in range(1, 101):
    if i % 15 == 0: print('FizzBuzz')
    elif i % 3 == 0: print('Fizz')
    elif i % 5 == 0: print('Buzz')
    else: print('i=', i)
```
