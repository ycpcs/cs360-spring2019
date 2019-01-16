---
layout: default
title: "Assignment 2"
---

**Due: Monday, Feb 5th in class** Late assignments will be penalized 20% per day.

Book Questions from *Introduction to Algorithms - 3rd ed.*
==========================================================

2.3-5 (recursively)

3-2 (with *brief* justifications for *each* row)

4-1 (b,c,d,e), 4-3 (a)

Merge sort implementation.

*Hints:*

> 2.3-5 - Be sure to give a *recursive* algorithm and the corresponding recursive equation. Then solve the equation via Master theorem.
>
> 3-2 - Refer to the properties of logs and exponentials in section 3.2, particularly eq. 3.15, 3.18, and the following properties
>
> ![image](images/assign02/asyprop.png)
>
> i.e. polynomials are bounded by exponentials and logarithms are bounded by polynomials.
>
> 4-1 - Use the Master theorem by identifying the appropriate cases.
>
> 4-3 - Remember that logarithms are bounded by polynomials.

**Implementation**

A skeleton project is provided in [CS360\_Sorter\_Merge.zip](../assign/src/CS360_Sorter_Merge.zip). The zip file contains both a Visual Studio project and a Linux/OSX makefile to compile the code. **Sorter.cpp** contains both utility functions as well as empty sort function stubs - you should not need to modify **main()** or *any* of the utility functions.

> -   For each input size, the program generates a *random* array **D[]**
> -   **D[]** is copied into the array **A[]** *prior* to each sorting function call (such that each sort works on the *same* data sets)
> -   You may wish to uncomment the **print\_array()** call after writing each sort to test your code for **n**=16 and **NUM\_AVG**=1 to verify the sort is working correctly
> -   Since C++ does not have an **A.length** member variable, I have included a function called **length(A)** which will return the length of the array (which is stored in **A[0]**)
> -   All arrays have been expanded by 1 (with appropriate adjustments to any loops) to agree with the pseudocode from the book where array indices range from **A[1]** -\> **A[n]**

*Your Task*

Implement the sort algorithm *as given in the pseudocode below* for merge sort. Insert counter increment statements (note: a **count** global variable is provided), into each sorting function for each *executable* line of *pseudocode* (e.g. count all three lines required to implement a swap as a *single* operation). Use this counter to *empirically* measure the runtime of each sort. Only increment the counter for statements *within* the sorting functions, i.e. do not include any initialization overhead incurred in **main()** or the utility functions. Note that **count** is reset prior to each sort call but the results are stored in a 2D array **counter** which is used to display a table of all results once all the sorts and runs have completed.

Generate runs for 13 input sizes by changing the **\#define MAX\_RUNS** symbolic constant. This will generate data for increasing powers of 2 from 2<sup>4</sup> = 16 to 2<sup>16</sup> = 65536.

The **\#define NUM\_AVG** sets the number of data sets of each size to generate in order to compute an *average* runtime for each size. This value should be set to a reasonable number, e.g. 10, to give a good approximation of the *average* runtime of each sort. Note that the larger the value that is chosen, the longer the program will take to run.

You should generate tables for *two* different input *ranges*

> -   Set **\#define MAX\_RANGE 32768** (giving elements in the range [1 -\> 32768])
> -   Set **\#define MAX\_RANGE 1024** (giving elements in the range [1 -\> 1024])

Once the data for all input sizes and element ranges have been generated, make a *meaningful* plot (e.g. using Excel) of the data showing *important* characteristics. In particular:

> -   Plot number of inputs *n* vs. empirical average runtimes as **data points**
> -   Show the *best fit* asymptotic **curve** for **cn lg n** appropriate for the sort. Determine an *approximate* value of **c** to the nearest 0.5 for each sort that fits the actual data relatively well. (Hint: Simply manually choose values for each **c** and plot the corresponding asymptotic curve until it fits the data *reasonably* well, i.e. you do not need to mathematically find the "best-fit" values.)

**Hint:** To plot **cn lg n**, consider making another column in the spreadsheet that computes the values for each empirical input size *n* and then plot that data as connected points without showing the individual data points.

*Merge Sort*

    MERGE-SORT(A,p,r)
    1  if p < r
    2     q = (p+r)/2
    3     MERGE-SORT(A,p,q)
    4     MERGE-SORT(A,q+1,r)
    5     MERGE(A,p,q,r)

    MERGE(A,p,q,r)
    1  n1 = q - p + 1
    2  n2 = r - q
    3  let L[1..n1+1] and R[1..n2+1] be new arrays
    4  for i = 1 to n1
    5     L[i] = A[p+i-1]
    6  for j = 1 to n2
    7     R[j] = A[q+j]
    8  L[n1+1] = INF
    9  R[n2+1] = INF
    10 i = 1
    11 j = 1
    12 for k = p to r
    13    if L[i] <= R[j]
    14       A[k] = L[i]
    15       i = i + 1
    16    else
    17       A[k] = R[j]
    18       j = j + 1

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
