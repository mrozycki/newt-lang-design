Newt Programming Language Design - Program structure
====================================================

I've once heard someone say "Programming languages are not optimised for
writing 'Hello, world!'". And that's true, they're not. Moreover, usually they
even shouldn't be, because why waste your time on something like this.

However, if you're learning programming, "Hello, world!" is the first program
you will ever see. So it's important to make a good first impression,
especially on a person that has never programmed before.

Non-solution #1: Java
---------------------

Imagine you don't know how to program, so you go to a Java class and the first
thing the teacher shows you is this:

    public class HelloWorld {
      public static void main (String[] args) {
        System.out.println("Hello, world!");
      }
    }

What does `public` mean? What's a `class`? `void`? `main`? Oh, `main`'s easy,
it's because this is the main function of the program. Function?

I guarantee you, half of the class at this point lost all their interest.
From the rest, half of them will get it wrong the first time they type it in
(because to them it's just a stream of characters, that mean nothing specific).
Some of them will take half an hour to finally get it right. Same applies to C#.

Non-solution #2: C++
--------------------

Now let's have a look at another non-solution, C++:

    #include <iostream>
    using namespace std;

    int main()
    {
      cout << "Hello, world!" << endl;
      return 0;
    }

This is a bit better. At no point you get a meaningless stream of words. Still,
though, why do we include anything? Why is there a hash sign at the beginning
of this one line? Oh, it's because it's a preprocessor directive. Pre... pro...
what? And the `using namespace`? Just copy it already, would you?

Then we get to the `cout`. I'd dare say, for the beginners, this is the single
most error-prone line in the history of programming. `count` instead of `cout`,
getting the arrows the wrong way, putting a space between the angle brackets,
writing a number of brackets other than 2, one instead of l at the end of `endl`,
no semi-colon. I swear, I don't know a single person that typed it in right the 
first time they tried (copying doesn't count).

Almost a solution: D
--------------------

Let's have a look at how D does it:

    import std.stdio;

    void main() {
      writeln("Hello, world!");
    }

This is better. We're getting somewhere. The import line is quite simple,
could be even explained and understood, `void main` still seems a bit like
magic, but at least it's only two words. Still, I believe we could do better.

We're almost there: Pascal
--------------------------

Now let's have a look at this one:

    Program HelloWorld;
    Begin
      WriteLn('Hello, world!');
    End.

It looks like it was designed for teaching! Maybe because it actually was,
since it's Pascal. Here how this code works, line by line: first we say this
is HelloWorld program. Here it begins, here it writes line "Hello, world!",
here it ends. Et voila! Press F5 to compile and run and see for yourself.

Newt's solution
---------------

This is how it looks in Newt:

    program HelloWorld {
      console.write("Hello, world!");
    }

It's basically a copy of Pascal's solution, with C-like syntax. Not entirely,
as you'll see with function declarations, but at this point it's almost the
same piece of code. No `import`s of `include`s, the student should not worry
about it at this point. No magic words that have no meaning. One may say that
`console` could be dropped as well (as requires understanding what the console
is). This is discussed in the IO section of the design.
