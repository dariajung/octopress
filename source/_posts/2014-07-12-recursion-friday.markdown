---
layout: post
title: "Recursion Friday"
date: 2014-07-12 12:38:25 -0400
comments: true
categories: [Hacker School, Recursion, Haskell]
---

Yesterday at Hacker School was Recursion Friday. Basically, a group of HSers sat down and worked on various recursive problems and brain teasers in the languages of our choice. 

Recursion used to make me go like this:

![Scared](http://media.giphy.com/media/NoglyWTK9tCMw/giphy.gif)

But somewhere along the way as I was learning Haskell, recursion started to click with my previously recursion-addled brain.

One of the questions yesterday was to find all of the permutations of a string. After some white boarding with Denise and Georgi, talking it through with Alan and Tom, we basically came to the conclusion that the algorithm should be something like this (in pseudocode):

```
Permute("abcd") =
    "a" + Permute("bcd") 
    <list concatenation> 
    "b" + Permute("acd") 
    <list concatenation>
    "c" + Permute("bcd") 
    <list concatenation>
    "d" + Permute("abc") 
```

So, generate all of the permutations of the string without one of the elements of the original string, and concat it with all possible permutations of the smaller string, then concat all of those together to get the final list of permutations.

After speaking with Alan about a Haskell implementation, this is what I ended up with

```haskell
import Data.List

permute :: Eq a => [a] -> [[a]]
permute [] = [[]]
permute xs = [ y | prefix <- xs, y <- map (prefix:) 
                   $ permute $ xs \\ [prefix]]
```

An obnoxiously short list comprehension.

Pull the prefix from the original string, map a list concatenation of the prefix, (prefix:), to the various permutations of the rest of the string. ```\\``` is this nifty function in the Data.List library that performs list difference, so it was an easy way to exclude the prefix from the original string (thanks to Alan for showing me that). 

```haskell
ghci> permute "abcd"

["abcd","abdc","acbd","acdb","adbc","adcb",
"bacd","badc","bcad","bcda","bdac","bdca",
"cabd","cadb","cbad","cbda","cdab","cdba",
"dabc","dacb","dbac","dbca","dcab","dcba"]
```

Recursion still blows my mind.