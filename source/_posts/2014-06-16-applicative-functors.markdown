---
layout: post
title: "Applicative Functors"
date: 2014-06-16 17:02:53 -0400
comments: true
categories: 
---

Today at Hacker School, I was studying functors and applicative functors in Haskell. Functors are structures that "can be mapped over" [1]. So, applicative functors are functors that allow functions to be applied *within* a functor. Functor-ception.

This concept proved to be a pretty difficult one for me to grasp today. I wrangled with it for several hours, reading and re-reading Learn You a Haskell's [explanation](http://learnyouahaskell.com/functors-applicative-functors-and-monoids) for them before I broke down and asked for help on the Haskell Zuplip thread.

The particular problem I was sweating over was writing an Applicative instance for a ```Parser```:

```haskell
newtype Parser a = Parser { runParser :: String -> Maybe (a, String) }
```

I was eventually able to come up with this:

```haskell
instance Applicative Parser where
    pure x = Parser $ \s -> Just (x, s)
    p <*> q = Parser $ \s ->
            case (runParser p s) of 
                Nothing -> Nothing
                Just (f, s') -> case (runParser q s') of
                    Nothing -> Nothing
                    Just (x, s'') -> Just (f x, s'')
```

To be continued -- going to sleep now.

Resources <br/>
[1] [Haskell/Applicative Functors](http://en.wikibooks.org/wiki/Haskell/Applicative_Functors)