# nya

## nya the catgirl

![nya](http://i.imgur.com/UcqXJyPl.jpg)<br>
a photo of nya-chan (taken by [SciFi](http://konachan.net/post/show/191401/animal-animal_ears-black_hair-cat-catgirl-cat_smil))

nya is an adorable catgirl who lives in a wonderful world paralleled
with us called にじげん. She's cute, smart, and always curious about
the world she lives. "Ahhh? Nya-chan want to check its type nyaaa~" is
what she speak most.

nya, strictly speaking, is not a programming language. Because she
does not aim to be anything executable. In the other word, I didn't
even plan to write an evaluator for her.

nya is a field for me to carry out my own idea about how a
contract-based static type-checking system should be.

nya consists of a simple dynamic-typed language and a type system for
the language.

お楽しみに!

## features

Kinds of types supported:

* regular types (T): `Int, Str, Bool`
* union types (U): `(T/U Int Str)` *(I planned to improve the syntax for this in the future)*
* function types (F): `(Str -> Str)`

Currently only above will be implemented, because I failed on the
trial implementing these features myself:

* type parameters: `(Array Int)`
* polymorphic types: `(Array a -> Int)`
* ~~type functions~~

However, these two features will still be expected in the future
versions, perhaps after I know more about contract-based type
systems. (These are more likely to be implemented in System-F type
system, I will implement that as my next project)

As one of my fav features, functions *always* curry. So the expression `(+ 1)` has the type `Int -> Int`, given that `(+ :: Int -> Int -> Int)`.


<sup>[1]</sup>: custom types are quite the same as regular types,
except the latter ones are built-in.


## limitations & todos

nya cannot handle type check on recursive function yet. ~~While you can
rewrite your recursive function with help of fixed point combinator to support
it.~~ No, you cannot use Y-combinator as it requires dynamic types,
also there is no fix-point combinator built-in in nya so far. That is
to say, you cannot have recursive function at this point.

Nonetheless, I will add support for that in the following versions.


## type detection & type check
nya features type detection and type check. That means you can ask nya
"what's the type of this expression" and she will give you a proper
answer. If you fed her with a wrongly typed exprssion and ask about
its type, like `(+ "abc" 1)`, she will be sad tell you that she cannot
handle it because there is a consistency in type.

## nya's syntax

### commands

* `(annotate name :: type)`: annotate a name with a type signature
* `(deftype typename)`: define typename (does actually nothing, only for legibility)
* `(def name expr)`: define a variable with the value of given expression

### expressions

* `(if cond then else)`: just if, simply, cond part will be required to have type 'Bool'
* `(let var val expr)`: bind the result of val to var, and expression expr under the new binding
* `(fn :: type [params ...] body)`: define a function with type specified. the params and the body will be type checked.
* `1,2,3,...`: integer values
* `"xxxx",...`: strings
* `#t,#f`: boolean values
* `var`: any symbol is an identifier
* `(func args ...)`: apply args to func
* `(:: expr type)`: type annotated expressions, the type check of expression will be ignored and the result of the whole expression will be the given type
* `($ exprs ...)`: just like bracket-ed expressions, in order to distinct from function calling.

### type signatures

* `Int,Bool,Str`: built-in types (actually the same as regualr types)
* `A`: a name started with uppercased letter is a regular type
* `(T/U A B C)`: union of types `A`, `B`, and `C`.
* `A -> B -> C`: function type, means that it takes values in type `A` and `B`, and return something in type `C`
* `(A)`: the same as `A`
* `A -> (B -> C)`: equivalent to `A -> B -> C`.

types can be nested, for example, you can have:

```
(T/U (A -> B)
     (A -> (T/U B C)))
```

as a valid type signature.

## more?

Just read the code, I left some comments in the source code!
