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
System programming is the idea of writing the most efficient program possible; in order to do it, one usually has to have the ability to sacrifice some abstraction and step into the world of direct pointer manipulation, referential transparency, etc. in order to be closest to the bare metal machine.
The abstraction to sacrifice that I will focus on is Currying, a technique implemented mainly by functional programming languages with the ability to regard functions as first-class objects.
In layman's term, Currying is the idea of eliminating multi-argument functions with single-argument ones.
To achieve it, one sends the arguments one by one to each function that all of each but the last returns a function abstracting over the remain arguments.
In the view of category theory, that is possible because of the natural isomorphism between the hom-functor between \\(A \times B\\) and \\(C\\) and the hom-functor between \\(A\\) and \\(C^B\\) in cartesian closed categories.
In a system programming language, we shall minimize the gap between the code the programmers write and the native settings on bare metal.
However, computers nowadays have functions that receive several arguments at once.
If we apply the well-known simplification from multi- to single-argument functions, either the compiler has to generate several partially applied helper functions, or (sometimes necessarily) function pointers have to be passed around.
In either case, Currying induce an overhead to the machine.
