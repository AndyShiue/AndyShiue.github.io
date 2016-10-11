---
layout: post
title: "The need for another hierarchy of universes in system programming languages"
categories: Programming
---

In the first edition of Martin-Löf's type theory preprinted in 1971, Martin-Löf introduced a universe, normally called \\(\mathcal{U}\\), in his theory.
It contains (i.e. is the type of) all types including the universe itself.
After the theory was quickly found to be inconsistent by Girard, Martin-Löf then presented a so called "predicative" theory, with a hierarchy of universes, each usually written with a subscript, e.g. \\(\mathcal{U}_0\\), \\(\mathcal{U}_1\\), \\(\mathcal{U}_2\\) ..., and the type of each universe is the higher one universe.
So, for example, the type of \\(\mathcal{U}_0\\) is \\(\mathcal{U}_1\\), and the type of \\(\mathcal{U}_1\\) is \\(\mathcal{U}_2\\), and going on and on.
In this article, I exploit the need for (at least) one other hierarchy of universes, written \\(..\mathcal{U}_n\\), in which \\(n\\) is a natural number in the metatheory, as in the above notation \\(\mathcal{U}_n\\).

To explain why other hierarchies of universes would be useful in a system programming language, one should know what system programming is.
System programming is the idea of writing the most efficient program possible; in order to do it, one usually has to have the ability to sacrifice some abstraction and step into the world of direct pointer manipulation, referential transparency, etc. in order to be the closest to the bare metal machine.
The abstraction to sacrifice that I will focus on is Currying, a technique implemented mainly by functional programming languages with the ability to regard functions as first-class objects.
In layman's term, Currying is the idea of eliminating multi-argument functions with single-argument ones.
To achieve it, one sends the arguments one by one to each function that all of each but the last returns a function abstracting over the rest of the arguments.
In the view of category theory, that is possible because of the natural isomorphism between the hom-functor between \\(A \times B\\) and \\(C\\) and the hom-functor between \\(A\\) and \\(C^B\\) in cartesian closed categories.
In a system programming language, we shall minimize the gap between the code the programmers write and the native settings on bare metal.
However, computers nowadays have functions that receive several arguments at once.
If we apply the well-known simplification from multi- to single-argument functions, either the compiler has to generate several partially applied helper functions, or (sometimes necessarily) function pointers have to be passed around.
In either case, Currying induce an overhead to the machine.

Sometimes zero-cost abstractions is achieved by fallbacking to a lower-level outset, retaining the ability to build higher abstraction.
In Currying, the case we focus on, I propose to provide not only uncurried functions by default, but also special mechanisms to be generic over arity.
Below is an example of such a function, in which we sum up 2 natural numbers inductively:

$$
\begin{array}{lll}
sum( & 0       & : \mathbb{N}, r: \mathbb{N}): \mathbb{N} = r \\
sum( & Succ(l) & : \mathbb{N}, r: \mathbb{N}): \mathbb{N} = Succ(sum(l, r))
\end{array}
$$

Note that \\(sum(a)\\) shouldn't be allowed without an explicit lambda because of what is explained.
The next one is a function summing up its arbitrarily many arguments, being generic over arity:

$$
\begin{array}{ll}
sumAll()                              & : \mathbb{N} = 0 \\
sumAll(head: \mathbb{N}, \ulcorner tail \lrcorner: ?) & : \mathbb{N} = sum(head, sumAll(\ulcorner tail \lrcorner))
\end{array}
$$

\\(\ulcorner foo \lrcorner\\) can be seen as flattening a list of arguments.
As usual, the pattern matching syntax \\(\ulcorner _ \lrcorner\\) is for deconstructing value, and the term syntax \\(\ulcorner _ \lrcorner\\) is for constructing one.
Specifically, if someone writes \\(sumAll(1, 2, 3)\\), pattern matching matches \\(head\\) to \\(1\\) and \\(tail\\) to \\(2, 3\\); the \\(\ulcorner _ \lrcorner\\) syntax is meant to collect several arguments.
On the other hand, the recursive call on the right hand side is applied with the arguments \\(\ulcorner tail \lrcorner\\).
Here, the same syntax expands the arguments we collected.

What should be the type of \\(\ulcorner tail \lrcorner\\)?
The most obvious choice is that it should be a homogeneous list generic over some type \\(T\\).
In lots of programming languages without Currying, variable arguments is implemented that way.
However, it could sometimes be too restrictive.
For example, it cannot express the arguments in the argument list is alternating between some type \\(T\\) and another type \\(U\\).
What is the way to build abstraction in programming languages?
An obvious and primitive notion are functions.
Therefore, directly or indirectly, what should be filled into the question mark should call a compile-time function that generates the argument list.
Why "compile-time"?
We can then monomorphize the function upfront before running it, making the overhead minimal.
The whole idea of compile-time functions and arguments is described [here](http://andyshiue.github.io/programming/2016/05/01/modes.html) with the concept of *modes*.
I'm just going to make a very brief review of the notion we need to proceed.

I introduce another way to pass arguments, called **const mode**, in which the arguments should be supplied at compile time.
Arguments in const mode are written inside brackets (\\([]\\)) and can be inferred.
Actually, the type of the argument list should be an argument in const mode.
We can call purely functional **const function** in const mode.
Now the \\(sumAll\\) example can be fully defined using const mode and a const function called \\(replicate\\), which is a function generating the list of arguments of the same type:

$$
\begin{array}{lll}
replicate[0: \mathbb{N}]       & (T: \mathcal{U}) : ?? = \ulcorner  \lrcorner \\
replicate[Succ(n): \mathbb{N}] & (T: \mathcal{U}) : ?? = \ulcorner T, replicate[n](T) \lrcorner
\end{array} \\
\begin{array}{ll}
sumAll()                                                              & : \mathbb{N} = 0 \\
sumAll[Args: replicate(\mathbb{N})](head: \mathbb{N}, \ulcorner tail \lrcorner: Args) & : \mathbb{N} = sum(head, sumAll(\ulcorner tail \lrcorner))
\end{array}
$$

How would \((??\)) be, then?
If we say the type of a heterogeneous list is the list of the types of each member of the list, we might want the type of the list to also be heterogeneous.
Fortunately, we don't have to recurse forever to build higher-order argument lists because of a feature of normal type systems:
The type of the type of any value is a universe.
With a cumulative hierarchy of universes \\(\mathcal{U}_0 <: \mathcal{U}_1 <: \mathcal{U}_2 ...\\), the types of any arguments would belong to a universe.
We can assign each \\(\mathcal{U}_n\\) a universe \\(..\mathcal{U}_n\\) which is a list the type of which is \\(\mathcal{U}_n\\) and have arbitrary length; because of cumulativity, the types of all arguments belong to a sufficiently large \\(\mathcal{U}_n\\).
Therefore, \\(??\\) would be \(..\mathcal{U}_n\\), for a sufficiently large \\(n\\).
