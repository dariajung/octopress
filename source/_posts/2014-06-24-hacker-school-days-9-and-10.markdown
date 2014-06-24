---
layout: post
title: "Hacker School: Days 9 &amp; 10"
date: 2014-06-24 09:58:30 -0400
comments: true
categories: [Hacker School, Haskell, Python]
---

I didn't get a chance to blog about last Friday (Day 9) so I'll do a quick recap:

- First day of interview prep.
- Worked on [Manage those Phonebooks](https://hackpad.com/Manage-those-phone-books-wK1MycZ5ATb) in Python.
- Turns out I had a lot of trouble parsing command line inputs, so I spent a good chunk of time on that before I decided to come back to it at the end.
- This exercise made me feel a bit uncomfortable about how well I know a language. I've been spending all of my time on Haskell and haven't touched Java or Python in a while.
- Continued reading about Monads.

Yesterday (Day 10), we received new check-in groups. It seems that they rotate every two weeks, and I'm enjoying that as it gives me the chance to interact with more of my fellow Hacker Schoolers in a smaller setting. 

I spent a good chunk of the morning finishing up the last assignment from Brent Yorgey's Haskell course programming a Risk, the <a href="https://en.wikipedia.org/wiki/Risk_(game)" target="_blank">boardgame</a>, simulator. It was cool to play around with Random generators to simulate die rolls, and also to simulate 1000 invasions (repeated calls to battle until there are no defenders remaining, or fewer than two attackers left) of varying defending and attacking army sizes. This was encompassed in a Battlefield data type, where Battlefield is defined as:

```haskell
type Army = Int

data Battlefield = Battlefield 
                   { attackers :: Army, defenders :: Army }
```

After this, I ended up stumbling on Peter Norvig's Sudoku solver [paper](http://norvig.com/sudoku.html) and decided to implement it in Haskell. I've been struggling through lots of type errors but I was surprised and happy to find that I got so engrossed in my task that I stayed at Hacker School for almost 12 hours yesterday. It's really neat to be this absorbed in something, and feeling myself gain more confidence through being challenged by my own curiosities. Once I finish this up, I will definitely be needing some code review.