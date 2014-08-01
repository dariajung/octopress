---
layout: post
title: "Gayle Laakman McDowell Talk Recap"
date: 2014-08-01 14:32:53 -0400
comments: true
categories: [Gayle Laakman McDowell, Interview, Jobs]
---

On Wednesday evening, a couple of us headed to a talk by Gayle Laakman McDowell, the author of _Cracking the Coding Interview_.

She gave us some redundant information, but also some great insights that I had never thought about before.

First some things before the ~technical~ aspect of the interivew:

- Try to keep your resume to one page because most resume readers spend maybe 5 - 15 seconds looking at it. There are no fast and hard rules for how it should be formatted, but it should be scannable in that amount of time.
- Put your outside of school/work projects on your resume! Many candidates don't put their projects on their resume for whatever reason.
- Ask your recruiter what to expect from the interview. There is no reason to be afraid to ask about what you might encounter. However, take this with a grain of salt because the recruiter isn't going to be the one interviewing you.
- Coming off a bit weird to a recruiter is okay. As long as you aren't being as asshole, don't worry too much.

Other pre-interview stuff to know: 

- Struggling during an interview is _normal_. The whole point is to see how you reason through difficult questions.
- How you do is relative to people who are asked the **same** question. (This in particular was something that made so much sense, but was something I had never realized. I always quantified my success by how many questions I got correct.)
- Hashtables go a long way.
- Know linked lists, arrays, arraylists, binary search trees, merge sort, and quicksort well.
- Know Big O like the back of your hand.
- Try to recode data structures from scratch.
- Write code on paper so you don't freak out when you have to white board and don't have nice things like syntax highlighting.

During the interview:

- LISTEN for the little details. If you're given a list, is it sorted already? Are the elements distinct? Repeat the question back to make sure you understood it.
- Work through the question using a _good_ example.

But what is a good example? Let's work with this question Gayle gave us:

> Given two sorted arrays, compute the intersection.

What about: 
```haskell
[1, 5, 9, 15]
[2, 3, 9, 20]
```

This is bad because this is a special case, in several ways. The two arrays are the same length, and the element that appears in both arrays are in the same index. These are also too small.

In general, try to come up with examples that avoid special cases, and are about 50% larger than your initial instinct. So if you think about three element arrays, try working with six element arrays.

Brute force a solution first; you can optimize it later but it's better to have a solution to work with. Walk through the brute force solution using your example. Remember the small details when implementing your algorithm, ie: is the input sorted? is the information cached? etc.

The brute force approach to solving this is go through the elements of the first array, and check all elements of the second array to see if they match. Move onto the next element in the first array and do the same thing. Keep doing this until you've gone through the entire first array.

After this, try to imagine what the fastest you can imagine an algorithm being for the problem you have been given. She called this the best conceivable runtime. Was your solution O(nlogn)? Can you see it being solved in linear time? Try to get there.

Let's go back to the example question and see how we can optimize it.

```haskell
[1, 5, 6, 8, 9, 15]
[2, 3, 4, 5, 9, 20, 31, 33, 34]
```

You will have to go through every element in the first array, but not for the second. Why? Well, we know these arrays are sorted. So if we're looking to see if 1 is in both arrays, we look at 1 in the first, but we hit a 2 in the second. Since these are sorted, anything after 2 is going to be greater than 2. We can stop looking here.

Think about spacetime trade offs. Also always keep in mind hashtables because apparently they can be used to solve a lot of algorithms questions in optimal ways. This particular problem can be solved using a hashtable. I have solved it in Python [here](https://github.com/dariajung/interview-prep/blob/master/data_structures_algos/arrayintersect.py).

Some whiteboarding tips:

- Code far top left corner.
- Write small and straight.
- _If_ it helps, write pseudocode. But don't write psuedocode that uses syntax that looks too much like a programming language's because it'll just look like shitty code.

Code breadth first:

- Modularize from the very beginning.
- Go level by level, top down.
- Hit the most interesting thing first, then move down. 
- You're most likely to screw up on something like shifting bits around, but that isn't very interesting, so just save it for last.
Interviewers will not care if you messed up on something like that if you got the bigger picture correct.

If you're ever confused, stop, and recoup. Don't push through when confused. Walk through your example again.

When you're done writing your algorithm, test your code with an example, but NOT the example you used to understand the question. Good examples are long but not necessarily good test cases. Go with something shorter so if you hit a bug, you'll hit the bug faster. Start with small general test cases, then go to special cases.

Look at your code for interesting lines; what lines are most probable for errors?

After this, follow up with your recruiter!

Also, always keep in mind that interviewers are people too, and they all have varying personalities. If one is being really quiet, that doesn't mean you aren't doing well. Sometimes interviewers act harsher if you are doing well! What. They don't think you need their help and they're thinking about ways to push you.

Cool. Once you get an offer, negotiate, because it's a win-win. 30 minutes isn't a lot, but hey, you might get a couple thousand dollars out of it. Counter offer their offer by bumping it up $20k. They'll probably throw you a bone and meet you in the middle.

Obviously Gayle's advice should also be taken with a grain of salt.