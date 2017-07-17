## Three Criteria
- Memory
- Space
- Using Asymptotic notation for that

**it is common to identify vertices not by name (such as "Audry", "Boston", or "sweater")
but instaed by a number**

- We typically number the |V| vertices from 0 to |V|-1

1. Edge Lists
2. Adjacency Matrices
3. Adjacency List

# Edge Lists
- a list, or array, of |E| edges. 
- To represent an edge, we just have an array of 2 vertex numbers, or an array of
objects containing the vertex number of the vertices
- if the edge have weights, then add the third element to the array or more information to the
object, giving the edge's weight
- total space for an edge list is \theta (E) 
- Ex: [[0,1],[0,6],[0,8],[1,4],[1,6],[1,9],[2,4],[2,6],[3,4],[3,5].[3,8],[4,5]]
So each [0,1] means the vertex number of 0 and 1, which 0 ---- 1 and [0,6] means 0 --- 6 so 0 is also
connected to vertex 6
- Edge list are simple, but if we want to find whether a particular edge is in the graph or not
we have to search throuh linear |E| edges.

# Adjacency Matrices
- For a graph with |V| vertices, an adjacency matrix is a |V| x |V| matrix of 0s and 1s, **where the entry in
row i and column j is 1** if and only if the edge (i,j) is in the graph
- It will be a matrix, and the value of the vertex represent the index m, n in the matrix, 
if there is a connection between 0 and 1 then row 0 and column 1 (0,1) will be mark 1
- With Adjacency Matrices we can find whether the edge is present in the graph in constant time,
just look at the corresponding entry in the matrix
- Ex: see whether edge (i,j) is in the graph by looking at graph[i][j]
- Disadvantage : V^2 space even if the graph is sparse, relatively few edges, if you are 
ask if to find all vertex that is adjacent to the given vertex i, you will need to run |V| entries in row i,
even if it is parse (because you see if it is 1 then it is the adjacent of vertex i)
- For an undirect graph, the adjacency matrix is symmetric: the row i, column j entry is 1 if and only if the 
row j, column i entry is 1.
- For directed graph, the adjacency matrix need not be symmetric.

# Adjacncy Lists-
- for each vertex i, store an array of the vertices adjacent to it.
- Typically will have an array of |V| adjacency lists, one adjacency list per vetex,
```
ex: [ 
        [1,6,8],
        [0,4,6,9],
        [4,6],
        [4,5,8],
        [1,2,3,5,9],
        [3,4,],
        [0,1,2],
        [8,9],
        [0,3,7],
        [1,4,7]
    ]
```

- It doesn't have to be in any particular order, although it will be good 
to be in an increasing order.
- Now, if you want to find if all adjacent list in vertex i, you are able to 
do it in constant time, because you just index on that particular array and 
look at it in that particular list. 
- it will take \theta (d) for the time to find the adjacency list, depending on the 
degree of the vertex i 
- if the edge is weighted, then the item in each adjacency list can either be an object
or a 2 item. 
- Space complexity of adjacency list: |V| list, although each list could have as many as 
|V| - 1 vertices. 
- Undirected graph adjacency list: 2|E|, because each i,j will contain duplicate, one in i list, and 
the other in j list, and there are E edges. 
- For directed graph with 1 edge, on each vertex, it will be |E| because each list will only have 1 value.
