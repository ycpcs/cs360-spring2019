---
layout: default
title: "Lecture 25: Maximal Flow - Ford-Fulkerson Algorithm"
---

Last lecture provided the framework for maximum flow problems and proved the key theorem - max-flow min-cut - that all algorithms are based on. This lecture we will investigate an algorithm for computing maximal flows known as *Ford-Fulkerson*.

Ford-Fulkerson Algorithm
========================

The *Ford-Fulkerson algorithm* builds upon the general strategy presented last time.

<pre>
	1.  for each edge (u,v) ∈ G.E
	2.     (u,v).f = 0
	3.  while there exists a path p from s to t in the residual network G<sub>f</sub>
	4.     c<sub>f</sub>(p) = min{ c<sub>f</sub>(u,v) : (u,v) is in p}
	5.     for each edge (u,v) in p
	6.        if (u,v) ∈ E
	7.           (u,v).f = (u,v).f + c<sub>f</sub>(p)
	8.        else
	9.           (v,u).f = (v,u).f - c<sub>f</sub>(p)
</pre>

This algorithm runs efficiently as long as the value of the maximal flow \|*f* <sup>\*</sup>\| is reasonably small or if poor augmenting paths are avoided.

Edmonds-Karp Algorithm
======================

An extension that improves upon the basic Ford-Fulkerson method is the *Edmonds-Karp algorithm*. This algorithm finds the augmenting path using BFS with all edges in the residual network being given a weight of 1. Thus BFS finds a *shortest path* (in terms of number of edges) to use as the augmenting path. With this modification, it can be shown that Edmonds-Karp runs in O(*VE*<sup>2</sup>).

**Example**

Consider the following flow network

> ![image](images/lecture25/MaxFlowexample.png)

Note that clearly \|*f* <sup>\*</sup>\| ≤ 24 (the smaller of the capacities leaving the source or entering the sink).

*Iteration 1:* Choose the augmenting path *p*<sub>1</sub> = \< *s*, 1, 3, *t* \> which has *c*<sub>f</sub>(*p*<sub>1</sub>) = 12 (due to *c*(1,3)) giving the residual network

> ![image](images/lecture25/MaxFlowexample1.png)

*Iteration 2:* Choose the augmenting path *p*<sub>2</sub> = \< *s*, 2, 4, *t* \> which has *c*<sub>f</sub>(*p*<sub>2</sub>) = 4 (due to *c*(4,*t*)) giving the residual network

> ![image](images/lecture25/MaxFlowexample2.png)

*Iteration 3:* Choose the augmenting path *p*<sub>3</sub> = \< *s*, 2, 4, 3, *t* \> which has *c*<sub>f</sub>(*p*<sub>3</sub>) = 7 (due to *c*(4,3)) giving the residual network

> ![image](images/lecture25/MaxFlowexample3.png)

At this point there are no other augmenting paths (since vertex 3 is the only vertex with additional capacity to the sink but has no flow in from other vertices). Hence the final flow network with a min-cut shown is

> ![image](images/lecture25/MaxFlowexample4.png)

with maximal flow \|*f* <sup>\*</sup>\| = 19 + 4 = 23 (or 12 + 11 = 23).

