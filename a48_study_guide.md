# CSCA48 Study Guide

> Once you understand C and all its glory, you will learn to hate on Python.

If you are using Windows, I highly suggest using a Linux Virtual Machine like 
Ubuntu or dual booting Ubuntu and Windows (if you are willing to make your 
relationship with the world of tech more permanent :) ).

## Section 0: Basic Data Types



## Section 1: Pointers

Any programming language at its very heart is about storing and moving information
around. In fact, to your computer, there is no difference between an `int` or `char`
or even `char*` etc., they are simply a sequence of bits that are passed around in your
machine. It is the human component and only this component that makes the decision 
that an `int` expresseses our idea of quantity or number and `char` expresses our idea
of characters. If you were to "ask" your computer what is stored at a particular memory
address, the response will always be "I don't know. Who cares?". The first byte 
at this location could be interpreted as a `char` or the first 4 or 8 bytes at 
the same location (depending on your machine) could be interpreted as an `int`, `char*` 
or any other data type. The point being, **memory isn't specifically "formatted" to store your requested data type**. 
An `int` is stored in the same way as a `char`,`char*`, `double` etc. - a sequence of bytes. 
A data type simply defines how many bytes we should read starting from a location.

Pointers in C are like any other datatype. When declaring a pointer, your computer simply
allocates 8 bytes in memory to store a sequence of 8 bytes. It is us who decided to
first interpret these 8 bytes as a number then as a memory address.

Whenever you pass in a variable to a function in C, it is always copied. If its
an `int`, the bytes of size `sizeof(int)` are copied. If its a `char*` the bytes
of size `sizeof(char*)` are copied. These copied values exist as local variables
inside your function, specifically parameters, and go out of scope when the function
returns. The same logic is true for returning a value from a function, the value is copied
and sent back to the caller.

Passing in a pointer into a function has **absolutely no difference**, the value the pointer
holds (i.e the 8 bytes that store the memory address) are copied and stored as a local variable in the function (i.e your parameter). Failure to distinguish the above ideas about copy on pass and copy on return leads to main source of confusion about pointers. People tend to think
that pointers are passed to function in a special way - **they are not**. They are done in the
exact same way an `int` or `char` etc. would be passed in.




## Section 2: Linked Lists