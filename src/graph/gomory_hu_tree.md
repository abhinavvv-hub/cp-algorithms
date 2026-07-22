# Gomory-Hu Tree

This article discusses an advanced Data Structure used in Graph Theory **Gomory-Hu Tree**.

## Problem Statement

Let $G = (V, E)$ be an Undirected Graph with non-negative edge weights. We would like to be able to compute the global minimum cut on the graph (i.e., the minimum
over all min-cuts between pairs of vertices `s` and `t`, where s, t &isin; V ). 

##
Clearly, this can be done by computing the minimum cut for all pairs $$\genfrac{(}{)}{0pt}{0}{n}{2}$$ of vertices, but this can take a lot of time. Gomory and Hu showed that the number of distinct cuts in the graph is at most n − 1, and furthermore that there is an efficient tree structure that can be maintained to compute this set of distinct cuts.
Well, of course one can use a Randomized Algorithm like Karger-Stein which finds the global minimum cut in $O(n^2 log n)$ with a high probability. But here, we will discuss the deterministic Polynomial time Algorithm of finding that Global Minimum Cut.

> [!NOTE]
> Gomory-Hu trees work because the cut function is both submodular and symmetric.
