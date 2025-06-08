---
layout: post
title: "Setting up Skills Workflow - Weekly Update #11"
date: 2025-06-07
excerpt: "Roslyn and Skills!"
categories: [GameDev,Project,Update]
pinned: false
---

# Hello!
Man, I really have to think about better quipy intros. I've stopped since someone told me they were cringe. Very rude by the way!<br><br>

I would like to preface this with the fact that I am a little scatterbrained today, so this post is a bit all over the place.<br><br>

Anywho, happy Pride Month! I've been hard at work on streamlining my workflow, and heavily debating my life choices. Before I get into that, I made a lot of progress onmy tool that I would love to share! Although, I don't remember where I left off ahaha.<br><br>

# Editing Skill Values
This step was pretty much identical to editing the Character's values. The parser looks for the "SkillValue" attribute, which looks a little like this:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_11/skillvalue.png" alt="">
</p>  <br><br>

The first parameter is the display name on the tool GUI, the second is the order of which that appears, the third is the type of data, and the fourth is the actual value. All of this is fairly helpful in displaying the values correctly, but not necessarily editing and updating them. You can see how it looks here:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_11/uiex.png" alt="">
</p>  <br><br>

It is very nice and helpful to be able to easily swap between skills and edit them. You may be asking now if the skills are character specific - as in every single skill is designed for a specific character in mind. Currently, this is true - but it doesn't have to be! These values we are editing are base values; they're going to be the same regardless of what character uses it. Character scaling comes into play in the GetInformation function call, which I will talk about later.<br><br>

# Creating Skills
A big feature that actually took the most time was dynamically creating the syntax trees when creating a new skill. If you never worked with ASTs, just know that they are very particular and repetitive with their syntax. It is much easier to just code the thing yourself than working with generating syntax trees!<br><br>

Regardless, I got a very neat generation script working that creates the syntax tree and then prints it! More specifically, it adds the skill if it exists, otherwise creates a new one:

<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_11/skill_creation.gif" alt="">
</p>  <br><br>


And that generates this file:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_11/skillgen.png" alt="">
</p>  <br><br>


Doing this was more tedius than difficult. The actual difficult part that I STILL haven't figured out is adding the skill to the registered skills list while keeping a pretty format! More specifically, it currently does this:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_11/returnrawr.png" alt="">
</p>  <br><br>


The stupid new line is not working! I've tried everything I could to fix it as well! Leading trivia, formatters, whitespace normalization. Nothing is working! In the end, I realized I'm a quitter, and just gave up.<br><br>

But at least it is better than what it was doing before:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_11/newrawr.png" alt="">
</p>  <br><br>


Which, by the way, was caused by me foolishly believing that the newline token would automatically insert a whitespace after it. Apparently, that was an OUTLANDISH assumption! (dw roslyn I still love you)<br><br>

# Project Planning
I'm not the best planner, so a lot of my engine code is very messy and quickly becoming a bit annoying to work with, especially as I start building syntax trees, but, alas, my hubris is my stubborness. I do, however, kind of want to go over what I'm finding, in case anyone is following along with me! <br><br>

## Fun Fact! I Do Not Engage With Communities
Like actually. I don't really engage with communities around things. C# communities, Gamedev communities, and where it has really been an issue is Monogame communities. To be quite frank, I have barely done any engagement with Monogame. If I'm unsure on how something works, I literally just look it up in Google and then read about it for a bit. <br><br>

Let me be clear, this is really not a good way of doing things!<br><br>

Recently, I have joined the Monogame discord and started lurking a bit. Lovely people, but I have realized a few things:<br>
\- Apparently Async is NOT good with XNA<br>
\- There are A LOT of libraries that do things I'm doing (I kinda knew this already)<br>
\- A lot of people are just way more cracked than me ;-;<br><br>

I'm not particularly bothered by these revelations, but I do want to make it clear that a lot of what I do is not top-of-the-line update-to-date stuff. I tend to just do things I think will work. I'm not one to particularly care about doing the best and easiest thing, but that is something you should note when reading through this. <br><br>

It also brought to light my decision to not do ECS. I'm seeing a lot of other developers implementing ECS and prefabs using JSON. It's impressive! However, I'm not convinced I need to use prefabs for my game. Certainly would be helpful for simulation-like games. I can see a desperate need for a prefab system in that way, but I'm quite unsure if it's worth it for an RPG - especially considering the tool I'm developing. I'm not a fan of using reflection (which seems required for an ECS Prefab system) due to unneccesarry performance costs. <br><br>

Anywho, sorry for the rambling! I figured some of you might be interested to hear my internal struggles. Hope y'all have a great week!<br><br>