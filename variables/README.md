Newt Programming Language Design - Variables
============================================

Types
-----

The language is statically typed.

The general idea is to have 4 primitive types: `Integer`, `Real`, `Boolean`,
`Character`, along with compund types like `String`, `File`, `Sprite` (for
graphics) etc., as well as user-defined types (discussed in another section).

`Integer` would be an unbounded, unsigned integer type (basically a bignum).
This is so that the student doesn't have to worry about value boundaries.
From my experience, the immediate response to "this number will not fit in an
int" is changing it to a float (double if they remembered that float is not to 
be used), instead of expected change to long (or long long in case of C++).

`Real` would be a double precision floating point type or a pair of unbounded
integers for the mantissa and exponent. The former is currently more feasible,
as it is easier to implement and also is good enough for most of the uses and
would actually allow to learn how imprecise floating point computation is.
Real type literals can be given in the form of `1.2`, `.01` or `1e10`. 
Form `1.` is not valid, as it is obsolete and often included in languages only
for historical reasons. 

`Boolean` is self-explanatory. Boolean values are written `true` and `false`.

`Character` is still being under consideration. The two options are: one byte
using ASCII or two-byte Unicode character (as in Java). The reason for the
former is compatibility with C/C++, while rationale behind the latter may be
"it's 2014, for God's sake!".

Character literals are written with single quotes, like in C++, e.g. `'a'`.

`String` is just an array of characters with `+` operator overloaded for
concatenation and `<`, `==`, `>` etc. for lexicographical comparison of strings.
String literals are written with double quotes, e.g. `"Hello!"`.

Other built-in compound types are explained in their corresponding sections.

### Why `Real`?
Because there is no good way to call a floating point type. Let me explain:
0. `Float` will cause students to use `float` in Java, C/C++ etc. when they
make the transition.
0. `Double`. Double what? Double precision. Compared to what? Good luck
explaining that.
0. `Number`. Isn't integer a number as well? JavaScript solves it by getting
rid of integer data type and leaving `Number` to do everything.
0. `Rational`. Brings a fractional representation to mind. Also `Rational pi`
looks ridiculous.
0. `Decimal`. It was a close one. It does bring fixed-point to mind, but that's
not a big enough issue. The only reason `Real` was chosen instead is that it
is actually used by some programming languages (D, for example. Or Pascal).

Thus leaving us with `real`.

### Why not `int`, `real`, `bool` and `char`?
It is still a viable option and may be used in the final version.

### Why not `int`, `real`, `boolean` and `char` (like in Java)?
Because having `boolean` as the only one not shortened makes me cringe.

### But `real` is not shortened either.
How do you make `real` shorten so that it still makes sense?

Definition, initialisation and assignment
--------------------------------------

C-style declarations are kept. So that definition of an integer looks like this:

    Integer n;

Initialisation can only be made as definition+assignment. C-like `int n(10);` or
the C++11 `int n{10};` will not be implemented, as they are unnecessary
complications to be introduced to a teaching programming language, especially
that they are not really present in any programming language other than C/C++.

The assignment operator itself is not finally decided yet, but the most feasible
option right now seems to be the Pascal `:=` operator. Why change the `=`?
Because it may be surprisingly confusing to new programmers, as they may
intuitively see it as a symmetrical operator. I've seen that a few times and it
is usually very difficult to explain that it is in fact not the case that `5=a`
is not the same as `a=5`, as the belief that the familiar `=` operator is
symmetrical is, if present, really strong.

Another option is a `<-` operator for assignments. Obvious advantage is that
it clearly shows the direction of assignment (which is not the case with `:=`,
which is not that intuitive and only indicates lack of symmetry). Its downside
is that it is not remotely similar in appereance to the widely used `=`
operator, which may make the transition more problematic.

Thus, for now, an assignment looks like this:

    n := 10;

And an initialisation looks like this:

    Integer n := 10;

Compound assignment operators like `+=`, `-=` etc. and increment/decrement
operators will probably not be introduced, as they are a complication
unnecessary for a beginner and would double the time spent on implementing
mathematical operations. However, as they are present in all the C-style syntax
languages, a student will learn them at some point anyway and thus they may be
introduced in later versions of the language.

Constants
---------

Constants will be created by using a `Constant` modifier at initialisation.
Like so:

    Constant Real pi = 3.14159;

The keyword `constant` may be changed to `const` if the type names are changed
to `int` etc.

Pointers and references
-----------------------

Pointers and references will probably not be introduced in the first version
of the language, as with the call-by-value for every type (primitive or
compound) they seem unnecessary. They may be introduced later with optional
call-by-reference. Call-by-value vs call-by-reference is discussed in the
'Functions' section.


Arrays
------

Arrays are constant size, however the size doesn't have to be known at compile
time. The C-style array definitions are kept. The square brackets operator to
access a given field of an array is also used. Examples:

    Integer nums[10];

    Integer n := console.readInteger();
    Integer tab[n];
    tab[0] := 0;

Array literals are given with curly braces, as in C, like so:

    {1, 2, 3}

Allowing for initialisations:

    Integer nums[3] = {1, 2, 3};
    Integer digits[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};

And even constant arrays:

    Constant Integer numbers[] = {4, 8, 15, 16, 23, 42};
