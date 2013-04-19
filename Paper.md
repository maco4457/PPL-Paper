Differences between Python and Lua 
======
(Both Strongly-Typed, Dynamic Programming Langauges!)
------

Outline:

Introduction

Introduce dynamic typing and strong typing (what they mean, ex?, etc.)

differentiate between strong/weak& dynamic/static (different qualifier sets for kinds of typing)

background on str/weak & sy/stat. : http://en.wikipedia.org/wiki/Type_system#Type_checking

strong/weak http://en.wikipedia.org/wiki/Strong_and_weak_typing

Both Lua and Python are considered strong-typed language

similar in the beginning (both started as scripting languages), evolved differently

Python 

Lua

Only uses coercion between strings and numbers(not nearly as strongly typed as Python)

“string-numeric coercion is not an exception to strong type checking in Lua, it can still be classified as strongly typed” http://the4thwiki.com/lua/types.html

Conclusion?

Finish off with some main similarities and differences that make these languages comparable?

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






