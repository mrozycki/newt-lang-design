Newt Programming Language Design - Input/Output
===============================================

Printing text to the screen
---------------------------

You've had a gist of it in the 'Program structure' section, but let's now
discuss why it looks the way it does. Again, a few non-solutions first.

### Non-solution #1: Streams in C++

C++ has streams. They seem OK, they look simple to use, embedding variables
in the printed text is easy.

    cout << "Hello, " << name << "! Nice to meet you!" << endl;

It's also consistent with how you handle files:

    myFile << "Hello!" << endl;

But it's not consistent with anything else. The `<<` operator construct looks
like nothing else in the entire language (except for maybe the `>>` operator
construct). That's the main issue I have with it.

### Non-solution #2: `System.out` in Java

In Java you use the `System.out.print[ln]`. It's a bit long and may seem
intimidating at first to a beginner. Also what do you mean by `print`? Like,
to the printer (I kid you not, I was asked that more than once). Those aren't
the biggest issues, though. Embedding variable values is.

In Java, to achieve it, you have to either use multiple `print`s or use
string concatenation within one. The former is bad, because it requires typing
out a lot of stuff. The latter is even worse. Why? Observe:

    System.out.println("2+2="+2+2);

What does it print out? Not `2+2=4`, that's for sure.

Don't get me wrong, I really think operator overloading is great. And usually
I would argue, that if someone writes code like the above, he's just a bad
programmer. The thing is though, beginners **are** bad programmers. We're
trying to stop them from making mistakes like those.

### Newt's solution

Newt introduces two functions, similarly to Java: `console.write` and
`console.writeln`. It has syntax consistent with other function calls.
It uses the word `write` instead of `print`.

What about the variable embedding? Newt addresses this in two ways.

#### Printing out multiple values
Both `console.write` and `console.writeln` can take multiple values, so that
you can write:

    console.writeln("Hello, ", name, "! How are you?");

So that the 2+2 example looks like this:

    console.writeln("2+2=", 2+2);

Giving a clear hint, that those two are separate and they are to be evaluated
separately and then printed out in order.

#### Explicit casting to string
String concatenation can still be done with the `+` operator, but is not
overloaded for other types. This way, if you want to concatenate string with
an integer, you have to cast it explicitly. Example:

    console.writeln("2+2="+string(2+2))

Although this is not the recommended solution in this case, as it's longer
and has worse legibility than the other solution. However, if you want explicit
concatenation of string and other type, this is the way to do it.

#### Why `console`, though?
The `console` prefix may seem unnecessary, as standalone `write` and `writeln`
could do a good enough job as well. There are two main reasons to keep it this
way.

The first is avoiding pollution of the global namespace. The other one, far more
important, is to keep consistency with handling files. This is explained in
detail below.

The obvious disadvantage is that it introduces overhead and makes the initial
leap slightly bigger. However, it can be easily explained by analogy to English
imperative: "Console, write line".

As for the word `console` itself, other possibilities like 'screen' or 'system'
are still being considered. However, 'console' at this point seems the most
feasible, as it is also used in languages like C# or JavaScript.

Getting input from keyboard
---------------------------

Here we have 4 non-solutions.

### Non-solution #1: scanf from C

To read an integer using scanf, we write:

    int n;
    scanf("%d", &n);

I don't think I have to explain why this is bad for beginners. Except for the
`scanf` (but again: I don't have a scanner) and `n`, everything else is just
a stream of characters, meaningless to a beginner.

### Non-solution #2: raw input (e.g. Python, Java's Reader/InputStream)

In Python, we have to read in raw input as a string and then parse it. So to
get an integer from user, we do:

    n = int(input())

And for a single integer it's fine, quite easy to explain and understand (if
explained correctly). But if we'd like to read in a list of numbers, we need
to do it this way:

    n = [int(i) for i in input().split(" ")]

Which is clear and concise for more advanced programmers, but introduces too 
big of a gap for beginners. Also requires all the numbers to be in one line,
so the program is not very flexible in the format of the input (unlike C and
C++ are).

### Non-solution #3: C++ streams

It has basically the same pros and cons as `cout`. It's also flexible in the
format of the input (like `scanf`), but it also requires a call-by-reference
mechanism for primitive types.

### Non-solution #4: Java's DataInputStream

Here, to get an integer, we do:

    DataInputStream instream = new DataInputStream (System.in);
    int n = instream.readInt();

And it's almost OK. It's flexible in the format of the input. It doesn't
require a big leap from learning about variables, it doesn't require manual
parsing, it's easy to understand. However, it does have the overhead of
initialising a `DataInputStream` from `System.in`. Basically a magical
incantation, which a beginner has to memorise, because it's too early for him
to understand it fully.

### Newt's solution

This is basically what Java's `DataInputStream` is, but without the painful
initialisation of the stream. So to read in an integer, all you need to do
is write:

    Integer n := console.readInteger();

There's also functions like `readReal()`, `readBoolean()`, `readCharacter()`,
`readString()` and `readLine()`. For discussion on datatype names, as well as
the assignment operator, see the 'Variables' section.

Most of them are self explanatory, maybe except the difference between
`readString()` and `readLine()`. The latter reads in an entire line (so from
current pointer to the first newline character), while the former reads in a
'word' (from current pointer to the first whitespace character: space, tab or
newline. Similarly to how C and C++ handle reading strings).

Handling files
--------------

Writing to files and reading from them works almost the same as doing it on
the console. The only difference is that you need to open the file first and
then call the functions on your file handler instead of on `console`.

    File in := system.open("hello.txt", "w");
    in.writeln("Hello, world!");
    in.close();

So you first open a file (whether it should be `system.open` is still being
considered). You specify the name and access type (read, write, append, binary
or a combination of those) and you get a file handler, which can be used just
like the `console`. At the end, of course, you need to close the file.
