---
layout: post
title: "Sipping on Elixir"
date: 2014-08-21 00:57:53 -0400
comments: true
categories: [Hacker School, Elixir]
---

```
 __________
< holy cow >
 ----------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

It's almost the end of my batch at Hacker School, but it's okay because I'm never [ever] graduating. &#10084;

<hr/>

This past week [José Valim](https://www.hackerschool.com/residents#José-Valim) has been in residence at Hacker School! José is the creator of the Elixir programming language, which is built on top of the Erlang Virtual Machine. (Joe Armstrong has said that Elixir "is good shit." [Seriously!](http://joearms.github.io/2013/05/31/a-week-with-elixir.html)). José is also a core contributor to Rails. So. Rad.

On Monday night, José gave us a quick introduction to Elixir and explained that Elixir is a functional, concurrent, but most importantly, a distributed language. He gave us a bit of background on Erlang and its origins as a language used for telecommunication. Erlang provides support for fault tolerent, non-stop, real-time applications. Also, hot swapping is pretty cool (which José did a demo of in Elixir). For these reasons (and many more), Erlang is the language used in messaging systems like Facebook messenger and WhatsApp.

I've been spending the past few days working through [Etudes for Elixir](http://chimera.labs.oreilly.com/books/1234000001642) in order to get a quick introduction to the language, and get myself up and running. 

Some quick first impressions/takeaways: 

Elixir is compatible with Erlang code, but it has a nice Ruby-like syntax. It's kinda like the love child of Ruby and Erlang.
Elixir has all the goodies like pattern matching, list comprehensions, anonymous functions that I heart from Haskell. There aren't quite type signatures; instead, there are these things called [specs](http://elixir-lang.org/docs/stable/elixir/Kernel.Typespec.html). Specs are mostly used for documenting code, but on some occasion, people use tools like [Dialyzer](http://www.erlang.org/doc/man/dialyzer.html) to find type errors (I will probably check this out at some point).

One thing I find super cool about `iex`, the Elixir repl, is the `h` command to read documentation.

![](/images/iex.png)

Also, Elixir has SUPERB documentation. I've been very pleased with how well explainations are written out, and that there are examples! Examples!

I'm making my way through most of the topics in Elixir's [getting started](http://elixir-lang.org/getting_started/1.html) section through études (currently getting acquainted processes), and I'm excited to learn about Mix and OTP next. In general, I'm excited to get deeper into Elixir since I don't know much about concurrent and distributed programming.

Today, José did a seminar on how Iterators are implemented in Elixir, going over eager map, eager filter, the idea of inlining and so on before introducing us to the idea of lazy map, etc. It was a very informative session and I will write about that more in a different blog post.

And just throwing this out there: HOW COOL IS IT TO BE ABLE TO ASK QUESTIONS IN PERSON TO THE CREATOR OF THE LANGUAGE YOU'RE LEARNING? Thanks a ton to Hacker School for this amazing opportunity.

So far, learning Elixir has been quite nice, and the transition from Haskell to Elixir has been pretty smooth.

Looking forward to all of the things I learn before the end of my batch.