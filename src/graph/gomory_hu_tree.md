# Gomory-Hu Tree

This article discusses an advanced Data Structure used in Graph Theory, that is, **Gomory-Hu Tree**.

## Problem Statement

Let $G = (V, E)$ be an Undirected Graph with non-negative edge weights. We would like to be able to compute the global minimum cut on the graph (i.e., the minimum
over all min-cuts between pairs of vertices `s` and `t`). 

##
Clearly, this can be done by computing the minimum cut for all pairs $$\genfrac{(}{)}{0pt}{0}{n}{2}$$ of vertices, but this can take a lot of time. Gomory and Hu showed that the number of distinct cuts in the graph is at most n − 1, and furthermore that there is an efficient tree structure that can be maintained to compute this set of distinct cuts.
Well, of course one can use a Randomized Algorithm like Karger-Stein which finds the global minimum cut in $O(n^2 log n)$ with a high probability. But here, we will discuss the deterministic Polynomial time Algorithm of finding that Global Minimum Cut.

> [!NOTE]
> Gomory-Hu trees work because the cut function is both submodular and symmetric.

A cut is a partition of the vertices V into two sets S and T.
Any edge $(u, v) &isin; E$ with $u &isin; S$ and $v &isin; T$ is said to be **crossing the cut** and hence, it is a **cut edge**.
The **capacity of a cut** is the sum of weights of the edges crossing the cut.

A u-v cut is a split of the nodes into two disjoint sets `U` and `V`, such that $u &isin; U, v &isin; V$.

Given a graph $G = (V,E)$ and two terminals $u,v &isin; V$, find the minimum u-v cut.

Given a directed graph $G = (V,E)$ in which every edge $(u,v) &isin; E$ has a non-negative, real-valued capacity $c(u,v)$.

• We distinguish two vertices: a source `s` and a sink `t`.

• A flow network is a real function $f: V × V &rarr; R$ with the following properties for all nodes `u` and `v`:
1. Capacity constraints: $f(u,v) &le; c(u,v)$
2. Skew symmetry: $f(u,v) = - f(v,u)$
3. Flow conservation ,unless $u = s$ or $u = t$

Two graphs $G = (V, E)$ and $G’ = (V, E’)$ are said to be flow equivalent iff for each pair of vertices $u,v &isin; V$, the minimum u-v cut (maximal u-v flow) in `G` is the same as in `G’`.

• It turns out that there always exist a `G’` which is a tree (Gomory Hu Tree)!!

• Notice that the $n - 1$ edges of the tree correspond to the $n - 1$ distinct min-cuts in `G`.

## Gomory-Hu Tree Construction Algorithm

Algorithm 1: GomoryHuAlg(G, R)



if |R| = 1 then

      return T = ({r}, ∅), Cr = V
else

      Let r1, r2 ∈ R, and let δ(W) be an r1, r2 minimum cut 
      // Create two subinstances of the problem
      G1 = G with V \ W shrunk to a single vertex, v1; R1 = R ∩ W
      G2 = G with W shrunk to a single vertex, v2; R2 = R \ W
      T1, (C1_r | r ∈ R1) = GomoryHuAlg(G1, R1) 
      T2, (C2_r | r ∈ R2) = GomoryHuAlg(G2, R2)    
      // Note that r' and r'' are not necessarily r1, r2!
      Let r' be the vertex such that v1 ∈ C1_r'
      Let r'' be the vertex such that v2 ∈ C2_r''
      T = (R1 ∪ R2, ET1 ∪ ET2 ∪ {rr'})
      (Cr | r ∈ R) = ComputePartitions(R1, R2, C1_r, C2_r, r', r'')
      return T, Cr
end if

======================================================================

Algorithm 2: ComputePartitions(R1, R2, C1_r, C2_r, r', r'')

// We use the returned partitions, except we remove v1 and v2 from Cr' and Cr'', respectively
For r ∈ R1, r ≠ r'

    Cr = C1_r
For r ∈ R2, r ≠ r''

        Cr = C2_r
Cr' = C1_r' - {v1}

Cr'' = C2_r'' - {v2}

return (Cr | r ∈ R)
