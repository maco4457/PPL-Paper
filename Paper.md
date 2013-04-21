The evolution of type-checking and definition in Python and Lua 
======
##How two scripting languages that are dynamically and strongly typed evolved to meet different needs specified by the community 

Introduction
------------------------
###dynamic typing and strong typing (what they mean, ex?, etc.)

>differentiate between strong/weak& dynamic/static (different qualifier sets for kinds of typing)
>background on str/weak & sy/stat. : http://en.wikipedia.org/wiki/Type_system#Type_checking

>strong/weak http://en.wikipedia.org/wiki/Strong_and_weak_typing

>Both Lua and Python are considered strongly-typed languages
>similar in the beginning (both started as scripting languages), evolved differently

Python
-----------------------


Lua
-----------------------

##original design decisions: 
keep the language simple and small;
keep the implementation simple, small, fast, portable, and free
http://www.lua.org/history.html

##"For our purposes, the language did not need type declarations.
Instead, we could use the language itself to write type-checking routines, 
provided that the language offered basic reflexive facilities, such as run-time type information."
Lua.org

Lua originally borrowed from Sol, a TeX-like description language designed for creating reports, and from Modula,
which (at least according to Wikipedia) was basically a Pascal fork. One of its first uses was for describing graphics
metafiles.

##Types in Lua
Initially, Lua had seven types: 
- numbers (implemented as floats), 
- strings, 
- (associative) tables,
- nil (a type with a unique value also called nil),
- userdata (a generic C pointer to represent C structures inside Lua), 
- Lua functions, and 
- C functions

"After eight years ... the only change in Lua types was the unification of Lua functions and C functions into a single function
type. To keep the language small, we did not [initially] include a boolean type. Like in Lisp, nil represents false, and any other value
represents true. This is one of the few economies that we sometimes regret today." Lua.org

##table?!
"A table is a collection of key and data pairs, where the data is referenced by key." Programming in Lua, 2nd ed.
Tables are the *only* built-in composite data type in Lua, so user-created types generally build upon tables.

Similar to Python's dictionary, PHP's associative array, Scala's map

Constructing a table looks like constructing a dict in Python: 
sweetNewTable = {} -- Creates a new, empty table
We pass tables by ref, can insert/delete values and indices (mutability), 

Now, Lua has eight types, but still no integer type!
The eight primitive types of Lua are now:
- nil, 
- boolean, 
- number, 
- string, 
- function, 
- userdata, 
- thread, and 
- (associative) table. 

"Python has many more primitive types, but implicit type conversions sometimes make the variations hidden or irrelevant. 
Consider that while Lua uses (without special build configuration) double-precision floating point for all numbers, 
Python has four numeric types: int, float, long, and complex. Does Lua need an integer type? Does Python?" the 4th wiki

"Lua allows simple arithmetic on numbers using the usual operators to add, subtract, multiply and divide," (Lua Types Tutorial)
but all 'numbers' are floats.

"Lua is a dynamically typed language. This means that **values have types but variables don't**."
Thus, there are no type/variable declarations, similar to Python; this is all inferred at runtime by the interpreter.
"Internally, each value has a tag that identifies its type; the tag can be queried at runtime with the built-in function type.
Variables are typeless and can hold values of any type." Lua documentation
The garbage collector keeps track of what values are in play at any given time and discards/deallocates those which aren't.


Lua *only* uses coercion between strings and numbers, and therefore is not nearly as strongly typed as Python.
The form of type checking that some consider to best describe both Lua and Python is **duck typing**:

"If it walks, like a duck, talks like a duck..."

A duck-typed language is dynamic and does its type checking at runtime.

In Python, ‘+’ performs arithmetic and also string concatenation.

Lua has a unique string concatenation operator, ‘..’ 

"This means that in Lua there is no type ambiguity to be checked for when performing addition and concatenation 
between numbers and strings."  http://the4thwiki.com/lua/types.html

“String-numeric coercion is not an exception to strong type checking in Lua, it can still be classified as strongly 
typed.” 
    
##“In a dynamically typed language, every variable name is (unless it is null) bound only to an object.
Names are bound to objects at execution time by means of assignment statements, 
and it is possible to bind a name to objects of different types during the execution of the program.” 
http://the4thwiki.com/lua/types.html

Conclusion
-----------------------

>Finish off with some main similarities and differences that make these languages comparable?

Any other ideas?




Python 
    
    >>> 1 + 1
    Output: 2
    
    >>> "1" + "1"
    Output: "11"
    
    >>> "1" + 1
    Output: TypeError: Can't convert 'int' object to str implicitly
    
    >>> “Hello” + 1
    Output: TypeError: Can't convert 'int' object to str implicitly
Lua

    > = 1 + 1
    2
    
    > = “1” + “1”
    2
    
    > = “1” + 1
    2
    
    > = 1 .. 1
    11
    
    > = “1” .. “1”
    11
    
    >= “1” .. 1
    11
    
    >= "Hello" + 1
    attempt to perform arithmetic on a string value






