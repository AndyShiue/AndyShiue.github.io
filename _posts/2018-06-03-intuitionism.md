# The Rise of Intuitionistic Logic

華語版：http://andyshiue.github.io/2018/06/03/intuitionism-zh.html

# Preface

First of all, I want to express my gratitude to National Tsing Hua University (NTHU)  for accepting my application of enrollment without my taking the ability test, but through an independent program to find students who have special skills, and my specialty is about programming languages and logic, which are the topics of this essay.

Interestingly, although this is the required essay for our freshman Mandarin course, I wrote the whole of it in English first and translated back to Mandarin, perhaps because there was almost no Mandarin resources of this kind so I was used to English in these specific topics.

This whole essay is intended for readers without any background of intuitionistic logic, though some common sense would indeed be useful. After finishing reading this essay, It would be my pleasure that the reader would be able to know the good parts of intuitionistic logic, or even better, to dive into this area.

# Overview

Since antiquity, there has been certain efforts being put on rigorous bases in math, which, eventually led to some standalone foundation, namely mathematical logic, between non-formalizable philosophy and all formal math, whereas more advanced concepts in math are defined within the system from more basic constructs.

In addition to having the ability to define new (mathematical) objects in a system, there also has to be some way to observe their interactions, perhaps closer to the common perception of what ‘logic’ means. From what constitutes varieties of mathematical logic, propositional logic is probably the most widely-accepted framework, reasoning about causes and effects. Some implications of it could be the chain rule, that if p causes q and q causes r, then p causes r, or the double negation rule, which says that something is true if it’s not false.

However, after propositional logic, there was a split among schools of logicians. Set theorists build up the domain of math with untyped sets; type theorists, on the other hand, presuppose there are objects of different, somehow incompatible types. As time goes by, set theories have become dominant in math, however, later research has revealed the incredible expressiveness of type theories compared to set theories.

This essay aims to provide a brief, incomplete introduction of the meaning of intuitionistic type theory, and why it hasn’t been popular yet despite the logic’s somehow being more “intuitive” for human beings, or perhaps more importantly, especially for computers, in my opinion.

# The Origin of Axiomatized Math: Euclid’s Geometry

We start from history and trace back to the inception of math. In order to provide some reason to a phenomenon, we explain it from simpler known facts, the process of which is called “deduction”. However, after rounds of deduction, any observation would ultimately be traced back to some a priori knowledge, that can only be taken for granted. Math, from a platonic view, is the idealization of the reality, and it seems natural enough to assume first causes, called “axioms”, exist in math and serve as the laws of the primitive notions along with the deduction rules.

Euclid, the ancient Greek mathematicians, pioneered in using axiomatized method to provide a basis of his geometry and attempted to conclude his discovery with 5 axioms. Although the axioms are later known to be far from complete, this kind of methodology has seen great success.

Even though students in math nowadays would probably think it’s easier, the axiomatization of natural numbers happens much later in the history of math, by Peano in 1889.

# Formalism: Merely Manipulating Symbols

The syntax to write math was also evolving at the same time. For example, parentheses were introduced in 1544, and the equal sign was introduced in 1557. Since late-19th century, the core of math, namely its logic, was eventually getting symbolized gradually. That everything in math is formalizable as symbols has led to a radical view on math, that

> (math) is much more akin to a game, bringing with it no more commitment to an ontology of objects or properties than ludo or chess.
> (https://plato.stanford.edu/entries/formalism-mathematics/)

It sounds like there’s some ironic defiance over the ancient Greek platonism, in which math is thought to represent perfect, ideal objects behind physical ones. Which means formalism is ...

> ... the view that mathematics is a meaningless formal game played with marks on paper, following rules. Traces of a formalist philosophy of mathematics can be found in the writings of Bishop Berkeley, but the major proponents of formalism are David Hilbert (1925) ...
(Philosophy Mathematics, Ernest)

# David Hilbert’s Dream

The perspective of math as a game would inevitably lead to a goal: to find the best rules of the game. The program led by mathematician David Hilbert around 1900 had such grand goal. Hilbert wanted to find some rules of math that is both

1. consistent, and
2. complete

A theory is consistent if any derived statement cannot be proved as both right and wrong; a theory is complete if every statement can be proved as either right or wrong. The former seems like a more basic requirement because saying something is both right and wrong is always utter nonsense at first sight. The latter would definitely be harder from the point of view of philosophy: if you view morality as a game, then you have to make sure you can identify anything as either justice or not from some basic arguments. It was thought that maybe it was easier to do something similar to math to make everything either true or false. The naïve plan is to add the newly-discovered undecidable statements as new rules. It’s like adding some act as a rule of morality if it was previously in the gray area. This is Hilbert’s dream, to provide a solid foundation that is guaranteed to be perfect for math. It was a pity that it was later proved to be impossible.

Kurt Gödel published such result in 1931. His first theorem stated it’s impossible for a useful system (“rules of game”) to be able to be both consistent and complete. What’s worse is that, his second theorem states it’s not even possible to prove the consistency of the rules inside the same system.

We can only believe in the consistency, but the first theorem suggests we shall not find a complete theory, but a reasonable one, and members in one school of mathematical philosophy has some criteria for choosing such rules, that is, not to be true, but to be constructive.

This is my opinion, and also the topic I want to discuss about. This is intuitionism.

# Classical Logic for the Truth, Intuitionistic Logic for the Right

At the beginning, intuitionism is literally, based on intuition. The pioneer of intuitionism, L. E. J. Brouwer, described intuitionism as:

> Completely separating mathematics from mathematical language and hence from the phenomena of language described by theoretical logic, recognizing that intuitionistic mathematics is an essentially languageless activity of the mind having its origin in the perception of a move of time. This perception of a move of time may be described as the falling apart of a life moment into two distinct things, one of which gives way to the other, but is retained by memory. If the twoity thus born is divested of all quality, it passes into the empty form of the common substratum of all twoities. And it is this common substratum, this empty form, which is the basic intuition of mathematics.
> (Brouwer's Cambridge lectures on intuitionism)

At that time, intuitionism is the same as neither formalism nor platonism, but as time goes by, they started to converge as a whole and intuitionism has gradually become synonymous with constructivism. Nowadays, intuitionists are also fine with the formalistic approach: to encode rules as sequences of symbols and manipulate those formulas. However, constructivity still and will still stand as an essential feature that makes it different to traditional math.

Below, I’m going to introduce an example to describe what constructivity, or rather, what non-constructivity is. Let’s say Anne is a violent little kid who is used to lying. Anne’s parents set out two rules for her to teach her the polite behavior.

1. Fighting with the others makes Anne get punished.
2. Lying makes Anne get punished.

Now, if Anne said to one of her parents, “I punched Shen.” The reader should think for a while now, that should Anne be punished?

According to classical logic, Anne must be punished. We know Anne is either lying or not. If she is lying, then she must be punished due to it, but if not, she must be punished for fighting.

However, assuming the two bad acts ought to receive different sorts of punishment, how should you punish Anne if you were her father? In the above deduction, it merely says she will be punished without providing any concrete method to do it. Therefore, in the constructive outset, it should not be provable that Anne will be punished without any further evidence given that we cannot construct such punishment. It might be true that Anne will be punished, but there hasn’t been a correct way to do it, and this is the gist of constructive math.

We can say that in constructive math,

* If you want to prove an implication, there must be some procedure, namely how the cause is transformed to the outcome.
* If you want to prove an existence, there must be a specific instance.
* If some statement or another is true, then the one that is really true must be specified.

In the above example about Anne, the option about the truth not being specified breaks constructivity. The core issue is that, we naïvely assume any statement must be false if it isn’t true; this shares the similarity to the aforementioned double negation rule, which says if the opposite of something is wrong, then it’s right, without giving an evidence. These are very reasonable speculations, but at the same time aren’t constructive at all: we simply can’t explain why it is so and how the opposite can be explained, and explainability is constructability. By the way, the last several usage of the word “truth” above is not in a classical sense, but has the meaning of “being constructable”.

# Curry-Howard Isomorphism

From the above introduction of constructivistic meaning, you may notice that implication, by its nature, is just a function, or transformation, if you prefer this terminology. In this kind of interpretation, provability of statements are viewed as mathematical objects indifferent from numbers of vectors, and implication is just a special case of a function from a statement to another. This is the most obvious link between two fields, proofs and programs, connected with the bridge “Curry-Howard isomorphism”.

First I want to say, lots of theorems have very different proofs for each of them. It would be possible to view a theorem having proofs as a type having elements. Proofs and elements are properties of its owner, and maybe we can be more aggressive, to say that elements are exactly proofs, or an “evidence” of such type, if you prefer this better word. Hence, types are statements in the sense that types have elements and statements have proofs. The scary name “Curry-Howard isomorphism” is just a jargon for such concept.

Back to some theoretical part, we say truth is any inhabited type, and falsity is the empty type due to its lack of evidence. The negation of a statement is defined reasonably to be a function from the statement to the falsity. The falsity is the same as absurdity, or a contradiction, and it is the thing we want most not to be able to prove. We say some statement is wrong if it can deduce a contradiction, and this is also written as its opposite being right.

If things are either right or wrong, this would mean for a statement we can’t prove to be right, it must be empty (having no evidence) because it has a function into emptiness. However, in this situation the “it must be empty” part isn’t constructive.

Functions, or to say transformations, is exactly the core of programming. I was amazed at how math and programming fit together so well several years ago. In this unified world of intuitionistic logic, programs and proofs work seamlessly. We can write programs in the unified language and later prove some of their properties, or we can require some proof for some function to be run on the computer. All of these, is already a dream for the undergraduates nowadays. In the traditional setting, we have nothing like this. However, classical logic is still what students are being taught in the world. In my opinion, not teaching intuitionistic logic stagnates the interdisciplinary education that’s been on hype in NTHU, at least in some parts.

# Why isn’t intuitionistic logic a success?

From what I see, the reason why intuitionistic logic isn’t really successful can be split into two parts: from the point of view of programmers, and from that of mathematicians.

On the side of programmers, programming languages that make extensive use of intuitionistic logic is often perceived as being too hard. Firstly because the current dominant paradigm of programming is still Object-Oriented Programming (OOP), not the functional programming that leans toward intuitionistic logic more. Second, there’s a tendency to make everyone able to write the code, without the need to be really professional. This could make big companies be conservative about their designing programming language, such as the Go programming language designed by Google.

However, the current trend is already going towards functional programming, that is considered to have a more solid theoretical foundation. When it comes to beginner-friendliness, there are already very difficult programming languages widely adopted in the industry such as C++. Moreover, if you don’t like to prove stuff in programming, you have the right not to do it, and in the case of C++ there are in contrast footguns that are unavoidable. Thus, I think such complex logic system isn’t much of an obstacle for its industrialization here.

I think the actual major reason that intuitionistic logic isn’t widely adopted in math is its slower development in history. People in the early-20th century seemed not to realize the importance of intuitionistic logic. Maybe the main reason is that computers weren’t even invented yet at that time and such logic system needs more sophistication. After set theory came out as the foundation of math, the society simply got stuck, which is similar to the situation in programming with OOP. They are just monopolizing the market first.

However, the situation in programming is changing. Thomas Samuel Kuhn introduced the concept of paradigm shift, that over time the scientific (here, mathematical) community could be abruptly transformed to perceive things in a very different way, and I believe given the increasing importance of computers, that day will finally come.

# Appendix I: Possible applications of intuitionistic logic

In the traditional approach, verification of a program is done by passing all the test cases. However, this can only spot the incorrectness of the program, but not guaranteeing it’s really done right. By utilizing some intuitionistic logic, we can know it doesn’t go wrong for sure.

In my opinion, intuitionistic logic could be used in several sectors that are not allowed to go wrong, such as the aerospace industry, banking systems, and one of the hottest topic in the field of programming currently – blockchains, witch are virtual currencies without a controlling authority. Although the cost of proving all the specifications could be very high, I still hope proving techniques will be adopted widely, due to the selfish reason that I’m interested in it and good at it.

# Appendix II: Multiple Identities – The Prospect

In this section, I want to provide a glimpse of the cutting-edge research area. A quite important branch in modern intuitionistic logic is the so called “higher-dimensional type theory”, which is centered on the concept of equality. Below, I’m going to tell an old philosophical problem, not to argue about the correct solution to it, but to demonstrate the actual difficulty of defining what equality is.

Let’s say there’s a ship made of wood. As time goes by, the ship slowly got rotten, and those rotten parts would be replaced by the new materials. After all old woods of the ship have been replaced by new pieces, is the new ship still the the original one?

Different philosophers’ opinion diverge, and I won’t discuss about any of them. But since there could be different interpretation of what equality is, why not make it possible for anyone to define their equalities? Again, an equality could also be seen as some mathematical object and when someone says two things are equal, they can specify in what sense they are by picking the notion they prefer, and it basically defers the right to decide to the people. Perhaps this is the most important intuition for higher-dimensional type theory.

However, those sorts of equalities defined by different people are possibly not equal; this suggests there could be two equal equalities, or equalities of equalities. We can even go on and on and construct higher equalities.

Much like our viewing proofs and elements as two ways of describing the same thing, in higher dimensional type theory, elements or proofs are again viewed as points in a space as a trinity, and a simple equality could be viewed as a line between two points. Those higher equalities can be two-or-more-dimensional faces and can be used to build the globular shape of a space, hence the name higher-dimensional type theory.

This section might be too hard for a reader who isn’t in this field, however, I included it in this essay, hoping to attract someone to go into this fledgling field.
