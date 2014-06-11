Newt Programming Language Design - Introduction
================

Newt is an imperative programming language with a C-like syntax meant for
teaching programming. Currently being at the design phase of development. So it 
won't be out for a while.

Table of contents
-----------------
0. Introduction
  0. [General idea](https://github.com/mrozycki/newt-lang-design#general-idea)
  0. [Features](https://github.com/mrozycki/newt-lang-design#features)
  0. [Roadmap](https://github.com/mrozycki/newt-lang-design#roadmap)
  0. [Questions](https://github.com/mrozycki/newt-lang-design#questions)
0. Program structure
0. Input/output
0. Variables, arrays
0. Mathematical operations
0. Functions
0. Compound types (structures)
0. Graphics
0. [Example code]((https://github.com/mrozycki/newt-lang-design/examples/queue.newt)

General idea
------------

Nowadays the popular programming languages are constantly being extended with
features that are difficult to understand for beginners. This makes a steeper
learning curve, as many of those advanced features affect the most basic
mechanics.

The idea is to design a language, that doesn't have those advanced features,
so that it can be consistent with itself and at the same time easy to
understand and therefore learn.

A programming language designed solely for the purpose of teaching makes more
sense today than ever. No good programmer knows only one programming language,
choice of the first one to learn becomes more and more arbitrary. At the same
time, the last widely known language designed with learning in mind was Pascal,
now obsolete. There is also Scratch, which, however good, was designed with
younger user base in mind and may not as easily gain attention from teenagers
or university students.

Features
--------

### Simple to understand, C-like syntax
Keeping the widely used syntax for variables, conditionals and loops, to ensure
an easy transition to languages like C, Java or PHP. At the same time dropping 
the `public static void main(String[] args)` or `using namespace std`, so there 
is fewer unnecessary things to understand/memorise on the early stages of 
learning programming.

### Verbose and redundant syntax
This may seem like an unwanted characteristic for a programming language,
but it may be desired for learning. It's difficult to get something wrong twice
in the exact same way and in the exactly two places that are connected.
Having a redundant syntax makes hard-to-find mistakes (like a semi-colon after
an if statement) syntax errors, so that they are easier to spot and avoid.

### Simplified mechanics
So that you don't have to bother with variable value limits, four different
types of floating point values, how to properly test string equality,
which way does the assignment go etc.

### Consistent syntax and mechanics
So you don't have to explain/understand more than one new idea at a time.
No more questions, that can only be answered "you don't know the language
well enough to understand it".

### Easy to use dedicated IDE
So you don't have to spend an hour trying to configure the tools and get bored
a few times before you can actually start coding. (At least I'm planning on
creating one)

### Simple graphics/sound libraries built into the language
You can quickly start coding fun stuff, without any additional complicated
installation and configuration. So that you or your students don't get bored
implementing Euclid's algorithm for the tenth time.

Roadmap
-------

Please remember that I'm an undergraduate student and at the moment I am
developing this project alone in my free time. I will be trying my best to
deliver a working implementation as soon as possible. Even at the cost of
delaying some of the goal mechanics to be implemented in the second version
of the language.

### Design
Carefully decide on all the mechanics and syntax. Make note of the features
that would be nice to have, but are not necessary in the first incarnation
of the language. Take all the feedback and adjust the design.

This should take several weeks and end with freezing the design for the first
version of Newt.

### Implement the compiler
I have literally no idea how long this will take.

### Complete the language documentation and write tutorials
This may be done in parallel to implementing the compiler, as at this point
the design should be frozen.

### Write a simple IDE
By 'simple' I mean text editor with syntax highlighting plus a compile button.

### Further development of the IDE and compiler
This would include optimising the compiler and the generated code, possibly
rewriting it in Newt, adding features to the IDE (autoindentation, syntax
autocomplete) and bugfixes in both.

### Start working on the second version of the language
Concurrently to further development of the first version. Possibly thinking
of some more sophisticated development cycle for the project.

Questions
---------

### Why is it called Newt?
Original idea was to call the language Newton/m^2 (you know, because Pascal),
but I decided this name is too long. So I shortened it to Newt, because it
also seems like a nice name.

### Why not do X instead of Y?
This repository is supposed to answer all the questions of this type. If your
particular quesiton is not answered anywhere or you believe I made a wrong call
making a certain decision, please do let me know. Any constructive feedback is
more than welcome. However, please bear in mind, that "language Z does it this
way" is usually not a good argument.

### X would give you better performance. Why not use it?
Generating optimal code is not the main priority. Newt is meant to be used
for teaching, so programs written in it will probably not be very complex.
Introducing a difficult to understand mechanic to gain a performance boost
(probably even unnoticeable for a beginner) is not a good idea. 

However, if your idea fits the general philosophy of the language **and** gives
a performance boost, please share! On the other hand, please also bear in mind
that delivering a working compiler has a higher priority than performance of
generated code, so your idea (even if it's good and I agree) may not be included
in the first version of the language.

### Why not just use Python?
If your goal language is Python, learn Python. If your goal are C-like
languages, transition from Python may be long and difficult. On the other hand
starting with a language like C++, Java or PHP may be intimidating and 
discouraging, while also requiring you to learn all the peculiarities of the
chosen language, that does not show in any other language.
