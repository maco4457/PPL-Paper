https://courses.washington.edu/b572/public/beamer2.pdf 
http://www.shallowsky.com/linux/LinuxPresentations.html
http://web.mit.edu/rsi/www/pdfs/beamer-tutorial.pdf

#0. Differences in type checking in two dynamic scripting languages#
Matt Comerford, Travis Pence, Kelly Kaoudis

#1. Advantages of Python
  - "batteries included."
  - Indentations requirement leads to clean readable code.
  - Gradual learning curve.
  - Ducktyping without the downside of ambiguity.
  - Extension Friendly

#2. Advantages of Lua
- very, very compact, **< 100 KB** (excluding standard libraries)
- easy to learn due to its small size
- an "embedding" language (as opposed to an "extension-friendly" language like Python)
- simplistic, close-to-English syntax
- only one dynamic associative data type, the table

#3. Similarities?#
- Started as scripting languages
- Dynamic and strongly typed languages
- Open-source, including commercial use (MIT license)

#4. Language origins#
Lua:
- Brazil had strong trade barriers, making it extremely difficult to buy customized software from abroad
- Created in 1993 by Roberto Lerusalimschy, Luiz Henrique de Figueiredo, and Waldemar Celes
- members of the Computer Graphics Technology Group (Tecgraf) at the Pontifical Catholic University of Rio de Janeiro, Brazil

Python:
- Implementation of the language was started in 1989 by Guido van Rossum at CWI in the Netherlands
- Designed as a successor to the ABC language capable of exception handling and interfacing with the Amoeba operating system

#5.Tiobe rank#
- Python: No. 8
- Lua: No. 20

#6. Lua's core design principles (Lua.org): #
- Keep the language simple and small.
- Keep the implementation simple, small, fast, portable, and free.

#7. Excerpts from the Zen of Python (PEP 20): #
- Beautiful is better than ugly.
- Explicit is better than implicit.
- Complex is better than complicated.
- Readability counts.
	
#8. Strong typing#
Language prevents successful execution of an operation on arguments that have differing types
- Pro: Explicit statements of intent 
- Con: Limits how "creative" one can be in using a given data type

#9. Weak typing#
Language allows implicit conversions (casts) on types when different types are present in an operation,
without necessarily throwing errors
- Pro: Less verbose, allows for shorter development time
- Con: Can be more obscure, harder to read

#10. Dynamic type checking#
Types are checked during runtime
- Pro: Save you from writing a few "extra" lines of code
- Con: If a variable is mispelled, it will not throw an error

#11. Static type checking#
Types are checked at compile/interpretation time
- Pro: Catch errors early on in development
- Con: Have to spend more time writing code

#12. Duck typing#
"If it walks like a duck, talks like a duck..." 
A duck-typed language is dynamic and does its type checking at runtime.

#13.

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

#14. String/number coercion in Lua#
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

#15. Python doesn't have automatic coercion, so is *more* strongly typed.
    >>> 1 + 1
    Output: 2
    >>> "1" + "1"
    Output: "11"
    >>> "1" + 1
    Output: TypeError: Can't convert 'int' object to str implicitly
    >>> “Hello” + 1
    Output: TypeError: Can't convert 'int' object to str implicitly

#16. Lua's metatables#
Metatables can be associated with a table or other value. One of their uses is "operator overloading" 
(via metamethods), defining certain normally disallowed 
operations like dividing a table by another table, or computing the union of two tables.

#17. Metatables vs Python's casting#
Say we have a value **j** in both Python and Lua.
In Python, we cast **j** to the appropriate type instead of 
setting a value in **j**'s metatable that allows us to perform the operation we want, like division, on **j**.

__"explicit is better than implicit."__  

    >>> "1" + str(1)
    Output = "11"
    
#18. Manual type checking#
In Lua, often it is more proactive to write and call a manual type-checking script from your program than to wait until
runtime. This is not necessary in Python.

#19. Conclusion#
- These languages share some of the basic characteristics (scripting, dynamic and strongly typed)
- Python is definitely the workhorse of the two languages, where Lua is all about keeping it simple
- While they may seem quite similar though, there are very key differences in their implementations that make them unique to the communities they serve


#Any Questions? 
