---
layout: post
title: "Hacker School: Day 7"
date: 2014-06-18 16:22:18 -0400
comments: true
categories: [Haskell, Hacker School, Applicative Functors, Lifting]
---

I can't believe it has already been a week and a half at Hacker School. Wow. 12 weeks seems like a lot but the time is already flying by.

Today, I decided to resume my studies in Haskell. I worked on the week 11 assignment for Brent Yorgey's Haskell course. I continued working with the ```Parser``` data type, implementing some utilies and several new Parsers. 

This is where I was introduced to ```*>``` and ```<*``` and the concept of lifting in functional programming (which I am still having a hard time fully understanding).

Described in the source for module ```Control.Applicative``` as:

```haskell
-- | Sequence actions, discarding the value of the first argument.
    (*>) :: f a -> f b -> f b
    (*>) = liftA2 (const id)
``` 
and 

```haskell
-- | Sequence actions, discarding the value of the second argument.
    (<*) :: f a -> f b -> f a
    (<*) = liftA2 const
```

Using some examples I worked out by hand:

```haskell
ghci> runParser (spaces *> posInt) " 345"
```

I understood this computation as first:

```haskell
ghci> runParser spaces " 345"
Just (" ", "345")
```
The ```" "```, the result, is disregarded. We pass on "345" to the next call:

```haskell
ghci> runParser posInt "345"
Just (345, "")
```

Since we are ignoring the result of ```runParser spaces " 345"```, the final result is: 

```haskell
Just (345, "")
```

Using the same inputs, but for ```<*``` this time:

```haskell
ghci> runParser (spaces <* posInt) " 345"
```

First we run:

```haskell
ghci> runParser spaces " 345"
Just (" ", "345")
```

This time, we *don't* disregard ```" "```.

We pass on "345":

```haskell
ghci> runParser posInt "345"
Just (345, "")
```

Here we are ignoring ```345```, the result of ```runParser posInt "345"```.

The final result ends up being:

```haskell
Just (" ", "")
```
Cool, how about one more.

```haskell
ghci> runParser (ident <* posInt) "hello 345"
```

```haskell
ghci> runParser ident "hello 345"
Just ("hello", " 345")
```

We keep ```"hello"``` and pass on ```" 345"```.

```haskell
ghci> runParser posInt " 345"
Nothing
```

Uh oh. We got ```Nothing```. There is no state for us to use in the return ```Maybe``` tuple, so we end up with ```Nothing```.

* ```posInt :: Parser Integer``` : Checks for positive integers in String input.
* ```spaces :: Parser String``` : Checks for spaces in String input.
* ```ident :: Parser String``` : an identiﬁer can be any nonempty sequence of letters and digits, except that it may not start with a digit.

I got this far in my understanding of these functions, but I still do not quite understand what is being "lifted" behind the scenes.

Lifting in the case of ```(a -> b) -> f a -> f b``` is defined in LYaH as "a function that takes a function and returns a new function that's just like the old one, only it takes a functor as a parameter and returns a functor as the result." I will mull this over more tonight, and perhaps ask Alan or some alumni in Zulip tomorrow if I am still having a hard time understanding the concept.

For about 30 minutes, I worked through the first six problems of [99 Haskell Problems](http://www.haskell.org/haskellwiki/99_questions). It's been pretty fun to revist things I learned a while back now that I am getting wrapped up in the intricacies of Haskell. My brain feels like it is exploding all the time.

Learning Haskell has been challenging. It is definitely rewarding, but there are many times when I feel discouraged because I don't know when I will understand things like Applicative Functors like the back of my hand. I often feel afraid that I *won't* ever understand these things, but then I tell myself, what's the rush?
