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

##Original design decisions: 
keep the language simple and small;
keep the implementation simple, small, fast, portable, and free.
http://www.lua.org/history.html

Lua is extensible by other things, instead of supporting multitudes of libraries and inbuilt functions. The language originally borrowed from Sol, 
a TeX-like description language designed for creating reports, and from Modula, a Pascal derivative which never gained widespread popularity. 
One of its first uses was for describing graphics metafiles, but now it's used most commonly as a 
C/C++ extension, and is especially popular for game programming. World of Warcraft uses it for interface customization. 
A Linux utility called Conky employs it to display changing information such as upload/download speeds, the weather outside, etc. on 
one's desktop by writing to the root buffer. It's even been used as part of a series of malware targeting Middle Eastern governmental installations, 
layered with compiled C++ modules.

##" For our purposes, the language did not need type declarations.
Instead, we could use the language itself to write type-checking routines, 
provided that the language offered basic reflexive facilities, such as run-time type information."
Lua.org

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
Tables are the *only* built-in composite data type in Lua. Therefore, basically everything in Lua relies on tables. 
- Tables can be used similarly to Python's dictionary, PHP's associative array, Scala's map... but also can function as an array; 
can be used for memoization of functions, can use a table like a string (where each character is one key, or one value, or...)
-  "Lua does not differentiate between arrays and dictionaries. All Lua tables are actually dictionaries. 
In an array the keys are just number object keys." Lua Tables Tutorial
- A table can contain a mixture of things: key, value pairs and array-like values
- "[Use] ordinary Lua tables (which are fully accessible from both C and Lua) as the foundation for your new data types." Egor Skriptunoff, Stackoverflow
        Constructing your own data type would just mean setting up a table and linking it to whatever you want it to be.
        Say you are creating a 3D structure and want a Cartesian coordinate Point type. So you create a table linking Point
        to a tuple of (number, number).
- We pass tables by ref, can insert/delete values and indices (mutability) but can also create read-only tables 

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
The garbage collector keeps track of what values are in play at any given time and discards/deallocates those which aren't, 
similar to in Python.

##Duck typing and coercion
Lua *only* uses coercion between strings and numbers, and therefore is not nearly as strongly typed as Python.
The form of type checking that some consider to best describe both Lua and Python is **duck typing**:

"If it walks, like a duck, talks like a duck..."

A duck-typed language is dynamic and does its type checking at runtime. However, Lua does this differently than Python.

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






