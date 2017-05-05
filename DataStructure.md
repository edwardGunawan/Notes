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


