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

##for our purposes, the language did not need type declarations.
    Instead, we could use the language itself to write type-checking routines, 
    provided that the language offered basic reflexive facilities (such as run-time type information)
    Lua.org

##Only uses coercion between strings and numbers(not nearly as strongly typed as Python)
    “string-numeric coercion is not an exception to strong type checking in Lua, it can still be classified as strongly 
    typed” http://the4thwiki.com/lua/types.html

    "Lua is a dynamically typed language. This means that values have types but variables don't, 
    so there are no type or variable declarations. Internally, each value has a tag that identifies its type; 
    the tag can be queried at run time with the built-in function type. Variables are typeless and can hold values 
    of any type. Lua's garbage collection keeps track of which values are being used, discarding those that are not."
    Lua documentation
    
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






