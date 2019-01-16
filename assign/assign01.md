---
layout: default
title: "Assignment 1"
---

**Due: Monday, Feb 4th in class** Late assignments will be penalized 20% per day.

Book Questions from *Introduction to Algorithms - 3rd ed.*
==========================================================

1.2-2, 1.2-3

2.2-3, 2-2

Insertion sort implementation.

*Hints:*

> 1.2-2 & 1.2-3 Remember that *n* must be an **integer**.
>
> 2.2-3 Be sure to give a *mathematically rigorous* justification for your answer and not simply an *intuitive* explanation. Consider what the probability is for the *i*<sup>th</sup> element being the desired one and how many elements were searched to find it.
>
> 2-2 (a) - Consider what **two** criteria are necessary for a sorting algorithm to be correct (the obvious one is that the elements end up in non-decreasing order, what is the other?)
>
> > (b) - What must be true both **before** and **after** the *inner* loop executes (consider what the inner loop does)? Remember you must show it holds for *initialization*, *maintenance*, and *termination* conditions.
> >
> > (c) - What must be true both **before** and **after** the *outer* loop executes (consider what the outer loop does)? Remember you must show it holds for *initialization*, *maintenance*, and *termination* conditions.
> >
> > (d) - Note this version of bubble-sort uses *fixed* iteration loops, i.e. no **while** statements.

**Implementation**

A skeleton project is provided in [CS360\_Sorter\_Insert.zip](../assign/src/CS360_Sorter_Insert.zip). The zip file contains both a Visual Studio project and a Linux/OSX makefile to compile the code. **Sorter.cpp** contains both utility functions as well as empty sort function stubs - you should not need to modify **main()** or *any* of the utility functions.

> -   For each input size, the program generates a *random* array **D[]**
> -   **D[]** is copied into the array **A[]** *prior* to each sorting function call (such that each sort works on the *same* data sets)
> -   You may wish to uncomment the **print\_array()** call after writing each sort to test your code for **n**=16 and **NUM\_AVG**=1 to verify the sort is working correctly
> -   Since C++ does not have an **A.length** member variable, I have included a function called **length(A)** which will return the length of the array (which is stored in **A[0]**)
> -   All arrays have been expanded by 1 (with appropriate adjustments to any loops) to agree with the pseudocode from the book where array indices range from **A[1]** -\> **A[n]**

*Your Task*

Implement the sort algorithm *as given in the pseudocode below* for insertion sort. Insert counter increment statements (note: a **count** global variable is provided), into each sorting function for each *executable* line of *pseudocode* (e.g. count all three lines required to implement a swap as a *single* operation). Use this counter to *empirically* measure the runtime of each sort. Only increment the counter for statements *within* the sorting functions, i.e. do not include any initialization overhead incurred in **main()** or the utility functions. Note that **count** is reset prior to each sort call but the results are stored in a 2D array **counter** which is used to display a table of all results once all the sorts and runs have completed.

Generate runs for 13 input sizes by changing the **\#define MAX\_RUNS** symbolic constant. This will generate data for increasing powers of 2 from 2<sup>4</sup> = 16 to 2<sup>16</sup> = 65536.

The **\#define NUM\_AVG** sets the number of data sets of each size to generate in order to compute an *average* runtime for each size. This value should be set to a reasonable number, e.g. 10, to give a good approximation of the *average* runtime of each sort. Note that the larger the value that is chosen, the longer the program will take to run.

You should generate tables for *two* different input *ranges*

> -   Set **\#define MAX\_RANGE 32768** (giving elements in the range [1 -\> 32768])
> -   Set **\#define MAX\_RANGE 1024** (giving elements in the range [1 -\> 1024])

Once the data for all input sizes and element ranges have been generated, make a *meaningful* plot (e.g. using Excel) of the data showing *important* characteristics. In particular:

> -   Plot number of inputs *n* vs. empirical average runtimes as **data points**
> -   Show the *best fit* asymptotic **curve** for **cn**<sup>2</sup> appropriate for the sort. Determine an *approximate* value of **c** to the nearest 0.5 for each sort that fits the actual data relatively well. (Hint: Simply manually choose values for each **c** and plot the corresponding asymptotic curve until it fits the data *reasonably* well, i.e. you do not need to mathematically find the "best-fit" values.)

**Hint:** To plot **cn**<sup>2</sup>, consider making another column in the spreadsheet that computes the values for each empirical input size *n* and then plot that data as connected points without showing the individual data points.

*Insertion Sort*

    INSERTION-SORT(A)
    1  for j = 2 to A.length
    2     key = A[j]
    3     // Insert A[j] into the sorted sequence A[1..j-1]
    4     i = j - 1
    5     while i > 0 and A[i] > key
    6        A[i+1] = A[i]
    7        i = i - 1
    8     A[i+1] = key

**HINTS:**

Function call statements **DO NOT** increment the counter since their runtime is evaluated by the execution of the function.

Return statement **DO NOT** increment the counter.

Loop statements, i.e. **for** and **while**, will execute *one more* time than the statements in the loop body. Hence a counter can be added to a loop as follows

    for (...) {
       count++;
       // Body of loop
    }
    count++;
    
    while (...) {
       count++;
       // Body of loop
    }
    count++;
    
For simple logic constructs, e.g. **if**, **if/else**, a count update can be added after the structure since only one branch will execute depending on the result of the condition

    if (...) {
       // Body of if
    }
    count++;
    
    if (...) {
       // Body of if branch
    } else {
       // Body of else branch
    }
    count++;
    
For chained logical structures, i.e. **if/else if/ else**, there will need to be counters in *each* branch for the *total* number of conditions evaluated since they execute sequentially

    if (...) {
       count++;
       // Body of first if branch
    } else if (...) {
       count += 2;
       // Body of second if branch
    } else if (...) {
       count += 3;
       // Body of third if branch
    } else {
       count += however many if conditions there are
       // Body of else branch
    }
