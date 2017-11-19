# Segment Tree
==================
- Segment tree can be used to do preprocessing and query in moderate time.

- Questions can be used in Segment Tree is like Sum of given range.
    - have array[0...n-1] find the sum of the lement from index l and r,
    - Changevalue of a specific element of the array to a new value x
    - One solution is to create another array and store sum from start to i at the ith
    index in this array. Sum ofa given range can now be calculated in O(1) time, but update
    operation takes O(n) time now. This works well if the number of query operations are large
    and very few updates.
    - Segment Tree can make query and update opearation **O(logn)**

#### Representation of Segment Tree
1. Leaf Nodes are the elements of the input array.
2. Each internal node represents some merging of the leaf nodes. The merging may be 
different for different problems. For this problem, merging is sum of leaves under a node.

- For array representation of tree is used to represent Segment Trees. For each node
at index i, the left child is at index 2*i+1, right child at 2*i+2 an the parent is at floor((i-1)/2)

#### Construction of Segment Tree from given array
- We start with segment arr[0...n-1] and every time we divide the current segment into 
two halves, and then call the same procedure on both halves.
- All levels of the constructed segment tree will be completely filled except the last level.
- It will be a Full binary Tree because we divide segments in two halves at every level.
- Total node will be ```2*n-1```
- Height of the segment tree will be log2n. Since tree is representing using array
and relation between parent and child indexes must be maintained, size of memory allocated for segment tree
will be ```2*2log2n-1```


- Query for Sum of given range
```
    int getSum(node, l, r)
    {
        if range of node is within l and r
             return value in node
        else if range of node is completely outside l and r
             return 0
        else 
        return getSum(node's left child, l, r) + getSum(node's right child,l,r)
     }
```

- Update a value: like tree construction and query operations, update can also be 
done recursively. We are given an index which needs to updated.
    - Let diff be the value to be added. We start from root of the segment tree,
    and add diff to all nodes which have given index in their range.
    - If a node doesn't have given index in its range, we don't make any changees to that node.

Time Complexity: tree construction is O(n), Query: O(logn), to query a sum, we process at most four nodes at every
level and number of levels is O(logn), update is also O(logn) to update a leaf value, 
we process one node at every level and number of levels is O(logn)

Geeks for geeks [Segment Tree](http://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)
