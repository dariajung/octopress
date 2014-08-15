---
layout: post
title: "Whiteboarding to Unconfuse Myself"
date: 2014-08-15 14:38:04 -0400
comments: true
categories: [Hacker School, whiteboarding, Haskell, Lenses]
---

A few days ago, I stumbled on a [repository](https://github.com/jwiegley/category-theory) on GitHub that was exploring category theory through the use of Coq, formalizing Edware Kmett's Hask library. Curious, I wondered what Hask was and read the description: "Category theory for Haskell with a lens flavor". 

But... what are lenses?

I remembered that I had bookmarked a [blog post](http://blog.jakubarnold.cz/2014/07/14/lens-tutorial-introduction-part-1.html) that Steve Klabnik tweeted a while ago because it was related to Haskell. And now it was relevant to my interests.

Lenses are, at a high level, something like "getters" and "setters" that are used in imperative programming languages. It's not uncommon to see something like `book.author.name`. Lenses provide an abstraction like this for Haskell.

I spent a long time staring at the explanations in this blog post, and after pairing with Alan a bit on a simple Lens implementation, felt blown away by the weirdness and how elegant of an idea this was.

A realization that I had about working with Alan (after ten weeks...) is that he is the type of person to think things out by writing on a white board. Up until this point, I had never really thought about whiteboarding as a way of getting my thoughts out so that I could actually *look* at them. And the act of writing type signatures out instead of staring at them on a screen made a lot of difference for me. (I do write on scratch paper, but I generally do so very disorganizedly).

After Thursday demo presentations, I spent about thirty minutes whiteboarding out my thought process for the implementations of `over` and `set`:

![whiteboarding 1](/images/wb2.JPG)

![whiteboarding 1](/images/wb1.JPG)

I guess moral of the story for me is that I should whiteboard more to figure out what I'm doing when I'm confused before jumping straight to code. A very simple epiphany, but a very helpful one.