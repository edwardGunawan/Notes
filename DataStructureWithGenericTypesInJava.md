# Data Structures with Generic Types in Java


## Interface
* An interface tells us nothing about how the data structure and the semantics, or meaning, of those operations. It only provides a list of supported operations along the specification about what types of arguments each operation accepts and the value returned by each operation
* A data structure implementation includes internal representation of the data structure as well as the definition of the algorithms that implement the operations supported by the data strucutre.


### Queue Interface
* Add(x): it adds the value x to the queue
* remove(): it removes the next value , y from the queue and returns y
* The FIFO queue removes items in the same order they were added, much, in the same way, a queue (or a line-up) works when checking out at a cash register in a grocery store.
    * add and remove operations on FIFO are often called enqueue(x) or dequeue()
* Priority Queue always removes the smallest element from the queue, breaking ties arbitrarily. This is similar to the way in which patients are triaged in a hospital emergency room. As patients arrive they are evaluated and then placed in a waiting room. When a doctor becomes available, they first treat the patient with the most life-threatening condition.
    * The remove() operation on a priority queue is usually called deleteMin()
* LIFO Queue is called a stack. Visualized in terms of stack of plates; plates are placed on the top of the stack and also removed from the top of the stack.
    * Add and remove is usually called push() and pop()
* Deque is a generalized of both FIFO(Queue) and LIFO(Stack)
    * Deque repreesnts a sequence of with a front and a back. Elements can be added at the front of the sequence or the back of the sequence.
    * addFirst(x)
    * removeFirst()
    * addLast(x)
    * removeLast()

### List Interface
- `size()`: it returns `n` length of the list
- `get(i)`: it returns the value xi
- `set(i, x)`: it sets teh value of x equals to x
- `add(i,x)`: it adds x at position i
- `remove(i)`: it removes the value xi, displacing xi+1, ..., xn-1;

These oepration are easily sufficient to implement the Deque interface:
```
addFirst(x) => add(0, x)
removeFirst() => remove(0)
addLast(x) => add(size, x)
removeLast() => remove(size()-1)
```

The terms Stack and Deque are sometimes used in the names of data structures that implement the List interface. When this happens, it highlights the fact that these data structures can be used to implement the Stack or Deque interface very efficiently. For example, the ArrayDeque class is an implementation of the List interface that implements all the Deque operations in constant time per operation.

### The USet interface: unordered sets
- unordered sets of unique elements
- `size()`: it reutrns the number of elements, n, in the set
- `add(x)`: it adds the element x to the set if not already presetn; it adds x to the set provided that there is no element y in the set such that x equals y. It returns true if x was added to the set and false otherwise.
- `remove(x)`: it removes x from teh set; it finds an element y in teh set such that x equals y and remove y. It returns y, or null if no such element exists.
- `find(x)`: it finds x in the set if it exists; it finds an element y in the set such that y equals x. It returns y, or null if no such element exists.

- IN java this is by overriding the class `equals(y)` and `hashCode()` methods.
- `Pairs`: two key are equal if their keys are equal.

### SSet: sorted sets
- `SSet` stores elements from some total order ,so that any two elements x and y can be compared. (TreeSet)
- This will be done with method called `compare(x,y)` which:

```
- if x < y, then the resulting value is negative
- if x > y, then the resulting value is positive
- if x = y, then the resulting value is 0
```

The difference semantic from USet and SSet is the `find(x)` method: it locates x in teh sorted set, it finds the smallest element y in teh set such tat y >= x. It returns y or null if no such element exists.
- this method of `find(x)` operation is sometimes referred to as successor search. IT differs in a fundamental way from `USet.find(x)` since it returns a meaningful result even when there is no element equal to x in teh set.
- `find(x)` in SSEt is logarithmic, while `find(x)` in USet is constant time.