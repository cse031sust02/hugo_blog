---
date: "2017-08-08T17:46:18+06:00"
title: "Data Structure Basics"
---

## What is Data Structure?

Data structures are ways to store data in an organized fashion so that it can be used efficiently. Just like there are many ways (i.e alphabetically or by genre) you can organize your books in a bookshelf.

#### Types
- **Linear** : Array, Linked List, Stack, Queue etc
- **Non Linear** : Tree, Graph etc

#### Operations
We can do different types of operations on different data structures. Such as : Traversing, Searching, Insertion, Deletion etc.

#### Complexity?
We can calculate complexity of different operations on different Data Structures. i.e, Complexity of Stack's push() operations is 0(1).

---

## Some Basic Data Structures

### Array

An array is a collection of homogeneous type of data elements.

	Operations: Traversing, Searching, Insertion, Deletion, Sorting, Merging
		
	Searching : Binary Search, Linear Search etc
	Sorting : Quick sort, Buuble Sort, Heap Sort etc

![Array](https://docs.oracle.com/javase/tutorial/figures/java/objects-tenElementArray.gif)

**image source** : [oracle](https://docs.oracle.com/javase/tutorial/figures/java/objects-tenElementArray.gif)

### Linked List

A Linked list is a linear collection of data elements called **nodes**. Each node has two part one is *info* and other is *link* part. info part gives information of current node and link part is the address of the next node.

	Operations: Traversing, Searching, Insertion, Deletion etc

	Types : Singly Linked List, Doubly Linked List, Circular Linked List etc 

![Linkded List](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/CPT-LinkedLists-deletingnode.svg/380px-CPT-LinkedLists-deletingnode.svg.png)

**image source** : [wikimedia](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/CPT-LinkedLists-deletingnode.svg/380px-CPT-LinkedLists-deletingnode.svg.png)

### Stack

Stack is a LIFO (Last In First Out) structure. A Stack is a list of elements where both insertion and deletion are allowed at only one end called Top.

	Operations : 
		push - insert new elements into the Stack
		pop - delete the top element from the Stack
		peek - returns the top element of stack.

![Stack](http://www.studytonight.com/data-structures/images/stack-data-structure.png)

**image source** : [studytonight](http://www.studytonight.com/data-structures/images/stack-data-structure.png)

A Stack is called **Overflow** when it is completely full, and is called **Underflow** when it is completely empty.

### Queue

Queue is a linear data structure, in which the first element is inserted from one end called REAR, and the deletion of exisiting element takes place from the other end called as FRONT. It is a FIFO (First In First Out) structure.

	Operations : 
		enqueue - insert new elements into the Queue
		dequeue - delete an existing element from the Queue

![Queue](http://www.studytonight.com/data-structures/images/introduction-to-queue.png)

**image source** : [studytonight](http://www.studytonight.com/data-structures/images/introduction-to-queue.png)


### Tree

A Tree is a non-linear data structure which organizes data in hierarchical (arranged in order of rank) structure. 

In tree data structure, every individual element is called as **Node**.

- The first node is the Root Node. 
- The remainging nodes forms subtree recursively. Every child node will form a subtree on its parent node.

![Tree](http://btechsmartclass.com/DS/images/Tree.png)

**image source** : [btechsmartclass](http://btechsmartclass.com/DS/images/Tree.png)


##### Terminology
 please check this [article](http://btechsmartclass.com/DS/U3_T1.html) to get a very good understanding about terminologies used in trees.
