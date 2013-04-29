Type-checking and definition in Python and Lua 
======
##How two scripting languages that are dynamically and strongly typed evolved to meet different needs

*Introduction*
------------------------

A scripting language is a programming language that supports the writing of *scripts*. These *scripts* are programs
written with the intention of automating the execution of certain tasks. The idea behind this is to remove the need
for a human operator to perform the execution one-by-one. Because of this characteristic, scripting languages have 
become an essential tool to the field of Computer Science, as a way to greatly increase the speed and reliability of 
task execution. 

Python and Lua two languages that are commonly embedded into applications to provide scripting support. An interesting
aspect of these languages, however, is that they shared very distinct characteristics to one another when they were
first introduced. Yet, through the steady evolution of these two languages, which has come mainly due to the
differing needs of each langauge's user base, Python and Lua have continued to grow and become different from one
another, while still maintaining basic similarities that they have shared since their inception.

####Type Checking

An important similarity between the Lua and Python languages deals with each language's *type checking* 
procedures. *Type checking* is the process of verifying and enforcing the constraints of types, and can occur at two
stages of a program's implementation.

######Static vs. Dynamic Typing

Static typing, which occurs at compile time, allows for errors to be caught early during the implementation phase,
and verifies that the conditions of type information will hold true for *every* possible execution of a the program.
This eliminates the need to repeat the type checking procedure every time a program is run, and while this can make 
program execution more effecient and thus faster, it also means static type checkers are much more convservative. This
can lead to a static checker that will reject programs that would otherwise execute correctly at run time. 

Both Python and Lua, however, fall into the second category: dynamic typing. Dynamic typing is issued at the run time
the program. in dynamic type checkers, values are assigned types, but variables are not. In other words, a variable can
refer to a value of any type. Dynamic typing also improves the support for dynamic programming language features, such
as generating types and functionality based on actual run time data. Dynamic typing also offers fewer *a priori* 
guarantees, meaning it will accept and executes programs that would be rejected by static type checkers, due to the
static checker's nature of being very conservative. 

######Strongly vs. Weakly Typed Languages

Both languages also share what is known as a *strongly typed* system. *Strongly typed* means a programming language will
prevent the successful execution of an operation on arguments that have differing types. This holds the main advantage 
over *weakly typed* systems, in which the programming language will implicitly convert, or cast, types when different
types are present in an operation, which can lead to ambiguity or an incorrect operation being executed. 

    (1) var x := 5;    // 'x' is an integer here, by default
    (2) var y := "37"; // 'y' is a string here
    (3) x + y;         // what will this yield?

To answer the question "what will this yield?", we must first look how the language is typed. In a strongly typed 
language, the program will be prevented from evaluating 'x + y' because the two types, int and string, are not the same.
However, in a weakly typed language, one of two things could come from evaluating 'x + y':
- 'y' will be converted from 'string' to 'int': x + y = 5 + 37 = 42
- 'x' will be converted from 'int' to 'string' and a concatenation will occur: x + y = "5" + "37" = "537"

This characteristic of a weakly typed language can make it very difficult to be positive about whether or not a program
will generate the correct output, as the user will be unsure of the correctness until after the code has executed during
run time. However, in the strongly typed systems found in Lua and Python, the code will throw an error during 
compilation, and the user will be able to address the problem, whether an error or simple abiguity, much earlier than
he/she would be able to if using a weakly typed system. 

While these two languages had similar beginnings and still share important characteristics with one another, both have
taken different paths of evolution that allow them to best satisfy the needs of their user bases. In the following 
sections, we will expand on Python and Lua, and further discuss the subtle differences that allowed these languages, 
which both started as strongly typed scripting languages, to evolve into the languages they are today.


*Python*
-----------------------

## Types in Python


One of the core concepts behind python is that "everything is python is an object." (diveintopython.net)  First it is necessary to define how  python defines an object.  In certain langauges, an object must have attributes and methods; however in python, a much looser definition is followed. This allows for objects (in python) to have neither methods nor attributes, or even to not have to capacity to be subclassable.  The primitive data types, such as string  or int , are really just objects themselves. Which means the numbers such as 42 are objects! Furthermore, there is an int object sitting next to the number 42 in memory. In fact, all instances of an integer object have their __class__ attribute pointing to the int object.

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


>Easier to ask for forgiveness than permission. This common Python coding style assumes the existence of valid keys or attributes and catches exceptions if the assumption proves false. This clean and fast style is characterized by the presence of many try and exceptm statements. The technique contrasts with the LBYL style common to many other >languages such as C.

>Look before you leap. This coding style explicitly tests for pre-conditions before making calls or lookups. This style contrasts with the EAFP approach and is characterized by the presence of many if statements.
>In a multi-threaded environment, the LBYL approach can risk introducing a race condition between “the looking” and “the leaping”. For example, the code, if key in mapping: return mapping[key] can fail if another thread removes key from mapping after the test, but before the lookup. This issue can be solved with locks or by using the EAFP approach.


*Lua*
--------------------------

######Lua design decisions:
- Keep the language simple and small.
- Keep the implementation simple, small, fast, portable, and free.
*http://www.lua.org/history.html*

######Compared to excerpts from the Zen of Python:
- Beautiful is better than ugly.
- Explicit is better than implicit.
- Complex is better than complicated.
- Readability counts.
*PEP 20 (The Zen of Python)*

######Lua may be considered:
- strongly typed
- dynamically typed
- duck typed, by Prof. Chang's definitions in the course notes.

On the typing spectrum, Lua is less strongly typed than Python, definitely dynamic (most incarnations of Javascripty are static, for comparison), and allows fewer implicit conversions than C. There are a few exceptions to this, such as string/number coercion, which I'll cover later, but in general, the rules of Lua are pretty definite about which types do and do not mix and match. We cannot add a Boolean and a thread, for example, or try to concatenate a function and a string.

######types in Lua, (in case you're unfamiliar with the language):
Initially, Lua had seven types:
- numbers (implemented as floats),
- strings,
- (associative, dynamic) tables,
- nil (a type with a unique value also called nil),
- userdata (a generic C pointer to represent C structures inside Lua),
- Lua functions, and
- C functions

"After eight years ... the only change in Lua types was the unification of Lua functions and C functions into a single function type." Lua.org

Now, Lua has eight types (but still no integer type!):
- nil,
- boolean,
- number,
- string,
- function,
- userdata,
- thread, and
- (associative, dynamic) table.

"To keep the language small, we did not [initially] include a boolean type. Like in Lisp, nil represents false, and any other value represents true. This is one of the few economies that we sometimes regret today." Lua.org

The programmer doesn't declare types. Lua doesn't require the x: String or j: Boolean stuff like in Scala, or even bool j like C. j = true creates and assigns, similarly to Python.

"Python has many more primitive types, but implicit type conversions sometimes make the variations hidden or irrelevant. Consider that while Lua uses (without special build configuration) double-precision floating point for all numbers, Python has four numeric types: int, float, long, and complex." the 4th wiki

######A brief description of strong typing
Here we take "strong typing" to mean that implicit conversions/coercions are generally not okay but also that type checking is performed at some point, and is fairly strict. We'll use "dynamic" or "static" as more a specifier of when exactly that type checking happens.

"In dynamically typed languages, type checking happens while evaluating the program (statically typed languages are type-checked before evaluation)." CSCI 3155 lecture notes

######Dynamic typing in Lua
"Lua is a dynamically typed language: values have explicit types but variables don't," (Lua documentation) so, similarly to Python, no type or variable declarations by the programmer are generally necessary for values.

The interpreter looks up type tags at runtime. This means if you write code that is never called for some reason, it should never be type checked.

"Internally, each value has a tag that identifies its type... Variables are typeless and can hold values of any type. Lua's garbage collection keeps track of which values are being used, discarding those that are not."

All this means that the interpreter/compiler has, in general, one less thing on its list to do each time you check if your code will compile (which is especially important for interpreted languages, which often compile slowly). However, this also means that if the programmer wishes to avoid strange runtime errors, a lot of the burden of type checking falls on his or her shoulders.

“In a dynamically typed language, every variable name is (unless it is null) bound only to an object. Names are bound to objects at execution time by means of assignment statements, and it is possible to bind a name to objects of different types during the execution of the program.” http://the4thwiki.com/lua/types.html

Lua DOES perform run-time type checking on its built-in operations, but:

unlike in more well-typed languages (by well-typed I mean the types are programmer-specified everywhere), no built-in mechanism in Lua for type checking the parameters and return values of function calls exists. The types are left unspecified, as seen below.

Lua:
    function factorial(n)
      if n == 0 then
         return 1
      else
         return n * factorial(n - 1)
      end
    end

Python:
    def factorial(n)
     if n == 0:
        return 1
     else:
        return n * factorial(n - 1)
        
Emulating a more static form of type-checking via user code is often done in Lua as part of the testing process. Something which might be considered both a disadvantage and an advantage of dynamic typing in Lua is that type checking must be done by the programmer. (Some ways to do this are with asserts or function decorators, as seen in the below example.)

"For our [original] purposes, the language did not need type declarations. Instead, we could use the language itself to write type-checking routines, provided that the language offers basic reflexive facilities, such as run-time type information." Lua.org

    is_typecheck = true

    function typecheck(...)
     return function(f)
       return function(...)
        assert(false, "TODO: ADD SOME GENERIC TYPE CHECK CODE HERE")
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
    
"The advantage is that the type information is outside of the function implementation. We can disable all the type checking by switching a single variable, and no added overhead would remain when the functions are executed (though there is some slight added overhead when the functions are built). This typecheck function could also store away the type info for later introspection," Lua.org type checking tutorial

Another solution to the lack of pre-evaluation type checking is the (optional to add) checks library.

"[The checks library] offers a terse, flexible and readable way to produce good error messages. Types are described by strings, which can of course be Lua type names, but can also be stored in an object's metatable, under the __type field. Additional, arbitrary type-checking functions can also be registered in a dedicated checkers table," Lua types documentation

A distinct advantage to Python is that this sort of type-checking by hand is generally not useful or necessary, in my experience with the language. However, a novice might find it a useful exercise to perform Lua-style type checking if he or she is unsure of what will run in Python.

######Why check types at all, especially if we want to get rid of them?
We only really need to check our code during writing and implementation for correct typing, rather than each time we interpret/compile. Anything typing-related is removable once the code is thoroughly tested, leading to a smaller footprint. This is useful for a module or script, which may be repeatedly compiled as part of other things.

We can take the functional paradigm that "code is data" literally here. All our code takes up space, and the less memory used by our code, the faster the code runs. While just removing type declarations from the source might not sound like a lot of improvement, consider how often you have to declare the types of everything in C, C++, or even Scala.

“Python has the ability to reduce errors though somewhat more static type checking [and stronger typing]. Lua programs are sometimes more error prone, due to automatic coercion, accessing of unset variables without an exception, and having to check most functions for nil values, rather than just catching the exceptions. There may be some advantages to some of these points however. IMO the only decent way of solving this is static analysis. Most of my catastrophic globals typos have been in less-used codepaths, and even had -w survived, they would have blown up on people at the worst times." JayCarlson, http://lua-users.org/wiki/LuaVersusPython

######aside: table?!
"A table is generally a collection of key and data pairs, where the data is referenced by key." Programming in Lua, 2nd ed.

Tables are the only built-in composite data type in Lua, so user-created types generally build upon tables. Though it is similar to Python's dictionary, PHP's associative array, Scala's map, a table can also be used as an array, or as a kludge of a dictionary and an array, including both key-value pairs and lone values. I'm going to briefly cover them in case you're unfamiliar.

Constructing a table looks something like constructing a dict in Python.

    table = {} -- Creates a new, empty table called, imaginatively enough, table

We pass tables by ref, can insert/delete values and indices (mutability),

    table.insert(table, position, value) --append
    table.remove(table,position)  --delete
    
can iterate over the contents using the ipairs() functionz (one of Lua's few built-ins),

    for index,value in ipairs(t) do
       print(index,value) 
    end

and can build new data types on top of tables using key-value referencing.

######Why tables are important to the way types are defined in Lua:

"Every value in Lua can have a metatable. This metatable is an ordinary Lua table that defines the behavior of the original value under certain special operations. You can change several aspects of the behavior of operations over a value by setting specific fields in its metatable. For instance, when a non-numeric value is the operand of an addition, Lua checks for a function in the field "__add" in its metatable. If it finds one, Lua calls this function to perform the addition." Lua.org

Value metatables can be used to enable or disable coercion between types in order to perform operations on two things that are initially of different types, though the language's default behaviour is mainly what I cover here.

######Duck typing
 The form of type checking that some consider to best describe both Lua and Python is **duck typing**:

"If it walks like a duck, talks like a duck..." A duck-typed language is dynamic and does its type checking at runtime.

######Coercion

Lua, by default, only uses coercion between strings and numbers, and therefore is not nearly as strongly typed as Python.

In Python, ‘+’ performs arithmetic and also string concatenation.

Lua has a specific string concatenation operator '..'. If we use it on a number, that number becomes a string.

    > = 100 + "7"
    107
    > = "1000" + 234
    1234
    > = "hello" + 234
    stdin:1: attempt to perform arithmetic on a string value
    stack traceback:
    stdin:1: in main chunk
    [C]: ?
    > = 234 + "1000"
    1234

"You can see that where a string can be converted to number, the calculation succeeds. The string "hello" cannot be converted to a number and so an error occurs. In statically typed languages (e.g. C) this would cause an error as you cannot assign a value to a variable of an incompatible type. This works in Lua because it is dynamically typed." Lua-users.org wiki

    > message = "hello " + who
    stdin:1: attempt to perform arithmetic on a string value
    stack traceback:
    stdin:1: in main chunk
		[C]: ?
        
The '+' operator doesn't concatenate strings in Lua.

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

In Python, concatenation-via-coercion between strings and its number types is not allowed. Though both languages are strongly typed, the number-to-string coercion in Lua makes it somewhat less so.

    >>> 1 + 1
    Output: 2
    >>> "1" + "1"
    Output: "11"
    >>> "1" + 1
    Output: TypeError: Can't convert 'int' object to str implicitly
    >>> “Hello” + 1
    Output: TypeError: Can't convert 'int' object to str implicitly
	
"In Lua there is no type ambiguity to be checked for when performing addition and concatenation between numbers and strings." http://the4thwiki.com/lua/types.html

“Yet: we consider string-numeric coercion not as an exception to strong type checking in Lua, it can still be classified as strongly typed.” the 4th wiki

This is true because every other type in Lua, while not programmer-specified, is distinct.



*Conclusion*
-----------------------

Python and Lua, while being very similar in their respective beginnings, have evolved to feed the needs of the 
communities that these languages support.

Python can easily be considered the work horse between the two langauges. Overall, it comes better equipped. An extremely
large amount of libraries with very useful functionality means Python is exceptional for offline work as well as tool
scripting. It's ability to perform highly and quickly with numerical computations, as well as built-in binary operators
(and, or, xor...), makes Python highly advantageous when working with embedded systems. Also, Python is whitespace sensitive,
and while this may seem like a hassle in the beginning, this characteristic leads to a somewhat universal standardization
of how any Python code will look, increasing its overall readability across different code bases. Finally, Python is 
extremely user (and more so "beginner") friendly in the available documentation, providing multiple resources, where Lua
lacks much of the introductory material.

Lua, on the other hand, is known mostly for being an extremely effective language while amazingly being able to keep
its simplicity intact. Lua packs a punch in under 100kb of space (excluding standard libraries), compared to Pythons 
824kb for Python's python22.dil package, all while maintaining a minimal amount of memory usage. Lua started as a 
configuration language, making it an ideal language for game design and implementation. Finally, Lua is well-known for
its support of multi-threading. This gives it the *huge* advantage of being suitable for embedding into mult-threaded
programs and systems right from the beginning, without the need of additional libraries or packages.

It's clear that Python and Lua started off as very similar scripting languages, and still do share similar basic
characteristics with each other. It can't be said whether or not one of these languages is better, but it's easy to see 
how each of them has evolved to the different languages they are today. Whether or not the language is built for power
or simplicity, they have both been built and rebuilt to satisfy the changing needs of their users. 
