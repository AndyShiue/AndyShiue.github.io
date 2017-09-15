---
layout: post
title: "Coinduction"
categories: philosophy
---

# Coinduction

There's only one way, namely *impurity*, to produce an instance of a coinductive type. What I was wondering is, in comparison, *why can we build inductive types anywhere?*

I realized it's because the `IO` monad represents **everything** the subject observes; other coinductive types exist merely for convenience. If inductive types can be built from sum, product and exponential, that all of them can be used to build coinductive types is self-evident, for the reason that they, as well as induction rules, are *induced*, which is why mathematical *induction* has its name, despite being deductive.

In my opinion, time can be described as a stream of predicates. Never do I find the use of a type more complex than a colist for it. Not assuming my death, I'm still young, hence the coinductivity. As far as being predicates, in Martin-Lof type theory it's no different from a set, which is no different from small types except being open. The open universe and the IO monad exist for the same reason, that is, to isolate chaos.

During writing this article, I changed my mind on whether induction is just an illusion. If it were, how is coinductive types any different while people have been analyzing them? At the end, illusion is just a specific kind of induced observation.
