Coursera course notes

# weeek 1

Paragims: imperative, functional, logic. OOP.

There is no mutation in math. Mutation is a key part of imperative programming.

Let's avoid mutation.

Tech talk: more parrallel computation. Functional programming is much better of it, then imperative. In imperative case even simple parallel programming can be tricky.

We can define variable, functions. 

Evalutaion and substitution. We can do it unless we won't have side-effects.

c++ - example with side effect. We should store additional variable here.

call-by-name and call-by-value evalutaion approaches. Call-by-name helps because it evaluates arguments only once. call-by-value helps when some arguments weren't used. In different cases different approach can be optimal.

if c-b-v terminates, then c-b-n evaluation also terminates. But not vise versa.

Scala by default uses c-b-v evalutation. If argument type starts with =>, then it's c-b-n. def func(x: Int, y: => Int) = ...

There are &&, ||, ! operators. you can write def abs(x: Int) = if (x >= 0) x else -x. You can evaluate if-else statements: evalutate condition, then select appropriate value.

Function parameters can be passed by name or by value. The same works for defenitions. val x = 2, val y = ... evaluates at the point of defenition. val x = ... - define value right now, def x = ... - define value when needed.

newton method for sqrt: X - argument, G - guess, g = (g + x/g) / 2 and iterate like this. 

You can define functions inside other functions (scoping). 

';' is optional in Scala. Multiline: put operator at previous line, braces. ';' needed for several statements at the one line.

For big doubles distance between two consequtive numbers can be quite big.

Defenitions from outer blocks are visible unless the are shadowed.

gcd recursion example, factorial recursion example. 

If a function calls itself at its last action, the stack frame can be reused, it's called tail recursion.

Tail recursion is iterative process. If the last action is calling a function (maybe different, maybe the same), stack frame can be reused. It called tail-calls. 

gcd is tail recursion. Scala optimizes direct recursive calls. @tailrec annotation. If the implementation isn't tail recursion, then it will trigger an error.

vanila factorial isn't tail recursion, but it can be tail recursion with a helper function: helper(number, accumulated).

# week 2

TBD
