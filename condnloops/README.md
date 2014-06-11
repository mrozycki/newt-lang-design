Newt Programming Language Design - Introduction
===============================================

Conditional statements
----------------------

The conditional `if` statement looks the same in every C-like language,
so there is almost nothing clever about it in Newt. It looks like this:

    if (condition) {
      // code
    }

Although, one thing is that only a braced block of code is allowed after
an `if` statement, therefore this:

    if (condition) do_something();

Is illegal. This serves two purposes. First of all, it makes typo like this:

    if (condition);
    {
      do_something();
    }

to be a syntax error. (If you don't know what's wrong with this code, notice
the semicolon after the `if` statement)

Then, this code:

    if (condition) do_something(); do_something_else();

which probably was intended to be:

    if (condition) {
      do_something();
      do_something_else();
    }

is also a syntax error. Thus making for easier finding of such bugs.

`if..else` statements are also a part of the language. After an `else` keyword
only a braced block or another `if` statement is allowed. Therefore this is
allowed:

    if (condition) {
      do_something();
    } else if (another_condition) {
      do_something_else();
    } else {
      break;
    }

But this is not:

    if (condition) {
      do_something();
    } else break;

`switch` statements will probably not be included in the language, as they
lead to writing very messy code and are not really necessary.

Loops: `while` and `do..while`
------------------------------

Again, nothing special about those two constructs. They take forms:

    while (condition) { 
      // code
    }

    do {
      // code
    } while (condition)

Just like with `if` statements, only a braced block is allowed as code to be
repeatedly executed, for exactly the same reasons as before.

Loops: `for`
------------

Again, nothing different from the C++/Java way of doing it:

    for (initialisation; condition; step) {
      // code
    }

Again, only a braced block of code is allowed.

As for the Java collections `for`:

    for (Item i: items) {
      // code
    }

It is still being considered whether it should be included in the language,
and even if, in what form. However, it is rather improbable that it will be
present in the first version of Newt, if at all.

Loops: `repeat` or `forever`
----------------------------

A `repeat` loop, that takes a number of iterations as an argument and repeats
some block of code that number of times is being considered. One of the uses
could be a `repeat () {}` construction, meaning "repeat forever", which is
cleaner than `while (true)` and more legible than the `for (;;)` idiom.

On the other hand, there doesn't seem to be any other uses for it, so another
idea would be to include a `forever` loop, which takes no parameters and repeats
the code until `break` is encountered.
