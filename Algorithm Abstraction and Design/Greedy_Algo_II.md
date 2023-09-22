#### Dijkstra's Algorithm
- Finding the min-weight path between two nodes in a directed graph given edge weights $\geq$ 0, source $s \in V$, and destination $t \in V$, find a shortest directed path from $s$ to $t$
###### Conceptual:
- Maintain a set of explored nodes S for which algorithm has determined $d[u]$ = length of a shortest $s\rightarrow u$ path
	- Find a vertex that is not yet included in the set $S$ and has a minimum distance from the sort
###### Proof of Correctness
- For each node $u \in S$: $d[u]$ = length of a shortest $s \rightarrow u$ path
- Proof by Induction on $| S |$ 
- Base Case: $|S|$ = 1 is easy since $S$ = {$s$}
	- 