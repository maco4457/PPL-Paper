Principles of Programing Languages Lightning Talk
------------------------------------------------

Kelly Kaoudis
Matt Comerford
Travis Pence

===============================================

#1. Introduction#

- point
  - sub point
	- sub point
	
#2. Strong vs. weak typing#
- Strongly typed: language prevents successful execution of an operation on arguments that have differing types
- Weakly typed: language allows implicit conversions (casts) on types when different types are present in an operation,
without necessarily throwing errors


#3. Dynamic vs static#
- Dynamically typed: types are checked during runtime
- Statically  typed: types are checked at compile/interpretation time

#4. Duck typing#
"If it walks like a duck, talks like a duck..." 
A duck-typed language is dynamic and does its type checking at runtime.

#5.

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


#6. Lua's core design principles (Lua.org): #
- Keep the language simple and small.
- Keep the implementation simple, small, fast, portable, and free.

#7. Excerpts from the Zen of Python (PEP 20): #
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
