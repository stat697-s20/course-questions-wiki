
# Questions about Problems and Recipes



[Course Structure Quiz, Problem 1]
* Question (mwong70-stat697): What skills can a statistician acquire by studying a Structured Query Language?

&dash; Answer (mwong70-stat697): To access, explore, prepare, analyze, and report data, and export results.



[Course Structure Quiz, Problem 2]
* Question (mwong70-stat697): Name the 3 types of SAS tools, and list 1 difference about them.

&dash; Answer (mwong70-stat697): SAS Windowing Environment, SAS Studio, and SAS Enterprise Guide. SAS Studio and SAS Enterprise Guide include features such as code completion, formatting, and syntax coloring that make programming much easier!



[Course Structure Quiz, Problem 3]
* Question (mwong70-stat697): How many hours did you spend on this week's reading assignments, so far? What is one takeaway?

&dash; Answer (mwong70-stat697): Between 1-4 hours per day. The publication year of the book {2011, 2014, 2017} did not matter.  



[Course Structure Quiz, Problem 4]
* Question (mwong70-stat697): In JupyterLab, locate the indicator that shows how many character-length your window is.

&dash; Answer (mwong70-stat697):  



[Course Structure Quiz, Problem 5]
* Question (mwong70-stat697): Jargons specific to SAS.

&dash; Answer (mwong70-stat697): variables = column, clause = command



[Course Structure Quiz, Problem 6]
* Question (mwong70-stat697): What follows after a `WHERE` block? Is it numeric or character? 

&dash; Answer (mwong70-stat697): 

1. a boolean statement; numeric 
2. <column> equality or inequality `=`, `<`, `>`, `>=`, and `<=` ; numeric
3. <column> `LIKE` <character> ; character



[Course Structure Quiz, Problem 7]
* Question (mwong70-stat697): What is the difference between African and European pigeons? 

&dash; Answer (mwong70-stat697): 



[summarizing-data Week 2 SAS Recipe]
* Question (mwong70-stat697): How do you box-highlight in SAS?

&dash; Answer (mwong70-stat697): oh no.. I forgot, but I wrote it down somewhere in my notes.



[summarizing-data Week 2 PY Recipe]
* Question (mwong70-stat697): Name one difference between python and SAS.

&dash; Answer (mwong70-stat697): Python commands use periods `.` to join functions. SAS uses space.


***



# Recipes Exploration Results




**SAS Kernel**
```SAS


*******************************************************************************;
* SAS Recipe: summarize-data-using-sql ;
*******************************************************************************;
/*
Scenario: We wish to summarize properties of columns in a table.

Approach: Use appropriate optional clauses in a SQL select query.

Recipe:
proc sql <options: optional>;
    <select clause: mandatory>
    <from clause: mandatory>
    <where clause: optional>
    <group-by clause: optional>
    <having clause: optional>
    <order-by clause: optional>
    ;
quit;

*/

*Example;

* imitating proc print;
proc sql outobs=3;
    select *
    from sashelp.iris
    ;
quit;

* imitating proc sort and proc print;
proc sql outobs=5 number;
    select *
    from sashelp.iris
    order by SepalLength
    ;
quit;

* count the number of rows that contain irises of the same Species and group the frequency.
proc sql;
    select Species, count(*) as Number_of_Irises
    from sashelp.iris
    group by Species
    ;
quit;

    select
         Species
        ,min(SepalLength) as Minimum_Sepal_Length
        ,median(SepalLength) as Median_Sepal_Length
        ,max(SepalLength) as Maximum_Sepal_Length
    from
        sashelp.iris
    group by
        Species
    ;
quit;

/*
Notes:
(1) These examples demonstrate the utility of proc sql, which can be thought of as a swiss-army knife, capable of replicating much of the functionality of SAS procs for summarizing data. Four fundamental examples are as follows:

(1a) A select query comprising a select and from clause emulates proc print.

(1b) A select query comprising a select, from, and order-by clause emulates proc sort.

(1c) A select query comprising a select clause with count functions, from clause, and group-by clause can be used to emulate proc freq.

(1d) A select query comprising a select clause with summary functions, from clause, and group-by clause can be used to emulate proc means.Note that a single proc sql step can have multiple queries, with each query executed as soon as its terminating semicolon is encountered. Also, note that proc sql always ends with a quit statement, since it's an interactive procedure.


(2) In addition, by including additional clauses, or options within each clause, even more flexibility in summarizing data becomes possible. A helpful mental model is to think of a SQL select query as a process for transforming an input dataset (or multiple input datasets) into an output dataset. A SQL select query is composed of 2-6 clauses, with each clause playing a different role in creating output. These clauses must be used in the following order:

(2a) The (mandatory) "select" subsets the columns from the input dataset, and can also include calculations creating new columns.

(2b) The (mandatory) "from" clause determines the input dataset.

(2c) The (optional) "where" clause subsets the rows from the input dataset. Without a "where clause", all rows from the input dataset will be used.

(2d) The (optional) "group-by" clause combines (aka aggregates) rows from the input dataset, producing new rows to include in the output dataset. Without a "group-by" clause, the rows from the input dataset (possibly subsetted by a "where" clause) will be used as-is when creating an output dataset.

(2e) The (optional) "having" clause subsets the rows available for inclusion in the output dataset, resulting in a final set of rows for the output datasets. Without a "having" clause, all rows available for inclusion in the output dataset will be used.

(2f) The (optional) "order-by" clause sorts the final set of rows for the output datasets. Without an "order-by" clause, the order of the rows in the output dataset will be unpredictable. A helpful mnemonic for remembering this required order is "so few workers go home on-time" (suggestive of "select from with group-by having order-by").


(3) In summary, proc sql provides great flexibility, because it implements a variant of the ANSI SQL (Structured Query Language) standard, which includes both data-definition-language queries (e.g., create-table, describe-table, drop-table, and alter-table) and data-manipulation-language queries (e.g., the select-query describe above, as well as insert-into, update, delete-from). In addition, the from clause in applicable queries can be used to combine datasets both vertically (with set-theoretic operations like union and intersection) and horizontally (aka "joins") with greater flexibility than data-step programming.   


(4) However, there's an important trade-off: Data-step programming and many other SAS procs operate on datasets row-by-row, meaning they load rows from disk as needed, allowing them to operate on arbitrarily large datasets. Proc sql, on the other hand, loads all rows from a dataset into memory at once, meaning it can only operate on datasets that can fit into memory. As a result, proc sql is often faster than data-step programming and specialized procs for small-ish datasets, but it tends to be slower (or impossible to use) for large-ish datasets. In addition, data-step programming has features that proc sql does not have, like by-group progressing and the do-loop. Similarly, specialized procs like proc freq have features, like generating two-way tables, that would be difficult to recreate in proc sql. Consequently, proc sql is powerful and useful, especially for combining datasets vertically and horizontally, but it is not a complete replacement for other SAS features.
*/



```



**Python Kernel**

```Python



###############################################################################;
# Python Recipe: summarize-data-using-pandas ;
###############################################################################;

# Scenario: We wish to summarize properties of columns in a table.

# Approach: Use appropriate pandas module methods and operations.

# Example:


import pandas

iris = pandas.read_csv('https://tinyurl.com/stat697-iris')

# print the first 3 rows from the iris dataset
iris.head(3)

# print the first 5 rows of iris dataset after sorting by sepal_length
iris_sorted_by_sepal_length = iris.sort_values(by=['sepal_length'])
iris_sorted_by_sepal_length.head(5)

# summarize values for qualitative and quantitaive variables

# print frequency of each species in iris dataset
print(iris['species'].value_counts())

# print median of sepal_length by species in iris dataset
print(iris.groupby('species')['sepal_length'].agg(['min', 'median', 'max']))


# Notes:
# 
# (1) The Python package pandas is commonly used to create so-called DataFrame objects, which are essentially the same as their R counterpart. You should think of them as rectangular arrays of values, where all values in a given column have the same type of value (e.g., string or numeric). In addition, columns have names associated with them, and rows have index values (non-negative integers by default).
#
#
# (2) In the above example, we first load the pandas module, which makes it available to the Python session. Because we're working in SAS University Edition, which includes a custom Python distribution created by the SAS Institute, the pandas module has already been installed, so it only needs to be loaded. (This means, if we were working in a different Python environment, we might first need to install the pandas module ourselves. Installing packages is typically done with the command-line tool pip, which you can read more about at https://pip.pypa.io/en/stable/installing/ )
#
#
# (3) After the pandas module has been loaded, we use its read_csv method to load the famous iris dataset over the wire, which returns a DataFrame object that we call iris. The URL for the dataset is https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv, which is a copy of the dataset hosted by a popular Python data-viz module called seaborn. 
#
#
# (4) This DataFrame object is then manipulated with other methods made available by the pandas module, which are all described in details at https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html
#
#
# (5) Note also the use of bracket notation for indexing specific DataFrame columns, e.g., iris['species'], which extracts the column names 'species'. A good overview of indexing in Python can be found at https://datacarpentry.org/python-ecology-lesson/03-index-slice-subset/
#
#
# (6) Finally, if you're new to Python, the following gives a great overview of built-in data structures, with the entire (incredibly short) book recommended as a comprehensive overview of Python notation and language conventions: https://jakevdp.github.io/WhirlwindTourOfPython/06-built-in-data-structures.html



```
