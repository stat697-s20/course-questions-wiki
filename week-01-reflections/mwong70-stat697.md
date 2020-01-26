
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

(1) recursive def. problem-solving method by calling a function by itself.
(2) "can't program their way out of a paper bag" -- an idiom for "one's way out of a paper bag" meaning: one is incompetent or unable to do something basic.
(3) chasm def. dissension.
(4) lest def. to avoid the risk of.
(5) Vertigo refers to a software company that works on UX solutions, some clients include Microsoft, Silverlight.
(6) flame-out def. a complete or conspicuous failure.


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


SAS Kernel
```
[1]:

34   ods listing close;ods html5 (id=saspy_internal) file=stdout options(bitmap_mode='inline') device=svg style=HTMLBlue; ods
34 ! graphics on / outputfmt=png;
NOTE: Writing HTML5(SASPY_INTERNAL) Body file: STDOUT
35   
36   data _null_;
37       do i = 1 to 100;
38           if mod(i, 3) = 0 then put 'Fizz';
39           else if mod(i, 5) = 0 then put 'Buzz';
40           else put i=;
41       end;
42   run;
i=1
i=2
Fizz
i=4
Buzz
Fizz
i=7
i=8
Fizz
Buzz
i=11
Fizz
i=13
i=14
Fizz
i=16
i=17
Fizz
i=19
Buzz
Fizz
i=22
i=23
Fizz
Buzz
i=26
Fizz
i=28
i=29
Fizz
i=31
i=32
Fizz
i=34
Buzz
Fizz
i=37
i=38
Fizz
Buzz
i=41
Fizz
i=43
i=44
Fizz
i=46
i=47
Fizz
i=49
Buzz
Fizz
i=52
i=53
Fizz
Buzz
i=56
Fizz
i=58
i=59
Fizz
i=61
i=62
Fizz
i=64
Buzz
Fizz
i=67
i=68
Fizz
Buzz
i=71
Fizz
i=73
i=74
Fizz
i=76
i=77
Fizz
i=79
Buzz
Fizz
i=82
i=83
Fizz
Buzz
i=86
Fizz
i=88
i=89
Fizz
i=91
i=92
Fizz
i=94
Buzz
Fizz
i=97
i=98
Fizz
Buzz
NOTE: DATA statement used (Total process time):
      real time           0.03 seconds
      cpu time            0.00 seconds
      
43   
44   ods html5 (id=saspy_internal) close;ods listing;
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


```
[2]:
for i in range(1, 101):
    if i % 15 == 0: print('FizzBuzz')
    elif i % 3 == 0: print('Fizz')
    elif i % 5 == 0: print('Buzz')
    else: print('i=', i)

i= 1
i= 2
Fizz
i= 4
Buzz
Fizz
i= 7
i= 8
Fizz
Buzz
i= 11
Fizz
i= 13
i= 14
FizzBuzz
i= 16
i= 17
Fizz
i= 19
Buzz
Fizz
i= 22
i= 23
Fizz
Buzz
i= 26
Fizz
i= 28
i= 29
FizzBuzz
i= 31
i= 32
Fizz
i= 34
Buzz
Fizz
i= 37
i= 38
Fizz
Buzz
i= 41
Fizz
i= 43
i= 44
FizzBuzz
i= 46
i= 47
Fizz
i= 49
Buzz
Fizz
i= 52
i= 53
Fizz
Buzz
i= 56
Fizz
i= 58
i= 59
FizzBuzz
i= 61
i= 62
Fizz
i= 64
Buzz
Fizz
i= 67
i= 68
Fizz
Buzz
i= 71
Fizz
i= 73
i= 74
FizzBuzz
i= 76
i= 77
Fizz
i= 79
Buzz
Fizz
i= 82
i= 83
Fizz
Buzz
i= 86
Fizz
i= 88
i= 89
FizzBuzz
i= 91
i= 92
Fizz
i= 94
Buzz
Fizz
i= 97
i= 98
Fizz
Buzz


```
