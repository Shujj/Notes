# Parser Combinator

__Recursive descent parser__ is a top down parser built from set of mutually recursive procedures each procedure implementing on of the productions of the grammar  
__Left recursion__ happens when `A -> Aa` either directly or through a series of substitutions. This is pertinent here because it leads to infinite recursion in recursive descent parsers.

> parser combinator is a higher-order function that accepts several parsers as input and returns a new parser as its output. Parser combinators enable a recursive descent parsing strategy that facilitates modular piecewise construction and testing. This parsing technique is called combinatory parsing.

So its a recursive descent parser with __parsers as procedures__

# Monad Transformers
Monads don't have the composablity of functors.  
If you have `functor` of `A` and `B` you can derive the functor for any `A[B[T]]` by composing functors for `A` and `B`
```scala
val a : Option[X]
val b : List[Y]
val ab : Option[List[Z]]
val function : Z => ZResult
// mapping f over ab aka defining map for type X[Y[_]]
ab.map(_.map(f))
```
In essence `functor[A[B[_]]] = (functor[A[_]])(functor[B[_]])`. No special knowledge of types `A` and `B` is required apart from the fact they have a functor defined for them.
This doesn't work for monadic compositions. 
```scala
val a : Option[X]
val b : List[Y]
val ab : Option[List[Z]] 
val function : Z => Option[List[ZResult]]
// trying to define flatMap[T[U[_]]] in terms of flatMap[T[_]] and flatMap[U[_]]
ab.flatmap(_.flatmap(function))
// this works but need info about the inner monad
ab.flatmap(x => x match {
                  case List()
                  case Nil => None // unit of outer Monad unit()
                }
)
```
The inner flatMap works only with `Z => List[Z]` We need information about `b type` so that we can apply `function` properly on `a type` i.e we need to free `Z` from the clutches of `List[Z]` which requires 

// blah blah blah ... come back again later 
