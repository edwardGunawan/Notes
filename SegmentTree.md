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


# Binary Indexed Tree (Fenwick Tree)
======================================
- The use for fenwick tree is to use the perfect sum of n arrays
    - Ex: the sum from 0-4 or the sum from 0-6
- Possibility of other alternative is to create another array that has all the sum

- Fenwick tree: Construct: O(nlogn), update: O(logn), sum: O(logn)


(Fenwick Tree)[https://www.youtube.com/watch?v=4SNzC4uNmTA]
### How does the tree is constructed?
- The root will be the dummy node which is 0
- It ris based upon the binary indexed of the tree, so the parent element is 
identified from the first 1 bit in the element and flip that, means flip the right most set bit
    - Ex: 0 is a child of 1, 2, 4, 8 because binary number of 1 if you flip it will be 0
    h4 is 100 flip it will be 0 and 8 is 1000 will be 0
- TYhe tree need to be constructed such that the parent index of an ith node is obtained 
by adding by the decimal value corresponding to the last set bit of ith.
    - Ex: parent of 9 is 1001: 9 last set bit is the first 1 so 1001 + 0001 => the parent node of 9
```
    // starting from index+1 for every index in arr[]
    // Add the value from the array to the corresponding nodes and their ancestor parents
    void updateBIT(int BIT[], int n, int index, int val){
        index = index+1;

        while(index <= n){
            BIT[index]+=val;
            index += index &(-index); // getting the parent index
        }
    }
```


### Get the sum Operation of the BIT
- The update opearation, instead of constructing the tree, can also be used simply 
update nodes in the BIT individually.
- The value will be the same as we constructing the tree, but the parent and the child
relationship will be based upon subtracting the LSB

- Therefore, building tree in this way and do the same operation for getting the value
of the tree
```
    int getSum(int [] BIT, int index){
        int sum = 0;
        index = index+1;
        while(index>0){
            sum+= BIT[index];
            index -= index &(-index); // index & (-index) get the LSB
        }
        return sum;
    }
```


- Great BIT with explanation (LeetCode)[https://discuss.leetcode.com/topic/31599/java-using-binary-indexed-tree-with-clear-explanation]
