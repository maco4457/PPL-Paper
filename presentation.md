#1. Differences in type checking in two dynamic scripting languages#
Matt Comerford, Travis Pence, Kelly Kaoudis

#2. Main points#

#3. Language origins#

#4.Tiobe rank#
- Python: No. 8
- Lua: No. 20
	
#5. Strong typing#
Language prevents successful execution of an operation on arguments that have differing types

#6. Weak typing#
Language allows implicit conversions (casts) on types when different types are present in an operation,
without necessarily throwing errors

#7. Dynamic type checking#
Types are checked during runtime

#8. Static type checking#
Types are checked at compile/interpretation time

#9. Duck typing#
"If it walks like a duck, talks like a duck..." 
A duck-typed language is dynamic and does its type checking at runtime.

#10.

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


#11. Lua's core design principles (Lua.org): #
- Keep the language simple and small.
- Keep the implementation simple, small, fast, portable, and free.

#12. Excerpts from the Zen of Python (PEP 20): #
- Beautiful is better than ugly.
- Explicit is better than implicit.
- Complex is better than complicated.
- Readability counts.

#Slide 8#

#Slide 9#

#Slide 10#

#Slide 11#

#Slide 12#

#Slide 13#

#Slide 14#

#Slide 15#

#Slide 16#

#Slide 17#

#Slide 18#

#Slide 19#

#Any Questions? 
