# implement Maximal Tourism from HackerRank:
```

import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        int m = in.nextInt();
        int[][] route = new int[m][2];
        for(int route_i=0; route_i < m; route_i++){
            for(int route_j=0; route_j < 2; route_j++){
                route[route_i][route_j] = in.nextInt();
                }
            }
     //   System.out.println(max);
        int [] arr = new int[n+1];
        int [] sz = new int[n+1];
        
        for(int i =0; i< m ; i++){
            int first = route[i][0];
            int second = route[i][1]; 
            arr[first] = first;
            arr[second] = second;
            sz[first] = 1;
            sz[second] = 1;
           // debug(arr);
        }
        
        for( int i =0; i<m; i++){
            int first = route[i][0];
            int second = route[i][1];
            union(first,second,arr,sz);
            //debug(arr);
            //debug(sz);
        }
        
        int res = 0;
        for(int i: sz){
            if(res < i){
                res = i;
            }
        }
        System.out.println(res);
    }
    
    private static int find(int i, int[] arr){
        while(i != arr[i] ) {
            arr[i] = arr[arr[i]];
            i = arr[i];
        }
        return i;
    }
    
    private static void union(int i, int j, int[] arr, int[] sz){
        int parent_i = find(i, arr);
        int parent_j = find(j, arr);
        if(parent_i != parent_j){
            if(sz[parent_i] >= sz[parent_j]){
//            System.out.println("in bigger or equal : " + parent_i + " , " + parent_j);
            arr[parent_j] = parent_i;
            sz[parent_i] += sz[parent_j];
            //sz[parent_j] = sz[parent_i];
            }else if(sz[parent_i] < sz[parent_j]){
               // System.out.println(" in less than: " + parent_i + " , " + parent_j);
                arr[parent_i] = parent_j;
                sz[parent_j] += sz[parent_i];
            }    
        }
        
    }
    private static void debug(int[] arr){
        for(int i : arr){
            System.out.print(i + ", ");
        }
        System.out.println();
    }
        
}
```

# Notes About Union_find
## Union_find: 
- Union command: connect two objects

is connected to: 
- Reflexive: p is connected to p
- Symmetric: if p is connected to q, then q is connected to p
- Transitive: if p is connected to q and q is connected to r, then p is connected to r.
- Connected components: Maximal set of objects that are mutually connected.

## Implement the operations:
### Find query: check if two objects are in the same component.
### Union command: replace components containing two objects with their union.

###  Goal:
    * Design efficient data structure for union-find.
    * Number of objects N can be huge.
    * Number of operations M can be huge.
    * Find queries and union commands may be intermixed
###  Class UF:
    * UF(int N) initialized union -find data structure with N objects (0 to N-1)
    * check for two series and see if it exist or not, if it doesn’t exist or connected between the two component, then union them.
### Quick find:
    * DS: integer array id[] of size N
    * interpretation: p and q are connected iff they have the same id
    * find: check if p and q have the same id, and if they are in the same id, then they will have the same component
    * union: merge components containing p and q, change all entires whose id equals id[p] to id[q].
        * kind of hard: you have to change for all the things that connected to one id to the other id
        * every time when you connected, or union, you have to loop through the entire array and changing all the entry of the same value with the first value to the second value id[q].
        ```
             quickFind (int N){
                id = new int[N];
                for(int i =0; i<N;i++){
                    id[i] = i;
                }
            connected(int p, int q){
                return id[p] == id[q];
            }
            unnion(int p, int q){
                int pid = id[p];
                int aid = id[q];
                for(int i =0; i<id.length; i++){
                    if(id[i]==pid) id[i] = qid; 
                }
            }
            ```
        * computation implementation: loop through N for the array, then union is very expensive, quadratic operation: N^2
### Quick union: lazy approach , same data structure, array id[] size N
    * interpretation : id[i] is parent of i, each entry of the array will contact reference to the parent, so the index of the parent is pointing to the value, so the root will pointing to itself
    * find: check if p and q have the same root, by checking if they are in the same connected component
    * Union: merge components containing p and q, set the id of p’s root to the id of q’s root. so it just change the one value of id[p] to q to make it pointing to the parent, but find require more work.
    * private finding root by chasing parent pointer, you can do while to do it while(i != id[i])
    * union —> find the two root, then set them equal
    * Quick union is faster than quick find, but its too slow still, because the tree can get too tall, which means if it is a linkedList, it will cost O(n)
### Quick union improvements: 
    * weighting : takes step to avoid having tall trees, keep track of the number of each tree, maintain balance by making sure that linking the smaller tree to the larger tree
    * DataStructure: same, but extra array each item gives the number of object in the tree rooted at i
    * Find: return root(p) == root(q);
    * union: modify quick union to: 
    * Always check if the parent are equal or not, if they are equal don’t do anything
        * link root of smaller tree to root of larger tree.
        * update the sz[] array.
        ```
         int j = root(p);
         int j = root(q);
         if(i == j) return;
         if(sz[i] < sz[j]) { id[i] = j; sz[j] += sz[i];}
         else { id[j] = j; sz[i] += sz[j];}
        ```
    * Running time: 
        * Find: takes time proportional to depth of p and q
        * Union: takes constant time, given roots.
        * Proposition: average case, it will go through logN because it goes through the depth of it.
    * Path compression: while traversing through, make every other node in the path point to its grandparent, thereby halving path length to make the tree more flat. by doing id[i] = id[id[i]]; 
    * No such algorithm that is linear.
### Application of Union-find:
    * Percolation 

