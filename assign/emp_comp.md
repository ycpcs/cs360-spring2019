---
layout: default
title: "Empirical Comparison Report"
---

**Due: Friday, March 9th in class** Late assignments will be penalized 20\% per day.

Empirical Sorting Comparison
----------------------------

The purpose of this assignment is to compare the various sorting algorithms implemented in assignments 1, 2, 3, and 4.

Submission
----------

The submission for this assignment should consist of a written report that graphically shows the results for all five sorts and provides a discussion of what was observed. **DO NOT** include your completed source code, but provide tables of numerical data in an appendix at the end of the report.

The report should include *meaningful* plots (e.g. using Excel) of all the data showing *important* comparison characteristics. In particular:

> -   Plot number of inputs *n* vs. empirical average runtimes as data *points*
	
> -   Show *curves* of the *best fit* asymptotic values **cn + k**, **cn lg n**, or **cn**<sup>2</sup> as appropriate for each sort. Determine an *approximate* value of **c** for each sort to the nearest 0.5 that fits the actual data relatively well. (Hint: Simply manually choose values for each **c** and plot the corresponding asymptotic curve until it fits the data *reasonably* well, i.e. you do not need to mathematically find the "best-fit" values.) Include a legend with each graph listing the "best-fit" asymptotic curve formula's.
	
> -   A table listing the sort method, asymptotic behavior, and empirical asymptotic formula with "best-fit" constants.
	
**DISCUSS** the results in terms of observed behavior (e.g. how well does the asymptotic behavior match the empirical data), comparison of behaviors between sorts (e.g. which ones perform better at which data set sizes), comparison of hidden constants for sorts with the same asymptotic behaviors, and any other important observed features. The discussion should refer to the graphs when appropriate to illustrate each aspect.

