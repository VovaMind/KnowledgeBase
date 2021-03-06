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

functions in functional languages is a first-class values, functions can be passed as a parameter and returned as a value

Higher order functions take other functions as a parameters or return functions

example: def sum(f: Int => Int, lowerBound: Int, upperBound: Int): Int = ...

Type A=>B means a function which takes argument of type A and returns type B.

We can use anonymous functions in order not to polute namespace and in order to avoiding a big amount of small functions. 

Anonymous functions is a kind of literals. Examples: (x: Int) => x * x, (x: Int, y: Int) => x + y. Type of parameters can be omitted if compiler can understand it by the context.

Anonymous functions is a syntactic sugar: you can replace them with {def f = ... f}.

We can modify sum function like: sum(f: Int => Int): (Int, Int) => Int = ...

And then we can use it like sumInts = sum(x=>x)

sum(cube)(1,10) -> we get sum of cubes functions and then we apply it to interval (1,10).

We can define such functions without nested functions, just using smth like sum(f)(a+1, b).

We can rewrite multiple argument functions like def f(arg_1)...(arg_n-1) = (arg_n => E). Or def f = (arg_1 => (arg_2 => ... (arg_n => E)...)). This is called *currying*.

Functional languages associate to the right, Int => Int => Int <=> Int => (Int => Int).

println - debug output.

define a class in scala:

class Rational(x: Int, y: Int) {
  
  def numer = x
  
  def denom = y
  
}

now we can do new Rational(1,2). we can define makeString(r: Rational) = ... . Or other methods like addRational(r: Rational, s: Rational): Rational = ...

Btw, we can omit types for args/return values if they are clear from the context.

we can define methods inside class. def add(other: Rational) = ... . 

we can define toString: override def toString = ...

we can define "private val g = gcd(...)" and then use it to reduce rational, and we can also have private functions. We can use def or val for the class fields.

we can use word this to get access to the fields. often we can omit it.

There are: require(condition, "message") and assert(condition). require is for parameters precondition, assert is for run-time checks.

You can define constructors like: def this(params) = this(...) or smth else.

We can evaluate expression with classes: substitute class parameters, substiture function parameters, substitute self-reference. 

You can use Infix notations, like r.add(s) => r add s. You can override standard operators like + or - etc. There are operations priority which is similar to the most of the languages. 

In scala you can have crazy operator names, but it's better not to use it. Maybe in some very specific contexts.

## week 3

abstract class CLASS_NAME { ... }  It can contain members which are not defined. We can't create it by new operator.

Example of abstract IntegerSet, and EmptySet implementation for empty sets. NonEmptySet also implements abstaction.

override def toString = ...

IntergerSet is a superclass, EmptySet and NonEmptySet are subclasses. Direct and indirect superclasses called base classes.

With no superclass Object is used (from Java).

override just a help for compiler, it doesn't do anything by itself. override is optional for abstaction implementetion, but if smth was defined in a superclass, than we must use override.

we can use "object X extends Y" instead of "class X ...". This leads us to a singleton (only one instance). 

```
object Hello {
  def main(args: Array[String]) = println("Hello")
}
```

We can start it from the command line ("scala hello").

Scala uses dynamic binging (dispatch), calling method depends on the run-time type.

Dynamic dispatch is analogous to call high-order functions. 

Code organised in packages. package X.Y.Z - at the program start. We can write import as:

*  import package.ClassNameA
*  import package.{ClassNameA, ClassNameB}
*  import package._ (wildcard import)

By default included:

*  Members of *scala* package.
*  Members of *java.lang* package.
*  All members of the singleton *scala.Predef*.

Int <- scala.Int, Object <- java.lang.Object, require (also assert) <- scala.Predef.require

scala-lang.org/, /api/current.

In scala we can have only 1 superclass. But it can contain several *traits*. Trait == abstact class, like:

```
trait Planar {
  def height: Int
  def width: Int
  def area = height *  width
}
```

Classes (objects) can inherit from at most 1 class, but from many traits. Like: class Square extends Shape with Planar with Movable ...

Traits are similar to interfaces, but they are more powerfull, because they can contain fields and concrete methods.

From the other hand traits can't contain (value) parameters, only classes can.

Scala class hierarchy: scala.Any is the basic one, than scala.AnyValue (scala.Double, scala.Int ... - are subclasses). scala.AnyRef (scala.ScalaObject, java.lang.String, scala.iterable, scala.Seq, scala.List). scala.Null can be used for all references. scala.Nothing can be used for everything else.

How Nothing is useful? It signals about bad termination or it can be element type of an empty collection.

throw Exc - exceptions are similar to java. throw new Error("...")

if (true) 1 else false - type estimation is AnyVal.

We can generalize type definitions by using params:

trait List\[T\]

class Nil\[T\] extends List\[T\]

Type param is written in square brackets, like \[TYPE\].

NoSuchElementException

def singleton\[T\](elem: T) = new Cons\[T\](elem, new Nil\[T\])

Than we can write singleton\[Int\](1), you can also write signleton(1), because it understanable from the context.

Type params don't affect evaluation in Scala. This is called **type erasure**. It's true for Java, Scala, Haskell etc. But it doesn't true for C++, C# etc.

Polymorhphism can work as:

*  the function can be applied to arguments of many types. Generics, instances of classes/functions are created by type parameterization.
*  the type can have instances of many types. Instances of a subclass can be passed to a base class.

IndexOutOFBoundsException

## week 4

Scala is based on objects. In theory, we can build everything from scratch using only objects.

Functions are objects with apply method:

'''
trait Function[A, B] {
  def apply(x: A): B
}
'''

object List and define "def apply(x1: T, x2:T)", and then we can do List(a, b).

Subtype declarations:

*  S <: T means, that S is subtype of T.
*  S >: T means, that S id supertype of T, T is subtype of S.

List\[subtype\] <: List\[supertype\] - it's correct, it's called covariant relationship. Arrays are not covariant.

To be covariant, class should have only immutable operations and have correct generation for new objects (change output type in case of merge for Lists), good substitution (input is more concrete or more superclass, result is more general or more subclass). Liskov substitution principle.

To implement expression tree we can use:

*  General interfaces => huge implementation (N^2 of growth).
*  def isInstanceOf\[type\]: Boolean, def asInstance\[T\]: T - it's very hacky and risky.
*  OO implementation, define eval in the every class. This approach is limited if we need to look deeper.

Pattern matching:

'''
def eval(e: Expr): Int = e match {
  case Number(n) => n
  case Sum(x, y) => ...
}
'''

Patterns are constructed from:

*  Constructors: Number, Sum etc.
*  Variables: n, x, y ...
*  Wildcards \_, matches everything.
*  Constants.

We can do substitution for the patterns matching.

List - fundamental data structure. Lists are immutable and recursive. Arrays are mutable and flat.

Lists are build from Nil and Cons (:: operator in scala).

(1, 2, 3) means 1 :: (2 :: (3 :: Nil))

Main operations: head, tail, isEmpty.

Patterns for matching: Nil, p :: ps (p - head, ps - tail), List(p1, ..., pn) means p1 :: ... :: pn.

We can implement sorting as insetion sort.

## week 5

List functions: .length, .last, .init (all except the last one), take n, drop n, (i).

List functions: a ++ b, a.reverse, a updated (n, x), list indexOf x, list contains x, splitAt.

pair, tuple.

access: pair.\_1, pair.\_2. or val (x, y) = pair

we can match pairs/tuples: case (nil, x) => ...

We use parametrized functions as arguments. We have scala.math.Ordering. We can write "implicit" before the parameter.

List functions: xs map (x => x \* x \* x). xs filter (condition). filterNot, partition (filter+filterNot), takeWhile (get elements while condition), dropWhile (drop elements while condition), span (drop+dropWhile).

List functions: List(x_1, ..., x_n) reduceLeft Op = (x1 Op x2) Op x3 ...

instead of (x,y) => x \* y, you can write \_ * \_

List fuctions: foldLeft which takes additional param z, (z op x_1) op x_2, ...

List functions: reduceRight (... x_n-2 op (x_n-1 op x_n)), foldRight.

Associative and commutative operations have equavalent on reduceLeft/reduceRight. But if not then results can be different.

We can use induction to prove correctness of the functional programs.

## week 6

In Scala we also have Vector in addition to Array. Vectors implemented with 32-fold Trie (index representation in 32-based system and each digit is a branch in the Trie, we can implement deque in the same way with negative indexes). Vector has faster access, than List.

Vector operations: x +: vector, vector :+ x. Attach an element. 

Seq is superclass of Vector and List, Iterable is superclass for Seq.

We also have Array. String and Array are subclasses of Seq.

Ranges: x until y, x to y, x to y by z.

Seq operations: exists, forall (is condition true for all elements), zip, unzip, flatMap (vs map? -> flatMap concatenes the result, map just maps), sum, product, max, min. 

Seq->IndexedSeq->Vector,Range

flatten method

for (i <- ... \[if i ...\]) yield i...

for (s) e, where s - sequence of generators and filters, e - return expression. generator: p <- x, filter: if f.

You can use {...} instead of (...). Also you can split by semicolons or by newlines.

We have Set in scala and toSet instruction. Sets are unordered and don't have duplicates. main operation s contains x.

mkString function, Vector.fill function

Scala has Map data structure. val X = Map(a->b, ...)

Map can be applied to the key: map(key), throws exceptions.

map get key, return Some(x) or None.

collection.sort, collection.sortWith, collection.groupBy.

map withDefaultValue value

Source.fromURL, input.getLines.toList.

Scala immutable collections are: easy to use, concise (one word instead of loop), safe (type checking), fast (can work in parallel), universal (one vocabulary for all collections).

Main topics: higher-order functions, case classes and pattern matching, immutable collections, no mutable state, flexible evaluation: by name/by value.
