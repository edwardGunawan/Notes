## Array and String
### Hashtable
#### AverageCase
| Search | Insert | Deletion | Access |
| ------ | ------ | -------- | ------ |
|   O(1) |   O(n) |   O(1)   |  N/A
- fast lookup
- Hash value of all possible key must be unique
- Implementing we can have small array with linkedlist
hash value will be hash(key) % array_length
- Implement Hashtable with binary search tree, 
guarantee O(logn) loook up time.
    * but we need to use less space

### ArrayList
| Search | Insert | Deletion | Access |
| ------ | ------ | -------- | ------ |
| O(n)   |  O(n)  | O(n)     |  O(1)  |


- Array Access is o(1) because we speaking just accessing it
- insert is O(n) because [2,4,6,8]
    * Inserting - at the beginning of the array: have to move all 4 elements down
- Same thing with delete where you will need to allocate the space after
deleting it



### StringBuffer
- Every concatenation on string, two strings are copied
over, character by character
- Require O(xn^2) because 
    * first iteration need to copy x character, 2nd 2x
    ( this will become O(x^2), O(x + 2x + ...+ xn))
- Stringbuffer simple creates an array of all the strings,
copying them back to a string only when necessary


## LinkedList
- Create LinkedList from Scratch
- The runner technique: you iterate through the linkedList with two
pointers simultaneously, with one ahead of the other. The fast node might be 
ahead by fixed amount or hopping nodes when iterating through. 
- Recursive algorithm will take O(n) space, where n is the depth of the 
recursive call. All recursive method can be implement iteratively, although
they might be much more complex.


## Trees and Graphs
- Fluency in implementing a tree or graph from scratch will prove essential
- Be sure to watch out for a the following issues and seek clarification
when necessary:
    * Binary Tree vs Binary Search Tree:
    a binary search tree imposes the condition that for all nodes, the left
    children are less than or equal to the current node, which is less than all the right nodes
    * Balanced vs Unbalanced
    * Binary Tree Traversal: in-order,post-rder,
    and pre-order traversal.
        * Most common is in-order, left, current, right
    * Graph Traversal: (know how to implement them)
        * BFS: using ** queue **, finding the shortest path of the vertex, finding neighbor nodes,
        GPS system to find nearby location, social network to find people in the specified
        distance
        * DFS: using stack, is typically the easiest if we want to visit every node
        in the graph, or at least visit every node until we find whatever we're looking
        for. However, if we have a very large tree and we want to be prepared to
            quit when we get too far from the original node, DFS can be problematic.


## Stacks & Queue
- Fundamental data types
    * Value: Collections of objects
    * Operations: insert, remove, iterate, test if empty
        * Intent is clear when we insert
        * When remove:
            * Stack: Examine the item most recently added <- LIFO
            * Queue: Examine the item last recently added <- FIFO
### Stack
  - Stacks of string data types
  ```
    public class Stack of String
    stackOfString() : create empty stack
    String pop(): remove and return the string most recently added
    boolean isEmpty() : is the stack empty

  ```
  - Implement using linkedList, or resizable array
  ```
    Linked List : 
    inner class: private class Node{
                            String item;
                            Node next;
                          }
    void push(String item){
         Node i = new Node(item);
         i.next = first;
         first = i;
    }

    String pop(){
        Node toDelete = first;
        first = first.next;
        return toDelete.item;
    }

    isEmpty(){
        return first == null;
    }
  ```

  - Performance: Constant time on push and pop
  
  - *Note* to implementing stack: 
    * Overflow
    * Null items
    * Loitering: holding reerence to an object when it is no longer needed
  ```
  Array:
    Use array s[] to store N Items on stack
    push(): add new item at s[N]
    pop(): remove item from s[N-1]

    public boolean is Empty(){ return N==0;}
    public void push(String item) { s[N++] = item;}
    public String pop() { return s[--N];}

    Resizing array:
    Repeat doubling: if array is full create new Array of twice the size
    public ResizingArrayStackOfString(){ s = new String[1];}
    public void push(String item){
        if(N == s.length){ resize(2*s.length); // add twice as large}
        s[N++] = item;
    }
    private void resize(int capacity){
        String [] copy = new String[capacity];
        for(int i =0; i< N; i++){
            copy[i] = s[i];
        }
        s= copy;
    }

    shrink array:
    push() : double size of array[] when array is full
    pop() : halve size of array s[] when array is on quarter full
    public String pop(){
        String item = s[--N];
        s[N] = null;
        if(N>0 && N== s.length/4) resize(s.length/2);
        return ite;
    }

    therefore: array is always in 25% to 100% full

  ```

  - Cost of inserting first N items:
    * N (array access/push) + (2+4+8...+N)(k any access to double to size k) ~ 3N
  - Array resizing not happen quite often, the memory is also a constant multiple,
  so amortized value will be constant.

  - Average running time for array:
    * amotized: O(1) on push and pop
    * worst case: O(N)
    * resizing will be called logarithmic, since it is double the size
  - Trade off of linkedlist vs Array
    * Linked list: 
        * worst case operation take constant time
        * use extra time and space to deal with the links
        * be sure that every operation is going to be fast
    * Array:
        * every operation takes contant amortized time
        * less wasted space
        * If total amount of time will be much less because individual operation are fast

### Queue

```
    QueueOfString();
    void enqueue(String item);
    String dequeue();
    boolean isEmpty();

    * maintain two pointer to first and last nodes of the list
    * insert fro mthe end o fthe list, remove from the front of the list FIFO

    implementation:
    dequeue() {
        String item = first.item;
        first = first.next;
        return item;
    }
    enqueue(String item){
        Node i = new Node(item);
        last.next = i;
        if(isEmpty()) first = last;
        else last = i;
    }

```

- Resizing array implementation:
    * Maintain two pointer: head and tail
    * enqueue: add new item at q[tail];
    * dequeue: remove item at q[head];
    * once past capacity, you ahve to put it back to 0, and check to resizing


### Generic
- Avoid casting in client
- Welcome compile time error, instead of run-time error
- replcae the type and replcae it with the generic type name
- Generic array creation is not allowed in java --> (item[]) new Object[capacity] (ugly cast)
- Good code has no cast.


### Iterator (use this as collection of obejct, Bag API)
- Purpose: want client ot just iterate through the collection
- Make stack implementation the iterable iterface
    * in java:
        * itearble: method that return iterator
        * iterator: boolean hasNext and item next()
- Reason: Create an elegant client code 
    * ex: forEach(string s : stack) ....

``` 
    public calss Stack<Item> implements iterable<item>{
        public iterator<item> iterator(){
            new ListIterator();
            }
        private class ListIterator implements Iterator<Item>{
            private Node current = first;

            public boolean hasNext() return current!= null;
            public item next()
                Item item = current.item;
                current = current.next;
                return item;
```

- Array in iterator for stack will be reverse iteration if you want to implement
it in queue, but for linked list, you don't have to change it

