---
layout: post
title: "Building a Cat Cam"
date: 2014-08-12 17:09:18 -0400
comments: true
categories: [Hacker School, Raspberry Pi, Hardware, Kitkat]
---

I recently purchased my first Raspberry Pi (the Model B+ whooho!)

!["PI"](/images/pi.jpg)

I decided that my first RaspPi project would be to build a Cat Cam to monitor Kitkat while I am away from the apartment. Occasionally he's being doing a few weird things like pooping outside of his litter box while I'm not home. Basically, this is me spying on my cat.

After a couple of component orders (PS3Eye webcam, MicroSD card) arrived, I was ready to start setting up my new Pi.

Dana lent me her serial cable so I could access the Pi without an external display. However, this meant that NOOBS wouldn't work (it seems to require an external display), and we had to mount Raspbian Wheezy onto the SD card. There are always bumps along the way to setting up new hardware... Soon after this though, I was able to SSH into the Pi, which was great!

But more complications followed... RaspPi is developed in the UK, so the locale was set to en-GB.UTF8. I had some problems figuring out how to get it to be en-US.UTF8 and was going crazy trying to figure it out, because I SWEAR I was selecting install new locales when I tried to generate and update them. (Lol, no I wasn't). Luckily, [Paul](https://www.hackerschool.com/residents#Paul-Tagliamonte) was able to help me troubleshoot and not pull my hair out.

Then, I was ready to set up the PS3Eye camera and motion detection snapshots using the motion package and following along with this [tutorial](http://chris.gg/2012/07/using-a-ps3-eyetoy-with-the-raspberry-pi/). The set up with the camera was incredibly straightforward, and things just worked! I was able to view the stream from within the local network of the Pi. But as it turned out, *only* the local network. When I excitely told Matt to view the stream (after I had pushed a simple Python-Flask app to Heroku), he told me that the stream was empty. 

Slightly deflated, I started looking around RaspPi forums and found out that my problem was because the RaspPis, as a default, only allow connections from a local network due to security reasons. Basically all of the suggestions pointed to enabling port forwarding, which seemed like a super insecure move, even for someone who has barely any knowledge of security practices. Basically, I would have to open up the Pi to the outside world so the stream could be viewable on the Internet. This meant that anyone could try to SSH into it; even if it has no sensitive information on it, I still don't want people in my Pi :/. 

(I took a break at this point to create a script that emailed my personal email account the IP address of the RaspPi every time it was booted to make it easy to SSH into it. Whoo!)

I wanted to avoid port forwarding if I could. I thought about it a bit, and last night, I remembered the awesome AWESOMENESS that is [ngrok](https://ngrok.com/). Ngrok creates a tunnel between localhost and the Internet. This totally solved my problem! So this morning, I played around with ngrok on the Pi, creating a tunnel that would allow the webcam feed to be viewable from the Internet, and used that in the Flask app feed source. To double check that this worked, I asked Matt to view it from Minnesota (he's on vacay visiting family). AND VICTORY, IT WORKS!

My next steps are to create a start script that runs the motion daemon, and a script to auto start ngrok. I have created a cronjob to delete the contents of a tmp file that takes a picture everytime the webcam detects motion (this can mean A LOT of pictures depending on where it is placed). At midnight every night, the script just deletes the day's worth of pictures, assuming that I will be able to look through them for any suspicious Kitkat behavior before the day is up.

I'm really excited to set this up at home and spy on my cat >:D Next, I want to build a toy component so I can play with Kitkat remotely. 
