---
layout: post
title: "Hacker School: Day 8"
date: 2014-06-19 21:35:35 -0400
comments: true
categories: [Hacker School, Haskell, Hardware, Arduino, Firmata]
---

End of week two. Crazy!

This morning, I spent a bit of time pairing with Dana and Georgi on Arduino and hardware things. Dana introduced us to [Firmata](http://www.firmata.org/wiki/Main_Page), a protocol for interfacing with the Arduino in different programming languages (instead of using the Arduino language, C/C++, or Assembly). She gave us examples in Node.js using [Johnny Five](https://github.com/rwaldron/johnny-five) and Python using [PyFirmata](https://pypi.python.org/pypi/pyFirmata/0.9.5). I ended up playing around with the Python example and an Arduino that was set up with a potentiometer, an LED, and a servo motor. Depending on the value read from the petentiometer, the LED would blink at a different rate, and the servo would move to a different angle. 

After seeing how this worked, and looking through the spare hardware parts at Hacker School, we found a photocell, which senses the amount of light being received. I hooked up the photocell to the breadboard and Arduino using this [guide](https://learn.adafruit.com/photocells/using-a-photocell) from AdaFruit &#10084; and a little help from Dana, and now the LED and servo were reacting to the readings from the photocell.

!["PyFirmata + Arduino"](/images/firmata.jpg)

After playing around with this, I got an idea to use a temperature and humidity sensor for garden/plant health. The Arduino would gather data, and if your plants need a little love, it would trigger something that would text you (maybe using Twilio) to tend to them. I need to order the temperature/humidity sensor before I can get started but I think this would be a fun hack that encompasses hardware and web development.

Once the hardware workshop concluded, I went back to Haskell where I started reading about Monads (*eeep*). Actually, Monads so far haven't been that scary. Confusing, yes, but not scary. Just another level of complexity up from an Applicative Functor. In fact, all Monads are Applicative Functors. The distinguishing factor is that Monads have the (>>=), or *bind*, method in their definition. 

A Monad is defined as:

```haskell
class Monad m where
    (>>=) :: m a -> (a -> m b) -> m b
    (>>) :: m a -> m b -> m b
    return :: a -> m a
    fail :: String -> m a
```

From what I can understand, (>>=) basically lets you pass some value of a Monadic context to a function that expects a normal value, and outputs a Monadic value.

Something else that struck me was that the definition of (>>) seems exactly like the definition of (*>):

```haskell
(>>) :: Monad m => m a -> m b -> m b
(*>) :: Applicative f => f a -> f b -> f b
```

So cool. 

```(>>)``` and ```(*>)``` ignore the result of the first monadic value/applicative functor but __not__ their effects.

I ended up reading most of LYaH's [chapter](http://learnyouahaskell.com/a-fistful-of-monads) on Monads, and have gotten a better understanding of both applicative functors and monads. I still have lots of reading material left, so I will continue that tomorrow.

As today was Thursday, Hacker Schoolers demo'd projects that they had been working on. Many of the projects were interesting, challenging, and quite frankly, a bit intimidating. They ranged from maze/percolater solvers, to CPUs in Clojure, to letting you edit Jekyll blogs in the browser! I wondered to myself if I would ever be presenting at a demo session this summer. The thought did cross my mind that maybe I should give up on learning Haskell because it is getting incredibly difficult for me to process, and everyone else seemed to be much more productive with their time than I was. I don't know, I will think on this more.

Mihai's demo on creating music and outputting the result as MIDI files actually inspired me to search for something that would allow me to do that in Haskell. I was able to come across the [Euterpea](https://github.com/Euterpea/Euterpea) library, which looks very promising. I think it would be fun to create a Markov Chain that took training data of different songs, and created new compositions. I hope to play around with this some in the coming days.

To conclude the day, Marisa, Alex, Rachel, and I started watching a documentary on the font Helvetica. It was very interesting to see how Helvetica's usage has evolved over time, and also the connotations that it has to people. Going from a clean, revolutionary font to an overused "nameless" font (as it is now employed by many corporations and government agencies) has given Helvetica an interesting reputation. Some people see it as the font of wars (Vietnam, Iraq war), and some see it as the quintessential modern typeface; a debate between modernists and postmodernists.
