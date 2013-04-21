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

*Python*
-----------------------

## Types in Python


One of the core concepts behind python is that "everything is python is an object." (diveintopython.net)  First it is necessary to define how  python defines an object.  In certain langauges, an object must have attributes and methods; however in python, a much looser definition is followed. This allows for objects (in python) to have neither methods nor attributes, or even to not have to capacity to be subclassable.  The primitive data types, such as string  or int , are really just objects themselve. Which means the numbers such as 42 are objects! Furthermore, there is an int object sitting next to the number 42 in memory. In fact, all instances of an integer object have their __class__ attribute pointing to the int object.

Python comes with two primitive objects, <type 'object'> and <type 'type'>
 
    >>> object 
    <type 'object'>
    >>> type 
    <type 'type'> 
    >>> type(object) 
    <type 'type'>
    >>> object.__class__ 
    <type 'type'>
    >>> object.__bases__ 
    ()
    >>> type.__class__ 
    <type 'type'>
    >>> type.__bases__ 
    (<type 'object'>,)


"These two objects are primitive objects in Python. We might as well have introduced them one at a time but that would lead to the chicken and egg problem - which to introduce first? These two objects are interdependent - they cannot stand on their own since they are defined in terms of each other." 

![src of image is cafepy.com](http://www.cafepy.com/article/python_types_and_objects/images/types_map.png)


##Duck Typing


    try:
      mallard.quack()
    except (AttributeError, TypeError):
      print("mallard can't quack()")


_EAFP:_

    try:
      x = my_dict["key"]
    except KeyError:
      # handle missing key
_LBYL:_

    if "key" in my_dict:
      x = my_dict["key"]
    else:
      # handle missing key

In the _LBYL_ example, it requires the key value to be looked up twice, once to ensure that it exists and the second to retrieve the pair value. 

"A try/except block is extremely efficient if no exceptions are raised." (docs.python.org)


    Easier to ask for forgiveness than permission. This common Python coding style assumes the existence of valid keys or attributes and catches exceptions if the assumption proves false. This clean and fast style is characterized by the presence of many try and exceptm statements. The technique contrasts with the LBYL style common to many other languages such as C.

    Look before you leap. This coding style explicitly tests for pre-conditions before making calls or lookups. This style contrasts with the EAFP approach and is characterized by the presence of many if statements.
    In a multi-threaded environment, the LBYL approach can risk introducing a race condition between “the looking” and “the leaping”. For example, the code, if key in mapping: return mapping[key] can fail if another thread removes key from mapping after the test, but before the lookup. This issue can be solved with locks or by using the EAFP approach.




*Lua*
-----------------------

##original design decisions: 
keep the language simple and small;
keep the implementation simple, small, fast, portable, and free
http://www.lua.org/history.html

##"For our purposes, the language did not need type declarations.
Instead, we could use the language itself to write type-checking routines, 
provided that the language offered basic reflexive facilities, such as run-time type information."
Lua.org

Lua originally borrowed from Sol, a TeX-like description language designed for creating reports, and from Modula, a
Pascal fork. It was designed as a description language for graphics metafiles, and is most commonly used layered as a C or C++ API today.
It's especially popular for game programming and other graphical uses, ut generally performs best when used as a functional scripting API.
World of Warcraft uses it for interface customization. A Linux utility called Conky uses it to display changing information like system data, the weather, and upload/download speeds directly on the desktop. It was even included
as part of the FLAME/Skywiper/Wiper malware as scripting support for already compiled C++ modules. 

It's currently listed as #20 in overall popularity online by the Tiobe index. Though as in Python whole programs can be written in Lua and
there is support for object-oriented and empirical programming, it's very conducive to a functional scripting style. This is due to elements
like its general lack of user-specified types, its simplicity, and its lightweight core.

##intro to types in Lua
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

"Lua is a dynamically typed language: **values have explicit types** but variables don't," (Lua documentation) 
so, similarly to Python, no type or variable declarations by the programmer are generally necessary. The interpreter looks up type tags at runtime. 
"Internally, each value has a tag that identifies its type... Variables are typeless and can hold values 
of any type. Lua's garbage collection keeps track of which values are being used, discarding those that are not."

- Lua performs run-time type checking on its built-in operations
- unlike in languages like C, there is no built-in mechanism in Lua for type checking the parameters and return values
of function calls. The types are left unspecified.

    function abs(x)
     return x >= 0 and x or -x
    end

"In dynamically typed languages, type checking happens while evaluating the program (statically typed languages are type-checked
before evaluation)." CSCI 3155 lecture notes

Sometimes, this means that type checking must be done by the programmer. (Some ways to do this are with asserts or function decorators,
as seen in the below example.) This allows us to check our code during writing and implementation for correct typing, but all type information
can then be removed at runtime, leading to a smaller overall footprint. Going back to the functional paradigm that "code is data,"
we can take this literally. All our code takes up space, and the less memory used by our code, overall we can run a faster program.
While just removing type declarations from the source might not sound like a lot of improvement, consider how often you have to 
declare the types of everything in C, C++, or even Scala.

    is_typecheck = true

    function typecheck(...)
     return function(f)
       return function(...)
        assert(false, "FIX-TODO: ADD SOME GENERIC TYPE CHECK CODE HERE")
        return f(...)
      end
     end
    end

    function notypecheck()
     return function(f) return f end
    end

    typecheck = is_typecheck and typecheck or notypecheck

    sum = typecheck("number", "number", "->", "number")(
     function(a,b)
        return a + b
     end
    )
    
"The advantage is that the type information is outside of the function implementation. 
We can disable all the type checking by switching a single variable, and no added overhead would remain when the functions
are executed (though there is some slight added overhead when the functions are built). The typecheck function 
could also store away the type info for later introspection," Lua.org type checking tutorial

##Duck typing and coercion

Lua *only* uses coercion between strings and numbers, and therefore is not nearly as strongly typed as Python.
The form of type checking that some consider to best describe both Lua and Python is **duck typing**:

"If it walks like a duck, talks like a duck..."

A duck-typed language is dynamic and does its type checking at runtime.

In Python, ‘+’ performs arithmetic and also string concatenation.

Lua has a (string) concatenation operator '..'. If we use it on a number, that number becomes a string.
(Below, we attempt to perform arithmetic on a string value in the Lua, and as expected it fails.)

    > message = "hello " + who
        stdin:1: attempt to perform arithmetic on a string value
        stack traceback:
            stdin:1: in main chunk
            [C]: ?

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
    
However, in Python, concatenation between strings and numbers is not allowed. Though both languages are strongly typed,
here we can see that the number-to-string coercion in Lua makes it less so.
    
    >>> 1 + 1
    Output: 2
    
    >>> "1" + "1"
    Output: "11"
    
    >>> "1" + 1
    Output: TypeError: Can't convert 'int' object to str implicitly
    
    >>> “Hello” + 1
    Output: TypeError: Can't convert 'int' object to str implicitly
    

"In Lua there is no type ambiguity to be checked for when performing addition and concatenation 
between numbers and strings."  http://the4thwiki.com/lua/types.html

“Yet: string-numeric coercion is not an exception to strong type checking in Lua, it can still be classified as strongly 
typed.” 
    
##“In a dynamically typed language, every variable name is (unless it is null) bound only to an object.
Names are bound to objects at execution time by means of assignment statements, 
and it is possible to bind a name to objects of different types during the execution of the program.” 
http://the4thwiki.com/lua/types.html

##table?!
"A table is generally a collection of key and data pairs, where the data is referenced by key." Programming in Lua, 2nd ed. 
Tables are the only built-in composite data type in Lua, so user-created types generally build upon tables. Though it is similar to Python's dictionary, PHP's associative array, Scala's map, a table can also be used as an array,
or as a kludge of a disctionary and an array, including both key-value pairs and lone values. 

Constructing a table looks like constructing a dict in Python: 
    sweetNewTable = {} -- Creates a new, empty table 
We pass tables by ref, 
can insert/delete values and indices (mutability), 
    table.insert(table, position, value) --append
    table.remove(table,position)  --delete
can iterate over the contents using the ipairs() function,
    > for index,value in ipairs(t) do print(index,value) end
can build new data types on top of tables using key-value referencing

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






