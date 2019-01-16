---
layout: default
title: "Assignment 3"
---

**Due: Monday, Feb 19th in class** Late assignments will be penalized 20\% per day.

Book Questions from *Introduction to Algorithms - 3rd ed.*
==========================================================

6.1-1, 6.1-4, 6.4-3

Heap sort and quick sort implementations

*Hints:*

> 6.1-1 - Recall that a heap is a *nearly complete* binary tree. Furthermore, the *height* of a heap is the maximal number of *edges* from the root to a leaf node.
>
> 6.1-4 - Consider what the heap property enforces with respect to the smallest node, i.e. where in the tree must it be.
>
> 6.4-3 - Explain the difference in run-times for best and worst case heapsort both practically and asymptotically.

**Implementations**

A skeleton project is provided in [CS360\_Sorter\_Heap\_Quick.zip](../assign/src/CS360_Sorter_HeapQuick.zip). The zip file contains both a Visual Studio project and a Linux/OSX makefile to compile the code. **Sorter.cpp** contains both utility functions as well as empty sort function stubs - you should not need to modify **main()** or *any* of the utility functions.

> -   For each input size, the program generates a *random* array **D[]**
> -   **D[]** is copied into the array **A[]** *prior* to each sorting function call (such that each sort works on the *same* data sets)
> -   You may wish to uncomment the **print_array()** call after writing each sort to test your code for **n**=16 and **NUM_AVG**=1 to verify the sort is working correctly
> -   Since C++ does not have an **A.length** member variable, I have included a function called **length(A)** which will return the length of the array (which is stored in **A[0]**)
> -   All arrays have been expanded by 1 (with appropriate adjustments to any loops) to agree with the pseudocode from the book where array indices range from **A[1]** -\> **A[n]**
> -   C++ also does not have an **A.heap-size** member variable, the parameter **heap-size** is passed as an additional parameter to any function requiring **A.heap-size**
	
*Your Task*
	
Implement the algorithms *as given in the pseudocode below* for heapsort and quicksort. Insert counter increment statements (note: a **count** global variable is provided), into each sorting function for each *executable* line of *pseudocode* (e.g. count all three lines required to implement a swap as a *single* operation). Use this counter to *empirically* measure the runtime of each sort. Only increment the counter for statements *within* the sorting functions, i.e. do not include any initialization overhead incurred in **main()** or the utility functions. Note that **count** is reset prior to each sort call but the results are stored in a 2D array **counter** which is used to display a table of all results once all the sorts and runs have completed.

Generate runs for 13 input sizes by changing the **\#define MAX\_RUNS** symbolic constant. This will generate data for increasing powers of 2 from 2<sup>4</sup> = 16 to 2<sup>16</sup> = 65536.

The **\#define NUM\_AVG** sets the number of data sets of each size to generate in order to compute an *average* runtime for each size. This value should be set to a reasonable number, e.g. 10, to give a good approximation of the *average* runtime of each sort. Note that the larger the value that is chosen, the longer the program will take to run.

You should generate tables for *two* different input *ranges*

> -   Set **#define MAX_RANGE 32768** (giving elements in the range [1 -> 32768])
> -   Set **#define MAX_RANGE 1024** (giving elements in the range [1 -> 1024])

Once the data for all input sizes and element ranges have been generated, make *meaningful* plots (e.g. using Excel) of the data showing *important* characteristics. In particular:

> -   Plot number of inputs *n* vs. empirical average runtimes as data *points*
> -   Show the *best fit* asymptotic **curve** for **cn lg n** appropriate for the sort. Determine an *approximate* value of **c** to the nearest 0.5 for each sort that fits the actual data relatively well. (Hint: Simply manually choose values for each **c** and plot the corresponding asymptotic curve until it fits the data *reasonably* well, i.e. you do not need to mathematically find the "best-fit" values.)

**Hint:** To plot **cn lg n**, consider making another column in the spreadsheet that computes the values for each empirical input size *n* and then plot that data as connected points without showing the individual data points.

*Heap Sort*

    HEAPSORT(A)
    1  BUILD-MAX-HEAP(A)
    2  for i = A.length downto 2
    3     exchange A[1] with A[i]
    4     A.heapsize = A.heapsize - 1
    5     MAX-HEAPIFY(A,1)

    BUILD-MAX-HEAP(A)
    1  A.heapsize = A.length
    2  for i = A.length/2 downto 1
    3     MAX-HEAPIFY(A,i)

    MAX-HEAPIFY(A,i)
    1  l = LEFT(i)
    2  r = RIGHT(i)
    3  if l <= A.heapsize and A[l] > A[i]
    4     largest = l
    5  else
    6     largest = i
    7  if r <= A.heapsize and A[r] > A[largest]
    8     largest = r
    9  if largest != i
    10    exchange A[i] with A[largest]
    11    MAX-HEAPIFY(A,largest)
	
*Quick Sort*

    QUICKSORT(A,p,r)
    1  if p < r
    2     q = PARTITION(A,p,r)
    3     QUICKSORT(A,p,q-1)
    4     QUICKSORT(A,q+1,r)
    
    PARTITION(A,p,r)
    1  x = A[r]
    2  i = p - 1
    3  for j = p to r-1
    4     if A[j] <= x
    5        i = i + 1
    6        exchange A[i] with A[j]
    7  exchange A[i+1] with A[r]
    8  return i+1

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
