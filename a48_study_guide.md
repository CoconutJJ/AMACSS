# CSCA48 Study Guide

<!--
    I would like to keep this study guide interesting to read, so the students
    actually enjoy reading it...
-->
> Once you understand C and all its glory, you won't like going back to Python.


## Section 0: Basic Data Types





## Section 1: Pointers

<!--
    I would like to provide a overview of how data is stored and moved around
    in the computer. Although feels like it isn't a review anymore, but I'm
    writing this to someone who's new to the material
-->

Any programming language at its very heart is about storing and moving
information around. In fact, to your computer, there is no difference between an
`int` or `char` or even `char*` etc., they are simply a sequence of bits that
are passed around in your machine. 

<!-- Sounds a little philosophical...-->
It is the human component and only this component that makes the decision that
an `int` expresseses our idea of quantity or number and `char` expresses our    
idea of characters. If you were to "ask" your computer what is stored at a
particular memory address, the response will always be "I don't know. Who
cares?". The first byte at this location could be interpreted as a `char` or the
first 4 or 8 bytes at the same location (depending on your machine) could be
interpreted as an `int`, `char*` or any other data type. 

<!-- 
    Feels like I'm trying to introduce a new concept... probably shouldn't
    be doing that. But I also want to be clear just how
-->
The point being, **memory isn't specifically "formatted" to store your requested
data type**. An `int` is stored in the same way as a `char`,`char*`, `double`
etc. - a sequence of bytes. A data type simply defines how many bytes we should
read starting from a location.


<!--
    The previous paragraphs is the attempt to the set the stage for this idea 
    below
-->
Pointers in C are like any other datatype. When declaring a pointer, your
computer simply allocates 8 bytes in memory to store a sequence of 8 bytes. It
is us who decided to first interpret these 8 bytes as a number then as a memory
address.

Whenever you pass in a variable to a function in C, it is always copied. If its
an `int`, the bytes of size `sizeof(int)` are copied. If its a `char*` the bytes
of size `sizeof(char*)` are copied. These copied values exist as local variables
inside your function, specifically parameters, and go out of scope when the
function returns. The same logic is true for returning a value from a function,
the value is copied and sent back to the caller.

Passing in a pointer into a function has **absolutely no difference**, the value
the pointer holds (i.e the 8 bytes that store the memory address) are copied and
stored as a local variable in the function (i.e your parameter). Failure to
distinguish the above ideas about copy on pass and copy on return leads to main
source of confusion about pointers. People tend to think that pointers are
passed to function in a special way - **they are not**. They are done in the
exact same way an `int` or `char` etc. would be passed in.

## Section 2: Linked Lists

You will use linked lists a lot during your upper year courses. It is a very 
fundamental data structure and mastery in manipulating linked lists is vital.

A linked list comes with some basic operations as you have seen in lecture.
While even a lackluster CS student could see how linked lists could be created
in Python with a class containing a `next` property. The pointers in C actually
give us a whole new level of control. The ability of being able to create a
pointer and dereference it somewhere later in your code is a very powerful tool.

Let's review some of the basic operations:


Let's first define our Node `struct` 
```c
typedef struct __node__ Node; // don't worry about this, this is called
                              // prototyping. It's so we can use the
                              // typedef keyword `Node` in our Node struct
                              // before we've actually defined it.

typedef struct __node__ {
    int v;
    Node * next 
} Node;
```

### `INSERT(head,k)`
Note the double pointer to head allows us to change the head node pointer by
dereferencing.
```c
/**
 * Inserts the Node k into the beginning linked list head.
 */ 
void insert (Node** head, Node* k) { 

    if (!head) return;
    k->next = *head;
    *head = k;
}

/**
 * Inserts the Node k into the end of linked list head.
 */
void insert (Node** head, Node* k) {

    if (!head) return;

    Node * curr = *head;

    // if this is the first node in the list, overwrite head.
    if (!curr) *head = k; return;

    // find last node in list
    while (curr->next != NULL) curr = curr->next;
    // set the next to our new node.
    curr->next = k;
}   
```

### `DELETE(head,v)` 
Delete is slightly more complicated as we have to consider the edge cases where
the node is the head of the list and the end of the list
```c
/**
 * Deletes Node with value v from linked list head
 * Returns 0 if node with value v is not found, 1 otherwise
 */
int delete (Node** head, int v) {
    
    if (!head) return 0;
    
    Node * curr = *head;
    Node * prev = NULL;
    
    // look for the node with value v.
    while (curr->v != v) { 
        // keep track of previous node, we will need it later
        prev = curr;
        curr = curr->next;
        // if we reach end of list prematurely, just return
        if (!curr) return 0; 
    }

    // it helps to consider the exit condition of this loop
    // exit condition: negation of while loop condition
    // -> curr->v == v
    // this means the loop will exit with curr->v == v

    if (!prev) { // if the node we want to delete is the head node.
        
        *head = curr->next; // overwrite the head node pointer to the next one.

    } else { // otherwise it occurs at the end of the list or the middle
        
        // if it's in the middle, this sets the previous node pointer
        // to the one after curr (curr being the one we want to delete).
        // if it's at the end, curr->next == NULL, hence still correct
        // as the prev node will now have prev->next = NULL. 
        // (i.e the new end  of the list)
        prev->next = curr->next; 
    }
    // free up the memory for curr (the deleted node)
    free(curr)
    return 1;
}
```

---
Questions, Comments and Suggestions can be directed to me at
[david.yue@mail.utoronto.ca](mailto:david.yue@mail.utoronto.ca)