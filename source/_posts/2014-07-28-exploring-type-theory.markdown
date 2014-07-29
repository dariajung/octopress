---
layout: post
title: "Exploring Type Theory"
date: 2014-07-28 22:19:39 -0400
comments: true
categories: [Hacker School, Type Theory, Coq, Emacs]
---

I started off today with a specific goal in mind. By the end of the day, I was pretty off my mark. 

My original intent was to work through a tutorial, [Algorithm W Step by Step](http://www.grabmueller.de/martin/www/pub/AlgorithmW.pdf), for implementing the classic Algorithm W (proposed by Robin Milner) for type inference in Haskell. I was stoked to finally take a closer look at Hindley-Milner and foolishly thought I would spend a few days on it. 

In reality, I had started my descent down the rabbit hole. I found myself reading, and while I felt comfortable with the actual Haskell code itself, the reasons for why the tutorial was implementing things by using sets, or talking about free type variables and type schemes made me feel that while I could infer knowledge from my understanding of Haskell, I was still lacking appropriate knowledge for this literature.

So, I asked this silly question on Zulip:

> **Stream**: Category Theory/Type Theory/Set Theory
>
> **Message**: Hi hi. I'm delving into Hindley-Milner for type inference and I'm finding lots of terminology that I don't understand. Are there any friendly introductions to all of the theories? AM I WAY IN OVER MY HEAD?

[Rntz](http://www.rntz.net/) pointed me to [Types and Programming Languages](http://www.cis.upenn.edu/~bcpierce/tapl/) as a resource and I was intrigued. I started reading it, and of course my attention started to wane because textbooks. After some googling, and remember back to my first week at Hacker School, I was reminded of a UPenn grad course called [Software Foundations](http://www.cis.upenn.edu/~bcpierce/sf/current/index.html). The course uses TAPL but also utilizes an interactive book of Coq proofs as its main text. Interactive? Sign me up.

Two ways to run Coq are through the CoqIDE or through Proof General Coq mode in Emacs. I found to my chagrin that CoqIDE was ugly and slow and in general, not something that I wanted to use. But that meant that I had to learn... Emacs. So for about two hours, I went through the Emacs tutorial and fiddled with my .emacs file, thinking about the time I saw Richard Stallman dressed as a saint from the Church of Emacs and resigned myself to learning a new text editor/operating system/whatever (plz don't hurt me, I'm new to emacs).

After this, I couldn't figure out how to return Coq through Proof General, and time passed while I grew increasingly frustrated. Then Alan to the rescue! He helped me figure out that emacs wasn't correctly loading my path, and once that was fixed, I was able to write Coq and do cute stuff like:

```coq
Proof. reflexivity. Qed.
```

Yay!

Tomorrow I will continue working through Software Foundations. Aki, an alum, has also kindly pointed me to some resources for implementing type inference algorithms which I plan to hit up once I have gotten a feel for the theory behind it. Excited to see where this leads.

Oh, and I remapped ```Caps Lock``` from ```ESC``` to ```CTRL```. So, uh, yeah.
