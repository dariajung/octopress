---
layout: post
title: "Applicative Functors"
date: 2014-06-16 17:02:53 -0400
comments: true
categories: 
---

Today at Hacker School, I was studying functors and applicative functors in Haskell. Functors are structures that "can be mapped over" [1]. So, applicative functors are functors that allow functions to be applied *within* a functor. Functor-ception.

This concept proved to be a pretty difficult one for me to grasp today. I wrangled with it for several hours, reading and re-reading Learn You a Haskell's [explanation](http://learnyouahaskell.com/functors-applicative-functors-and-monoids) for them before I broke down and asked for help on the Haskell Zuplip thread. (Now I know that I should ask for help if I can't figure something out in 15 minutes on my own.)

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

Applicative instances have a ```pure``` method and a ```<*>``` method. ```Pure``` is simple enough. It has a type declaration of ```pure :: a -> f a```. Basically, it takes a value of any type, and returns that value wrapped in an applicative functor. Where I had trouble was implementing ```<*>```. ```<*>``` has a type declaration of ```f (a -> b) -> f a -> f b```. Basically, it is like ```fmap```, but it takes a functor with a function in it, and another functor. The function from the first functor is sort of mapped over the value in the second functor.

Chen, Hacker School W '13, was a saint and guided me in grasping the intuition behind writing this applicative instance. ```P``` and ```q``` are both functors here. ```P```, however, is the functor that holds a function within it. In order to apply this function to the second functor, he was able to explain to me that I needed to "unwrap" the each functor and pass each state on to the subsequent action. In this case, that would be to call ```runParser``` on the functor ```p``` and the first state ```s```, which would return a type of ```Maybe ((a->b), String)```. This is where the cases come in. The result of ```runparser p s``` could either be ```Nothing``` or ```Just (f, s')```, where ```f``` is of type declaration ```(a->b)``` and ```s'``` is the second state. In the case of ```Nothing```, we return ```Nothing``` because there is nothing to pass on to the second functor. On the other hand, we again run ```runParser``` to "unwrap" the second functor. Just as before, in the case of ```Nothing```, we return ```Nothing```. Otherwise, we get ```Just (x, s'')```, where ```x``` is of type ```a``` and ```s''``` is the third state. With this, we can now apply ```f``` on ```x``` to go from something of type ```a``` to type ```b```, and return the third state ```s''```, resulting in ```Just (f x, s'')```.

Whew. I definitely learned a ton doing this. I hope my explaination made sense! 

Resources <br/>
[1] [Haskell/Applicative Functors](http://en.wikibooks.org/wiki/Haskell/Applicative_Functors)