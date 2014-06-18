---
layout: post
title: "Hacker School: Day 6"
date: 2014-06-17 17:09:44 -0400
comments: true
categories: [Hacker School, Python, Flask, Redis, URL Shortener, Haskell]
---

Today, I decided to take a mini break from Haskell (erm, I still did a wee bit of Haskell) and work on a one off project. I got in a bit early, around 9:30 am to finish up the [Applicative Functors](http://blog.dariajung.com/blog/2014/06/16/applicative-functors/) blog post. I was pretty impressed with how many Hacker Schoolers were already in at that point, and felt eager to start working. 

The little bit of Haskell I did today was to implement an ```Alternative``` instance for a ```Parser```.

If we remember from my previous blogpost, ```Parser``` is defined as such:

```haskell 
newtype Parser a = Parser { runParser :: String -> Maybe (a, String) }
```

The ```Applicative Parser``` instance is useful for making parsers of fixed and simple formats. Because we want to be able to handle
the concept of *choice*, we turn to the ```Alternative``` class.

The ```Alternative``` class is defined something like this:

```haskell
class Applicative f => Alternative f where
    empty :: f a
    (<|>) :: f a -> f a -> f a
```

(<|>) denotes a choice, so something like ```p <|> q``` means a choice between ```p``` or ```q```.

So, my ```Alternative``` instance ended up being:

```haskell
instance Alternative Parser where
    empty = Parser $ const Nothing
    p <|> q = Parser $ \s -> runParser p s <|> runParser q s
```

An important hint here is that there is already an Alternative instance for Maybe:

```haskell
instance Alternative Maybe where
    empty = Nothing
    Nothing <|> p = p
    Just x <|> _ = Just x
```

This means that we can simply call ```runParser p s``` and ```runParser q s```, which gives us Maybe tuples. We can then use (<|>) from the ```Alternative``` instance of ```Maybe``` to choose between those two tuples and pass it to the Parser constructor.

If ```runParser p s``` succeeds, return its results, else try ```runParser q s```. If that succeeds, return its results. Otherwise, a ```Nothing``` will be returned.

Pretty nifty!

The rest of today, I worked on a very simple [URL shortener](https://github.com/dariajung/url_shortener). 

I found a tutorial online that used the md5 hashing algorithm and a base 64 encoding to generate a randomized string. The last five characters of this were taken, sanitized, and then used as the key for a key value store in Redis as well as a slug. 

I whipped up a simple Flask app for 301 redirects from the shortened URL to the original URL. A quick lookup in Redis, and then a ```return redirect(location, 301)``` call did the trick. 

```http://blog.dariajung.com``` results in ```http://localhost:5000/iJp4fHs```. When I go to that URL, I am then redirected to my original URL.

The functionality is all very simple, so I don't check that the protocol identifier and such are in the URL. That might be for another day.

Overall, I think today was rather productive! 
