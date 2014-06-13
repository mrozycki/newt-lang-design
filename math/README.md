Newt Programming Language Design - Operations on values
=======================================================

This section defines the mathematical, bitwise, logical and relational
operations included in the language, together with their operators, their
associativity and precedence. Nothing surprising here.


Mathematical operations
-----------------------

Newt includes basic mathematical operations, like addition, subtraction,
multiplication and division (including modulo division) with usual operators
for those, respectively: `+`, `-`, `*`, `/`, `%`. All of them are
left-associative (i.e. `1+2+3` means `(1+2)+3`) with `*`, `/` and `%`
having precedence over `+` and `-`, with parentheses being used to change
the evaluation order.

As for the typing, type of `Real Op Real` is `Real`, `Integer Op Integer`
is `Integer`, `Real Op Integer` and `Integer Op Real` is `Real`. Modulo
division is not defined for `Real`s.


Logical and relational operations
---------------------------------

Logical operations and, or and negation is included with the usual operators 
`&&`, `||` and `!`, respectively. Negation takes precedence before conjuction,
which in order takes precedence before disjunction.

Relational operations like equal, not equal, less than, greater than, less than
or equal and greater than or equal are included as well, with the usual
operators `==`, `!=`, `<`, `>`, `<=` and `>=` respectively. They are all
left-associative.

Logical operations use short circuiting. That is, given `expr1 && expr2`,
`expr1` is evaluated first and if it evaluates to `false`, the entire
expression returns `false` without evaluating the second expression. Similarly
if in `expr1 || expr2`, `expr1` evaluates to `true`, `expr2` is not evaluated
and the entire expression evaluates to `true`.


Still to be decided
-------------------

Should bitwise operations: and, or, xor, negation and left/right shifts, be
included in the language? If so, should they only be defined for `Integer`
type, or `Character` and `Real` as well?
