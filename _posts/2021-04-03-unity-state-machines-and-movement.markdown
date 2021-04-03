---
layout: post
title:  "Unity State Machines and Movement?"
date:   2021-04-03
categories: [tutorial]
tags: [unity, bolt]
---

{% include youtube.html id="lYgFfF9B2Qg" %}

We’ve all seen that first tutorial that gets you started with a character moving across the screen.  For a lot of people, it’s the first tutorial they follow and it’s what gets them hooked on game development.  That thrill of creating something and being able to interact with it.  It can be intoxicating.  I believe the first tutorial of that type I followed was in an old book called, “Beginning DirectX 9” by Wendy Jones.  I think it had me moving an animated lion across the screen, wrapping around at the edges.  I was in my first year of college at the time and it blew my mind.  I’d only been programming for a couple of weeks and this felt like _magic_.

However, even at the time, I realized I had a problem.  If I held down both the left and right movement buttons at the same time, that little character would simply stop in place.  I knew it was an issue, but I had no idea how to solve it.  I figured I’d eventually figure out how to solve it, surely the book would teach me?  It didn’t.  In 2004, there weren’t nearly as many resources on game development that were freely available.  It wasn’t for another year, while studying game AI, that I first ran into the topic known as “Finite State Machines.”  I eventually stumbled into the idea that FSM’s might be useful outside of game AI.  That was a big epiphany moment for me.  I quickly realized I was using FSM’s all over the place, they just weren’t formal and obvious state machines.  It’s one of those, “Aha!”, moments we all get when really trying to learn and master a discipline.  Plenty more followed.

Of course, character movement is a series of states.  Different input, such as pressing the left or right button, triggers transitions between those states.  I had my solution!  Finally!

It’s been almost two decades since I’ve followed that tutorial.  When transitioning into education, teaching game development, I have been watching all sorts of tutorials from oh so many amazing creators, to see just how people are learning game development these days.  There are so many tutorials for beginners, but there’s not a lot out there teaching the intermediate stuff.  There’s very few tutorials out there teaching concepts like state machines, and even fewer teaching how to apply them in practice.

You have no idea how much I’m looking forward to contributing to the learning ecosystem!  I hope this tutorial helps those who are just now walking the path I did, twenty years ago.

- [**Project Files**](https://github.com/brenttaylor/Unity-State-Machines-and-Movement) - You can find the Unity project to follow along with the video here.