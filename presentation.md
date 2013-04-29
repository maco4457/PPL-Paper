#1. Differences in type checking in two dynamic scripting languages#
Matt Comerford, Travis Pence, Kelly Kaoudis

#2. Main points#

#3. Language origins#

#4.Tiobe rank#
- Python: No. 8
- Lua: No. 20

#5. Lua's core design principles (Lua.org): #
- Keep the language simple and small.
- Keep the implementation simple, small, fast, portable, and free.

#6. Excerpts from the Zen of Python (PEP 20): #
- Beautiful is better than ugly.
- Explicit is better than implicit.
- Complex is better than complicated.
- Readability counts.
	
#7. Strong typing#
Language prevents successful execution of an operation on arguments that have differing types

#8. Weak typing#
Language allows implicit conversions (casts) on types when different types are present in an operation,
without necessarily throwing errors

#9. Dynamic type checking#
Types are checked during runtime

#10. Static type checking#
Types are checked at compile/interpretation time

#11. Duck typing#
"If it walks like a duck, talks like a duck..." 
A duck-typed language is dynamic and does its type checking at runtime.

#12.

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

#13. String/number coercion in Lua#
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

#14. Python doesn't have automatic coercion, so is *more* strongly typed.
    >>> 1 + 1
    Output: 2
    >>> "1" + "1"
    Output: "11"
    >>> "1" + 1
    Output: TypeError: Can't convert 'int' object to str implicitly
    >>> “Hello” + 1
    Output: TypeError: Can't convert 'int' object to str implicitly

#15. Lua's metatables#
Metatables can be associated with a table or other value. One of their uses is "operator overloading" 
(via metamethods), defining certain normally disallowed 
operations like dividing a table by another table, or computing the union of two tables.

#16. Metatables vs Python's casting#
Say we have a value j in both Python and Lua.
In Python, we cast our data element j to the appropriate type instead of 
setting a value in j's metatable that allows us to perform the operation we want, like division, on j.

__"explicit is better than implicit."__  

    >>> "1" + str(1)
    Output = "11"
    
#Slide 16#

#Slide 17#

#Slide 18#

#Slide 19#

#Any Questions? 
