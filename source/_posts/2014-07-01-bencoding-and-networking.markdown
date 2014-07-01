---
layout: post
title: "Bencoding and Networking"
date: 2014-07-01 10:15:49 -0400
comments: true
categories: [Hacker School, Haskell, Bencoding, Networking]
---

One of the things that I have always been fearful of is networking. Sockets, TCP/IP, and forking, all of that. In a class at university, I had done some networking in C; I remember reading [Beej's guide to network programming](http://beej.us/guide/bgnet/), and I found myself returning to it, and appreciating it a bit more this time. It's funny how when you're learning something in school, you could care less about it. You just want to get from point A to point B in the shortest way possible. But when you have the time to be in a self-directed environment like Hacker School, you find yourself wanting to revisit things that you didn't learn properly the first time around, wanting to tell your past self: "You should have paid more attention when you were learning this!"

So, to learn networking in Haskell, I have decided to incrementally work towards building a simple Bittorrent client. Yesterday, I read about [bencode](http://en.wikipedia.org/wiki/Bencode), the encoding used by the Bittorrent protocol for torrent files (metadata).

Bencode supports four types of values:

- Integers
- (Byte) Strings
- Lists
- Dictionaries (Hash Maps)

Integers are encoded as ```i<integer encoded in base 10 ASCII>e```. Integers can be negative, but 0 cannot be -0.

ByteStrings are encoded as ```<length>:<contents>```. So "foo" would be encoded as 3:foo. The length of the content can be 0, but cannot be negative. 

Lists are encoded as ```l<contents>e```. Contents are bencoded elements of the list (in order), and are concatenated. Something like "cat31" would be encoded as l3:cati31ee.

Dictionaries are encoded as ```d<contents>e```. The keys must be bytestrings, and the dictionary is ordered lexiographically by key. The encoded key value pair follow each other immediately. {"cat": "meow", "dog": 44} would be encoded as d3:cat4:meow3:dogi44ee.

After reading this, I used the [Parsec](http://www.haskell.org/haskellwiki/Parsec) library and wrote a parser for bencoded values in Haskell. I tested it on a torrent for Ubuntu and got back this:

!["Metadata"](/images/torrent.png)

We can see things like:

- "announce": "http://torrent.ubuntu.com:6969/announce"
- "announce-list": "http://torrent.ubuntu.com:6969/announce", "http://ipv6.torrent.ubuntu.com:6969/announce"
- "comment": "Ubuntu CD releases.ubuntu.com"
- "creation date": 1391706680

and so on.

The crazy wall of text is mostly due to all of the pieces for this particular torrent.

After this, to get a better sense of networking in Haskell, I read up on TCP/IP and started working towards this [tutorial](http://www.haskell.org/haskellwiki/Implement_a_chat_server) on building a multi-threaded chat server in Haskell, and getting a feel for the Network.Socket library. 

At the very basic level: Socket -> Bind -> Listen -> Accept.

My networking journey will continue today...
