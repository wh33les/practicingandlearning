# Examples of data structures, in C

## Arrays (a.k.a. _lists_ or _vectors_) 
<details>
<summary>Click to expand. </summary>

An __array__ is a data structure consisting of a list of __elements__ of the same type, for example integers, floats, or characters.  A character array is sometimes referred to as a __string__.  An array's length _n_ is fixed unless it is a __dynamic array__, which for example can double in length when the number of elements assigned to it has exceeded _n_.  Elements of an array are given by their __index__, or position in the array.  In C, indices begin at 0.  In other languages indices can begin at 1.  An array may be sorted or unsorted.
```c
/* Prompts the user to create an array of digits from 0 to 9 of size ARRAY_SIZE_n 
*/
#include <stdio.h>
#define ARRAY_SIZE_n 10 // In this example I've decided n=10.

int main()
{
  /* Local definitions */
  int exampleArray[ARRAY_SIZE_n]; // defines the array exampleArray with size ARRAY_SIZE_n 
  int i; // counter variable for use in loops
  /* Gather input from the user */
  for( i = 0; i < ARRAY_SIZE_n; i++ )
  {	  
    printf("Enter a digit from 0 to 9: "); // prompts the user for an entry of the array 
    scanf("%d", &exampleArray[i]); // assigns the user's input value to exampleArray[i] 
    while( exampleArray[i] < 0 || exampleArray[i] > 9 ) // ensures the user follows the instructions
	{	
	  printf("No, enter a DIGIT, FROM 0 TO 9: "); // but presumes input is of type int
	  scanf("%d", &exampleArray[i]);
	} /* while */	
  } /* for i */	
  /* Print the array */
  printf("Here's the array: \n { ");
  for( i = 0; i < ARRAY_SIZE_n; i++ )
  {
    if( i != ARRAY_SIZE_n - 1 )
	  printf("%d, ", exampleArray[i]);
	else 
	  printf("%d", exampleArray[i]);
  } /* for i */
  printf(" }"); 
  /* Return */
  return 0;
} /* main */
```
### Pros 
* Constant-time access, as long as the address of an element is known.  
* Efficient storage, since no formatting data or pointers are associated.  
* Memory locality, i.e., elements are next to each other in memory.  
* Unsorted arrays: fast for maintenance (e.g., add, remove) operations. 
### Cons 
* Unsorted arrays: slow for search operations (e.g., successor/predecessor, minimum/maximum). 
### Big-Oh properties of basic operations (e.g., find, add, remove)
Operation | Unsorted | Sorted
--------- | -------- | ------
Find | _O(n)_ | _O(_ log _n)_
Add | _O(1)_ | _O(n)_
Remove | _O(1)_ | _O(n)_
Successor | _O(n)_ | _O(1)_
Predecessor | _O(n)_ | _O(1)_
Min | _O(n)_ | _O(1)_
Max | _O(n)_ | _O(1)_

__Question:__ Why is deletion _O(1)_ for unsorted lists?
</details>

## Linked lists
<details>
<summary>Click to expand. </summary>

A __linked list__ is an array with an additional structure, such that each element can have at least one pointer to another element or elements in the array.  In a __singly-linked__ list, each element (besides the last) contains a pointer to the next element in the array.  In a __doubly-linked__ list, each element (besides the first), in addition, has a pointer to its predecessor.  
```c
typedef struct { /* Linked lists are not predefined data types the way arrays are. */ 
} 
```
### Pros 
* For large lists, pointers to data are often faster to move and manipulate than the data itself.  
* Insertion and deletion becomes more efficient than for unlinked lists.
### Cons 
* To associate pointers to data takes more memory. 
### Big-Oh properties of basic operations (e.g., find, add, remove)
(_n_ = no. of elements in the array)

Operation | Unsorted | Sorted
--------- | -------- | ------
Find | _O(n)_ | _O(n)_
Add | _O(1)_ | _O(n)_
Remove | _O(n)_ (singly-); _O(1)_ (doubly-) | _O(n)_ (singly-); _O(1)_ (doubly-)
Successor | _O(n)_ | _O(1)_
Predecessor | _O(n)_ | _O(n)_ (singly-); _O(1)_ (doubly-) 
Min | _O(n)_ | _O(1)_
Max | _O(n)_ | _O(1)_

__Questions:__ 
1. Why isn't the search operation _O(_ log _n)_ for sorted linked lists?
1. Why is deletion _O(n)_ for unsorted singly-linked lists?
1. Why is deletion _O(1)_ for sorted doubly-linked lists?
1. Why is max _O(1)_ for unsorted singly-linked lists?
</details>

## Queues
<details>
<summary>Click to expand. </summary>

A __queue__ is a container structure in which data is accessed in the order in which it was stored.  In other words, it is a set whose Remove (__Dequeue__) operation satisifies "first in, first out" (FIFO).  The Add operation is called __Enqueue__.  A queue can be implemented using a doubly-linked list _Q_ with attributes _Q.head_ and _Q.tail_.  
```c
typedef struct {
} 
```
### Pros
* Not necessary to predetermine its size.
### Cons
</details>

## Stacks
<details>
<summary>Click to expand. </summary>

A __stack__ is a container structure in which data is accessed in the reverse order in which it was stored.  In other words, data accessed is independent of content and satisfies "last in, first out" (LIFO).  One way to implement a stack is using an unsorted array of fixed size.
```c 
typedef struct {
  item_type theStack[];
  int top;
} stack;
int push(stack S, item_type x)
{
  S.top = S.top + 1;
  S[S.top] = x;
  return 0;
}
item_type pop(stack S)
{
  if S.top == 0 
    error "underflow";
  else S.top = S.top - 1
  return S[S.top+1];
}
```
### Pros
* Used in backtracking.
* Best for when retrieval order doesn't matter.
### Cons
* Use by programming languages presents security issues.

Used in a depth-first search on a graph.

Operation | Efficiency 
--------- | -------- 
Add (Push) | _O(1)_ 
Remove (Pop) | _O(1)_ 

</details>

## Hashtables

## Binary search trees
<details>
<summary>Click to expand. </summary>

A __binary search tree__ is a binary tree with a unique labelling such that for any __node__ (vertex) with key _x_, all nodes to the left of _x_ have key values strictly less than _x_ and all nodes to the right have key values strictly larger than _x_.  Basic dictionary operations on a binary search tree are proportional the the height _h_ of the tree.  In a worst-case scenario, the tree may consist of a single chain and _h=n_, the total number of nodes on the tree.  However, it can be shown that the expected height of a randomly built binary search tree is proportional to lg _n_.
```c
/* Type declaration for a binary search tree 
*/
```
### Pros
### Cons
### Big-Oh properties 
(_h_ = height of the tree; between lg _n_ and _n_)

Operation | Worst time
--------- | ----------
Find | _O(h)_ 
Add | _O(h)_ 
Remove | _O(h)_  
Successor | _O(h)_ 
Predecessor | _O(h)_ 
Min | _O(h)_ 
Max | _O(h)_ 
</details>

## Priority queues/ heaps
A __heap__ is a binary tree which is completely filled up to its last row, which is then filled from the left to a certain point.  Each node  of the tree is stored as an element in an array.  The attributes of an array _A[0..n-1]_ that represents a heap are its length (_n_) and the size of the heap, which may be less than _A.length_.  
```c
typedef struct {
  int A[n]; /* n = A.length */
  int heap_size; /* A.heap-size */
} heap;  
```
If the root of the tree has index _0_ then each node _i_ has a left and right __child__, along with a __parent__.  The attributes of an element _A[i]_ for _0 <= i < A.heap-size_ are given in the following table:

Attribute | Value
----------|------
_A[i].parent_ | _A[ceiling(i/2)-1]_
_A[i].left_ | _A[2i+1]_
_A[i].right_ | _A[2(i+1)]_

If a value cannot be computed, for example, if _2i > A.heap-size_, then the value is `nil`.

A __(max-)priority queue__ is a set _S_ permitting the usual dictionary operations Add and Max, along with ExtractMax, which finds and removes the largest key from _S_, and IncreaseKey, which increases the value of a key _x_ in _S_ to a new value, _k_.  A heap can be used to implement a priority queue.  
### Pros
* A heap can demonstrate a hierchary structure among data without using pointers.  The attributes `parent`, `left`, and `right` are all given by formulas.
* Inserting a new element into a priority queue does not require reshifting of all existing keys; in fact, it only takes logarithmic time.  
### Cons
* Heaps only give a partial order.  Keys on the same level of the tree are incomparable.

A priority queue can also be implemented using a sorted or unsorted array, by including a pointer to the highest priority (e.g., max) entry.  The pointer gets updated upon insertion/building or deleting.
```c
typedef struct {
}
```
### Big-Oh properties 
Operation | Heap (or any balanced tree) | Unsorted array | Sorted array
--------- | --------------------------- | -------------- | ------------
Add | _O(_ lg _n)_ | _O(1)_ | _O(n)_
ExtractMax (Remove) | _O(_ lg _n)_ | _O(n)_ | O(1)   
Max | _O(1)_ | _O(1)_ | _O(1)_
