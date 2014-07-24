---
layout: post
title: "A Working gunzip and Soldering"
date: 2014-07-24 10:01:32 -0400
comments: true
categories: [Hacker School, gunzip, Haskell, Soldering, NeoPixels, Party Planning]
---

Yesterday was a super productive day for me. In the morning, I was in the midst of debugging my gunzip implementation in Haskell. 
I have a function ```addItem``` that adds a node to a HuffmanTree by writing an IORef val because I needed mutability. When I'm creating the HuffmanTree, I need to add a whole slew of values (from a code table) into the tree, so I mapped the addItem function over the list of codes, which returned ```[IO()]```. My problem here was that despite having added items to an initial empty tree, I was returning an unaltered tree. I was confused because I was sure I had allowed for mutability! But why?!

Luckily, Alan happened to be running an impromptu session on Monads where he covered the IO Monad, and attending that helped me figure out what my problem was, I think.


I'm still not precisely sure if I'm understanding correctly but ```[IO()]``` is a list of ```IO()```s. And things in the IO monad won't evaluate until run-time. So basically I had a list of thunk-like things that wouldn't write until evaluated.


This does not work
```haskell
let added =  map (\(label, codes) -> addItem root label codes) code_table
```

but this works
```haskell
added <- sequence $ map (\(label, codes) -> addItem root label codes) (code_table)
```

As an aside, ```added``` is actually a useless value (it's just a list of ```()```s). I don't care about it. All I care about is the value of ```root``` because I have mutated it to add nodes to it.

After this, I spent some time fixing off by one errors because I was translating Julia code to Haskell and Julia is 1-indexed while Haskell is 0-index. Lol. THEN IT WORKED. HUZZAH!

In the afternoon into the evening, I worked with Dana, Minnie, and Sophia on soldering chips, wires, and LEDs together. It was loads of fun and will continue today, I suspect.

![](https://pbs.twimg.com/media/BtRShaVIUAAQ6LR.jpg:large)