---
layout: post
title: "Hacker School Week 1"
date: 2014-06-15 18:20:07 -0400
comments: true
categories: 
---

!["HS Logo"](/images/hs_logo.png)

This past week was my first week at Hacker School, and I am finally getting around to setting up a blog!

I really haven't had much success with blogging in the past, so I am wondering how this is going to go, but I will try my best to write something everyday. The posts from my fellow batchmates have been very exciting to read, and have been a motivating factor for me to finally get Octopress set up.

Because I had already been working on a [course on Haskell](http://www.seas.upenn.edu/~cis194/lectures.html) that I found online before Hacker School started, that was mainly what I focused on during my first week. The course is broken up into 12 lectures, with corresponding homework assignments. The amazing thing is, I was able to work through about one week's worth of material *per day*. It's incredible what can happen when you are learning for the sake of learning, with no worries that generally come from a work or school setting. If you had told me one year ago that I would be geeking out over Haskell, I would have laughed in your face. I would have thought that it was too academic, too hard of a language for someone like myself to learn. What I am finding though, is that once I commited myself to learning Haskell, once I was comfortable with the idea that I *too* was capable of learning Haskell, I started to have fun with the assignments. 

The most recent assignment I worked on was with using the rose tree data structure from the ```Data.Tree``` library. Based on a tree of employees, where employees are given a name and a "fun" score, I was given the task of maximizing the fun score for a party and  returning its optimized guest list. The caveat is that if an employee's direct superior were also in attendance of the party, that employee wouldn't be able to have any fun, lowering their fun score to 0.  

I think my road block for this assignment was implementing a fold function for the ```tree``` data type (to which I could pass a function that found the max fun score at each subtree later). I wasn't sure what the type signature for the fold should have been, which took up the most of my time. Once I got this function worked out, I was able to work through the rest of the assignment.


I wrote the fold as such: 

```haskell
treeFold :: (a -> [b] -> b) -> Tree a -> b
treeFold f tree = f (rootLabel tree) (map (treeFold f) (subForest tree))
```

where ```tree``` is defined as 

```haskell
 data Tree a = Node {
    rootLabel :: a, -- label value
    subForest :: [Tree a] -- zero or more child trees
```

The ```rootLabel``` of the tree returns the element at that Node and then we map ```treeFold f``` to the subtrees of the Node, recursively calling ```treeFold f``` on the subtrees. These are then passed as parameters to the function ```f```.

---

Something else that I did last week was playing with Arduinos and Addressable LEDs (each pixel is individually programmable!). I bought an Arduino UNO a few years ago, and never had really done anything with it. Dana, a batchmate with lots of hardware experience, brought some addressable LEDs in for some of the Hacker Schoolers to play with. 

The cool thing was that Adafruit already had a library called [Adafruit NeoPixels](https://github.com/adafruit/Adafruit_NeoPixel) we could use, so we were able to just hook up the LEDs to the Arduino and we immediately saw a light show. 

!["HS Logo"](/images/led.jpg)

We played around with making the LEDs blink, which we achieved by Mod-ing the number of LEDs, and then changing the RGB value to (0, 0, 0). It definitely distilled the fear of hardware many of us had once we understood how easy it was to get started with it with all of the resources online. I am totally obsessed with Adafruit now!

My hardware project that I would like to accomplish this summer is a temperature sensor that based on the serial output changes the colors of the addressable LEDs. If warm, the LEDs light up yellow/orange, if cool, a green color, etc.

I am loving Hacker School thus far. Well, love is a bit of an understatement. 

