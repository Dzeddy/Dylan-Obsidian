G = (V,E)
E = edges between pairs of nodes
Captures pairwise relationship between objects
Graph size parameters: $n = |V|, m = |E|$ 
$V = \{1,2,3,4,5,6,7,8\}$
$E = \{1-2,1-3,2-3,2-4,2-5,3-5,3-7,3-8,4-5,5-6,7-8\}$
$m = 11, n = 8$

#### Graph Representation: Adjacency Matrix
- Space is $n^2$
- Two representations of each edge
- Checking if value is edge takes $\Theta(1)$ time
- Identifying all edges takes $\Theta(n^2)$ time

#### Graph Representation: Adjacency List
- O(m + n) space
- Checking edges takes $O(degree(u))$ time
- Identifying all edges takes $\Theta(m + n)$ time

#### Paths
- A path in an undirected graph is a sequence of nodes with the property that each consecutive pair is joined by a different edge in $E$
- 