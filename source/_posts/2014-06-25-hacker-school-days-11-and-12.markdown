---
layout: post
title: "Hacker School: Days 11 &amp; 12"
date: 2014-06-25 20:36:12 -0400
comments: true
categories: [Hacker School, Python, Haskell, Zulip, bot]
---

I'm getting behind on my blogging, meep. 

Day 11 recap:

- Spent half of the day trying to debug my sudoku solver's board parser, which was pretty difficult as everything type checked, but I was getting the wrong output.
- Learned about the [GHCI interactive debugger](http://www.haskell.org/ghc/docs/latest/html/users_guide/ghci-debugger.html), which let me place break points and inspect variables where the execution of the program has stopped.
- Alan gave me a quick overview of "equational debugging", which is to test little snippets of your program and make sure that it is returning the right output.
- I ended up pulling out more complicated bits of my code into smaller functions to make equational debugging more manageable.
- Spent the rest of the day finishing up the sudoku solver. I debugged the constraint propagation aspect of the program, and then implemented the depth first search function which utilized the constraint propagation logic.

Day 12 (today!), I decided to take (another) break from Haskell. I played around for most of the day with Paper.js, trying to make something beautiful, but eventually found that it didn't actually interest me too much. Around 3:00 pm, Stacy from Winter 2013 batch came by Hacker School to do a goal making workshop. It did really get me thinking about my time at Hacker School, and how I need to figure out when I can say that I have achieved my goal of being literate in Haskell. I think I will spend maybe a couple more weeks max on Haskell, and then switch over to Python. My main fear is that while Haskell is awesome, it isn't exactly a language that I will be able to work in once I become a professional software engineer.

After hitting a dead end with Paper.js, I decided to pivot and play around with Python. I implemented a simple echo server in Python, where the client will send back what the server sent to it. Then I got the idea to work on a GIF bot for Zulip because sometimes emoji just aren't enough :). You can ask gif bot "gif me cats" and an API query is sent to [Giphy](http://giphy.com/), and gif bot returns a gif that has been tagged with cats, in this example. It's basically done at this point, and works locally, but I'm not sure what the protocol is for having a permanent presence from the bot. Do I serve it on AWS/Heroku? I think I will ask Allison tomorrow. I'm also curious if I should demo this tomorrow afternoon.

Here is gif bot in action:

!["Gif Bot in action"](/images/gifbot.png)