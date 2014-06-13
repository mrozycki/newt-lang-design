Newt Programming Language Design - Functions
============================================

Main function
-------------

Main function is defined using an idiomatic `program` keyword, taking an
identifier that could be thrown away by an interpreter, but a compiler can
use it to generate an executable file name. There may be other uses to this
in later versions of the language.


Functions
---------

Additional named functions may be defined before the main function.
Such a function definition consists of function name, argument list, return
type and a block of code. Argument and return types may be any variable types
available, both primitive and compound, including the user defined ones.

The general structure of the definition looks like this:

    function name (type1 arg1, type2 arg2, ...) -> return_type {
      // code
    }

For example:

    function square (Integer n) -> Integer {
      return n*n;
    }

If a function doesn't return any values, the return type together with the
arrow token can be dropped, for example:

    function sayHello (String name) {
      console.writeln("Hello, ", name, "!");
    }

Empty argument list is represented by empty pair of parentheses, for example:

    function getRandomNumber () -> Integer {
       return 4; // chosen by fair dice roll.
                 // guaranteed to be random.
    }

### Why the bizzare function signature?
It can be read as "function X, taking those arguments and returning this type",
being easy to understand and remember. This is contrary to the usual C-style
syntax of `type name(arguments)`, that has no natural way to be read in the
order of declaration elements being written.

But then why not keep it consistent with variable declarations and have

    variable num : Integer;

    function square (n : Integer) : Integer {
      return n*n;
    }

This is an option still being considered. However, the only advantage of this
solution is keeping consistency between variable and function definitions, while
functions cannot be really treated as values, so there is no obligation to keep
them similar. 

The main disadvantage is that it makes definition with initialisation look
bizarre and the type annotation seem redundant, for example:

    variable num := 5 : Integer;

Since we already assigned an integer value to the variable, explicitly making
it an integer afterwards seems unnecessary. Compare: "variable called 'num'
with value 5, that is an integer" with "integer called 'num' with value 5".

Also it seem to be too far from the C way of doing things. As for the function
definition, it is a decision made mainly with code readability in mind. It is
not possible to have all three of 'internal consistency', 'consistency with C'
and 'readability', so often one of those has to be preferred, while sacrificing
the others.

This one is probably the most difficult decision made in the design of Newt,
but I strongly believe it is the right one. I am open to arguments on this one.


Parameter passing
-----------------

This was another difficult decision to make, as the popular C-style syntax
languages seem to be consistent with each other, but not internally consistent.
All of them have pass-by-value for primitives, but pass-by-reference for arrays
and objects.

Now, here's why pass-by-value for primitives and pass-by-reference for arrays
is a bad idea:

    function setToFive (Integer n) {
      n := 5;
    }

    function setFirstToFive (Integer[] ns) {
      ns[0] := 5
    }

    program MixedPass {
      Integer a := 0;
      setToFive(a);
      console.writeln(a);

      Integer as[] := {0, 0, 0};
      setToFive(as);
      console.writeln(as[0]);
    }

Knowing some programming, someone may expect to get zero and five, expecting
to have mixed parameter passing strategies. At the same time a beginner
programmer may expect either two zeroes or two fives. In the latter case,
being told the first one actually results with a zero, he will probably expect
a zero from the other one as well. Which is not how it works in most C-like
languages and may be confusing.

Both internally consistent solutions may cause confusion on transition to
a proper programming language. However, functions taking arrays as parameters
are less common in programs written by beginners, while if a function takes
any parameters, it is very likely that at least one of them will be a primitive
type value. Also, while some moder programming languages have pass-by-value
for arrays, none of them has pass-by-reference for primitives.

Thus a decision was made to have pass-by-value default for all types:
primitives, arrays and compound types. An obvious disadvantage is the memory
and time overhead needed to create a copy of each array and structure passed
as a parameter. Copy-on-write may be used to minimase the impact on functions,
that only read the array values.

The main advantage of that solution is that it doesn't require a full-blown
garbage collection or any memory management tool. Compound types and arrays may 
still be kept on the heap, while internally being stored as references on the
stack. However, we may simply deallocate all the values referenced from the 
current stack frame on function call return, as references cannot be returned.
Therefore there is no need for objects to outlive the stack frame.

This way there is also no need to introduce pointers and references, keeping
the language simpler. They may be included, however, in the later versions of
the language, together with optional call-by-reference for all types.


Variable number of arguments
----------------------------

`console.write[ln]`, as described in the IO section, takes a variable number
of arguments. I am still to come up with an elegant solution to solve this.
