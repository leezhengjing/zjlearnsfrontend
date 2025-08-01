---
layout: post
title: "the purpose behind this site"
date: 2025-08-02 01:38:00 +0800
categories: thoughts
--- 
I created this website with the intention to write in my own words the frontend concepts that I learn in my free time. For some context, the motivation behind this is due to my lack of knowledge regarding frontend development that I have come to realise in my current internship. 

### What motivated me?
It's been 6 weeks since I started my current internship at `GIC`, where I have been mainly working on the frontend using React and Typescript. It's an amazing company, the office facilities are great, and the engineers in my team are seriously impressive (I get to work with these guys!), and the pantry with their free drinks and snacks is my favourite place to visit when they restock at 2pm. 

### Sounds great, so what?
And then, it comes to work. I have felt the clear limits of being a heavy user of Copilot, not having the fundamental understanding of the programming language im working with, the tech stack, the patterns, the knowlege breath/depth, and I was humbled the very first day when it came to my first PR, where I did not even know what useEffect was doing (I completely got the cleanup functionality wrong, insisting that it had to be included outside any if blocks, pointing at the example code block). 

I'm not sure what was going through my supervisor's head at the time, but he simply told me to write some more test cases. In the process of doing so, I had to send him a very humbling message on Teams right after as I came to the realization that you did not have to put the cleanup code at the end of the useEffect block for it to work. (I mean, its called a cleanup, so you really only need it when you need to clean up something, like stale data or in the case of my PR, only in that if block when there was actually something to clean up T-T).

### And then there was more...
With that being the first week of intern, my confidence was shot, and any ticket I laid my hands on, would proceeded to get PR bombed and I found myself really questioning myself. Most of the work I did was just asking Copilot to do it, and in my brief review of its response, questions regarding the proposed solutions and alternative methods hardly crossed my mind.

In fact, I found myself not knowing what some lines of code were doing until my supervisor requested changes and asked what XXX code was doing in my PRs. In a short span of a month, I started wrestling back control of myself from chatgpt, and I would say now half the time where my tickets aren't trivial UI changes, I actually actively read documentation and find PR threads regarding the bugs I was facing when upgrading dependencies and etc (might have to migrate to tanstack v5 in the future too as our last unmet peer dep). 

I would say I actually improved quite a bit in this regard, of not just being a mindless copilot coder, and I could comfortably answer more of my supervisor questions in the PR, providing links and discussion threads to show that I did do my homework and explaining the changes I made. (thank you supervisor for waking me up from my LLM drunken stupor).

### The final straw

In the most recent meeting (literally the same day that I'm writing this), we had a design discussion for our project, ChatGIC, going forward regarding how we wanted to best handle the new extensions and agents that would have to be incorporated into our chat functionality, which was using SSEs. Our tech lead in charge started off the agenda going through the existing codebase and introducing very briefly rxjs to us, which introduced the Observable object. 

What seemed to be very basic patterns like Observer and Reducer patterns to him, to me was complete gibberish. I was writing down in a vim editor all the things he was explaining, so that I can go back home and watch some youtube videos and explanations regarding all the stuff that were thrown around. It was not a very productive discussion, and more of a lecture by him who clearly realized we were not on his level, when he was just like "Are yall aware of the Observer pattern?" and im just like nope.

I felt like ass, especially after I spent the whole day debugging why upgrading our authentication library by 3 major versions to the latest ver didnt break authnetication but broke user data retrieval (found a github thread and implemented a fix, administered by AI still but without my input of finding the actual bug from console logging and scouring the internet it would not have been so fast, but i literally spent like the whole day from 930 am to 330pm on this, then had to go for the meeting unprepared).

### Resolutions
And so came the birth of this website, as I strive to not be caught lacking in meetings again, hoping to skill myself up by the midpoint of this internship to be able to better contribute as a frontend developer intern :D. Its my belief that if I can explain things clearly in my own words, it would mean that I have a better grasp of the topic and concepts that I am learning/working with, and a good engineer should be one that can translate their knowledge clearly and communicate it to others. And so I'll be writing a few blog posts regarding some frontend courses I'll be learning on the side, and also putting in some code examples that I feel are relevant to the things i'm learning :D.


### Ground rules
- I will not use AI to help me in writing any of the blog posts.
- I will use vim on my personal laptop to write these blog posts in markdown.
- I will not just copy the learning materials that I study and paste it here, it has to be built from my own words and understanding.
- No promises on the consistency of posts, I also hope this does not become a dead repo. Many months to come in this internship, hopefully when I get better I could host a lunch and learn :).
