---
layout: post
title: "Commitment - Weekly Update #1"
date: 2025-03-30
excerpt: "Information regarding my plans."
categories: [General,Personal,GameDev,Project]
pinned: true
---

# Wow!
It's been a while since I touched this site - and I swear it was not on purpose! I know at the moment I probably do not have a single viewer (not even my mom! How sad!), but this is important to me to start doing. A 
point of this site was to log and market what I do, for my (hopeful) eventual project releases. It was also meant as a tutorial base, but I have been finding that more difficult to do fully employeed. Unfortunately, I 
don't think I will get to that section OR the project section for a while. But do not fear! For I come with some fun news! I know, so exciting.<br>

I have forever had an issue with consistency, and part of that comes with another issue I have struggled with. My memory is worse than a gold-fish. I am not really being sarcastic; I can retain process and ideas (think like math concepts) very well, but when it comes to specifc operable systems (codebases, how to cook my spaghetti) my memory kind of fails me. I have found that this makes two main issues for me: I don't remember what I did and through a bit of a butterfly effect, don't have motivation to continue what I was doing. In terms of the first solution, I am using this as a journal for my current project I am doing.<br>

This is all to say that I am planning to give weekly updates about what I have been doing on this project. I have very little optimism for this being read by others, but I want it to serve as a journal for myself. <br><br>

## Well, What Is This Project?
Yes, I suppose that is important context! To give a brief overview:<br>

For the past 6 years or so, I have been on and off developer a game that is essentially a passion project. The world has aggregated greatly from that time - and I will get to it when I post updates regarding it - but a big issue has been that the actual game project has died around 4 times. It's not anyone else's fault but my own; I've only ever developed on the codebase myself with this. The actual reasons it has died have all been various, but I do believe I can overcome them.<br>

In fact, I'm at a point where I can pretty confidentally say that I probably will stick with what I'm doing! This is why I want to start on this step of journaling and blogging development.<br><br>

## But What Changed?
Usually, this question is probably not interesting to ask, but I want to since it shares my philosophy around game development and the current advice around it. A lot of videos and creators seek to provide advice to indie devs that care about money (which is not to say that it is wrong). A lot of indie developers are not priveledged like me and/or have to do this in order to live. I do think it's a bit of a heartbreaking situation to me. People are pouring their souls into products that they *need* to sell in order to pay rent. <br>

I remember my Game Design 3 professor asking what an "art game" is and me not really having a reasonalbe definition for it (side note: loved him!). I don't remember what I actually answered or what he said about it, but I do know that he essentially talked about how outlook on development mattered. <br>

This is all to say, I think people focus way too much on what they think should be done rather than what they want to do. While I'm aspiratious, I'm not naive. The scope of this project is pretty extrodenary, but I see no reason for that to stop me from working on it. I make something for 10 years and no one buys it? So what? That's essentially what my mindset has come to.<br><br>

## How About For The Now?
Well! I do want to give you a bit of an idea for what I will be sharing. At the moment, I am implementing the combat system first before doing anything else. My next few updates will be about this. However, I want to spend my initial time to go over why I chose Monogame and how exactly I am designing this project.<br><br>

### Why Monogame?
There's two main reasons for this:<br>
- I love C#<br>
- I fucking love C# <br>
Now I hear a lot of people asking: Why not use Godot? Why not use Unity?<br>
Again, I am two main reasons for this:<br>
- Unity sucks and I have to liscence when I don't even know how to do taxes<br>
- I hate Godot because it doesn't use ECS or event-based systems (at least intuitively)<br>
I don't want to diss anyone who uses these two engines - they're perfectly viable and I actually loved using Unity for my previous projects. My choice for Monogame just comes from my knowledge on building projects and systems. I was recommended Godex by a friend as well, but I was against it because it wasn't, at least to my knowledge, going to be reliably updated to be in line with Godot. <br>

My choice for Monogame wasn't immediate either. I did actually build a good portion in Unity, then swapped to Godot, but I didn't then swap to Monogame. I made the dumb decision to try and make it in C++ and use a Vulkan renderer. While I am not unfamiliar with getting Vulkan to work and behave on my system and GPU, I spent like a year and half building that graphics engine and starting to integrate game logic only to boot it on my linux laptop and realize literally EVERYTHING was broken. I cried so much I had to restart again, as I knew that making it portable was going to be way more hell than it was worth. <br>

That is when I landed on Monogame! I'm super excited to learn it and use it! It already has been a blast setting everything up. <br><br>

### So You're Using ECS
Nope! I love ECS, but I've realized what makes most sense to me are event-driven systems. While I'm still a bit ignorant to the downsides and upsides to either, I'm arciteching my project to basically be layers of events. It has proved to be very handy so far and, honestly, pretty followable. 