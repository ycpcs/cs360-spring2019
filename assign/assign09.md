---
layout: default
title: "Assignment 9"
---

**Due: Wednesday, Apr 25th in class** Late assignments will be penalized 20% per day.

Book Questions from *Introduction to Algorithms - 3rd ed.*
==========================================================

24.3-2

26.1-7, 26.2-3

34-2 (10 points)

*Hints:*

> 26.1-7 - Consider how to modify each vertex of the original graph such that the flow *through* that vertex is converted from a *vertex capacity* to an *edge capacity* thus allowing the original maximal flow algorithms to be utilized.
>
> 34-2 - Bonnie and Clyde
	
> > a. Let there be *a* coins of type *x* and *b* coins of type *y*. Consider how many different amounts can be made with all the coins. Can this be enumerated in polynomial time?
		
> > b. Note that each larger denomination can be made *exactly* by combinations of smaller denominations (since they are all integral powers of 2). Determine the runtime of a greedy strategy where Bonnie takes the largest coin and then Clyde takes as many coins (largest remaining first) until he has the same as Bonnie, etc.
		
> > c. Another problem that can be shown to be NP-Complete is the *set-partition problem* (see problem 34.5-6 on pg. 1101) which decides whether or not given a finite set of numbers there exists a *partition* of the numbers into two sets such that the sum of the values in both sets are equal. Relate Bonnie and Clyde's problem to this one. Remember that to show a problem isis NP-complete you must *reduce* an existing NP-complete problem to this one. (Alternatively, but more difficult, is to reduce the *subset-sum* problem, described in section 34.5.5 on pg. 1097, which decides whether or not given a set of positive integers and a target value there is a subset of the integers that sum to the target.)
		
> > d. Again refer to the set-partition problem as above. Remember that to show this variant of Bonnie and Clyde is NP-complete, *assume* there is a polynomial time solution for it and show that then we could solve *every* set-partition problem by turning it into a Bonnie and Clyde variant.

