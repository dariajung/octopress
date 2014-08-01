---
layout: post
title: "Re-learning Math with Coq"
date: 2014-07-31 10:25:40 -0400
comments: true
categories: [Hacker School, Coq, Proofs]
---

The last time I was doing a lot of inductive proofs was during my third year of high school. I did a few in my Discrete Mathematics class, but to be quite honest, I hardly remember anything from that it (I should really revisit the material at some point...).

Considering that it has been more than four years --I took a gap year between my second and third year of university, I am now going into third year-- I was a bit unsure of my math chops. But working through [Software Foundations](http://www.cis.upenn.edu/~bcpierce/sf/current/index.html) has been an absolute blast. And it's been so cool to see the [Curry-Howard correspondence](http://en.wikipedia.org/wiki/Curry%E2%80%93Howard_correspondence) in action through writing proofs in Coq. 

Rntz gave a great presentation on [Curry-Howard](https://github.com/rntz/curry-howard-slides/raw/master/pres.pdf), presenting formal logic, a lambda-calculus, and then showing the connection between formal logic proofs and typed expressions/programs.

So far, I've been spending time proving some mathematical axioms such as the additive identity, multiplicative communtativity, right distributive property of multiplication over addition of numbers, and so on.

Coq has various proof tactics, `intros`, `destruct`, and `induction`, to name a few.

To show you the kind of stuff I've been doing, let's work through an example.

Let's prove that `n + 0 = 0`.

First we define the theorem (adding a 0 to the right side of a natural number gives us the original natural number):

```coq 
Theorem plus_0_r : forall n:nat, n + 0 = n.
```

So how do we prove this?

Well, first we need to introduce n into the scope of the proof.

```coq
Proof. 
    intros.
```

Coq shows us that we can now work with n, and that our subgoal is to prove that n + 0 = n.

```coq
1 subgoals, subgoal 1 (ID 88)
  
n : nat
============================
n + 0 = n
```

Cool. And now we can induct on n. In induction, you must prove the base case of `n = 0`, and for `n = S n'`; `S n'` can be read as the _successor_ of n', which is equivalent to n.

So now, we use the `induction` tactic in Coq:

```coq
Proof. 
    intros. induction n as [| n'].
```

Now we have two subgoals to prove, the base case and the successor case:

```coq
2 subgoals, subgoal 1 (ID 91)
  
============================
0 + 0 = 0

subgoal 2 (ID 94) is:
S n' + 0 = S n'
```

For my own benefit, I like to write out what case I am proving, which in this case is for when `n = 0`. 
As we see, Coq gives us `0 + 0 = 0`. We can simplify this expression by writing `simpl`, and Coq will reduce this to `0 = 0`. And we know `0 = 0`. It's a fact. We can simply write `reflexivity` to finish proving this subgoal.

As a sidenote, reflexivity will simplify for you, so it wasn't necessary to do the `simpl` step. However, I found it helps my thought process to write out all of the steps.

```coq
Proof. 
    intros. induction n as [| n'].
    Case "n = 0". simpl. reflexivity.
```

Coq now tells us we have one subgoal remaining:

```coq
1 subgoals, subgoal 1 (ID 94)
  
n' : nat
IHn' : n' + 0 = n'
============================
S n' + 0 = S n'
```

As you can see, we are given `IHn'`, an induction hypothesis to work with. So let's prove our second subgoal for case "n = S n'":

We can simplify this down to `S (n' + 0) = S n` by using the `simpl` tactic. Adding a 0 to n', and then calling a successor on it is no different from adding 0 to the successor of n'.

```coq
1 subgoals, subgoal 1 (ID 101)
  
Case := "n = S n'" : String.string
n' : nat
IHn' : n' + 0 = n'
============================
S (n' + 0) = S n'
```

But what's this? We have an induction hypothesis that tells us that `n' + 0 = n'`. Oh, this looks familiar. So let's rewrite `S (n' + 0)` using our induction hypothesis:

```coq
Proof. 
    intros. induction n as [| n'].
    Case "n = 0". simpl. reflexivity.
    Case "n = S n'". simpl.  rewrite -> IHn'.
```

```coq
1 subgoals, subgoal 1 (ID 102)
  
Case := "n = S n'" : String.string
n' : nat
IHn' : n' + 0 = n'
============================
S n' = S n'
```

Omg, the left and the right are equivalent. And now we can say, this is true by reflexivity, and end our proof by writing `Qed.`

Our full proof:

```coq
Proof. 
    intros. induction n as [| n'].
    Case "n = 0". simpl. reflexivity.
    Case "n = S n'". simpl.  rewrite -> IHn'. reflexivity.
Qed.
```

HOW COOL IS THAT???
