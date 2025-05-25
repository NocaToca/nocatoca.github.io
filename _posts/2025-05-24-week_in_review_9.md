---
layout: post
title: "Charge - Weekly Update #9"
date: 2025-05-24
excerpt: "Charge and Threats"
categories: [GameDev,Project,Update]
pinned: false
---
# Happy Memorial Day!
At least, to those of you in the U.S! Well, it isn't memorial day yet but it is memorial day weekend. I've been super busy this week - I didn't even have time to practice for lessons that I pay for! And no, it wasn't business relating to my game, unfortunately. If you havent noticed, my projectts and about me section is now filled out on my website! I spent the first half of the week doing that, then the rest doing more menial stuff. Like, I made a spreedsheet for finances. How lame is that?? I also have been working on a game jam. One of my friends wanted to participate in thatonegamecompany's game jam, so I've also been working on that. Hopefully that goes well. I don't have the best experience with jams.<br><br>

Anywho, I doubt that's what you came here for! Yes yes, my game. I did actually do quite a lot of work - in fact I did finish my goals for my prototype combat system! It's actually working really nicely for the spaghetti code that it is. <br><br>

# Charge!
The first main thing that was completed was the charge meter. You can see the new resources bars in action here (also wow! I really didn't have images or gifs in the last post?):
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_9/charge.png" alt="">
</p>  <br><br>

I'm still not sure if I want charge to be independent or team-wide. I'm going to test it out as independent first and see if it's more fun team-wide. Although, it will always be independent for AI. Regardless there are three main ways to gain charge:<br>
\- On turn start<br>
\- Dealing damage<br>
\- Taking damage<br><br>

Charge is useful for many reasons, the big one that actually isn't implement yet are turn breaks. Why haven't I implemented turn breaks you may ask? Well, the simple reason is that I didn't put it in the to-do so it doesn't exist. The excuse I am going to say is that I want to save it for later when I have a better idea of how the UI looks and how turn breaks will actually be incoorperated. <br><br>

# Skill Modifications
However, you can modify your skills' power and cast time with charge. Increasing charge increases the power but increases the speed penalty. Decreasing charge decreases the power but decreases the speed penalty. You can see how it affects the timeline here:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_9/basic_charge.gif" alt="">
</p>  <br><br>

If you remember from [the third weekly post](https://noellva.blog/gamedev/project/update/2025/04/12/week_in_review_3/), you'd know that ephemeral turns operate with modifications in a special way. That is, while they affect the cast time of the casting skill, they don't offset the cast of the next turn. You can see this working with Alata (since all of her skills are ephemeral):
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_9/ephemeral_charge.gif" alt="">
</p>  <br><br>

The main difficult thing about this whole process was that I implemented skills SO poorly. I refactered it when working with this system, but I had to iterate through each skill (I think theres about 18 of them) each time I changed something. I cannot tell you how irritating that was! Luckily, I made it so I really only need to change one class when changing something about skills as a whole, but geez! You'd think someone like me would have planned better than this!<br><br>

# Threat Detection
The last thing I did this week was highlight threats to the character that is currently focused. You can see how that works here:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_9/threat.gif" alt="">
</p>  <br><br>

I'll agree that it's kind of ugly, but at least it works! The main part of the threat detection (aka finding the threat range) was already implemented. You can see that in the targeting section of the [seventh week](https://noellva.blog/gamedev/project/update/2025/05/11/week_in_review_7/). All it does is pull from that then lerps through a highlight color and the draw color of the enemy. It's quite simple! In fact, most of what I did this week was simple :sob:<br><br>

# Well, What Now? Turnbreaks?
Well, you'd think! There's a lot more to do, so I'm not worried about finding something to occupy my time with. The general plan is that I will make the components to the game like little puzzle pieces and plug them all together. While they aren't totally independent, like I'm treating the enviornment and combat as seperate systems but they do interact, it is mainly to help break the project up into multiple smaller scoped projects. There are additionally other systems that are used pretty much consistently throughout multiple of these modules - these are the engine systems that I will create as I go. Particularly for combat, this was the UI system and the stub I created for the scene system!<br><br>

I did also mention that I wanted to do tooling. This is actually my next immediate goal. This includes three tools, which one is actually involving the next module I want to finish - the scene module! Overall, the three tools though are:<br>
\- Character Tool (Create characters, register/create skills, set up stats)<br>
\- Animation Tool <br>
\- Scene Tool<br><br>

I suspect the animation tool will be the hardest to make. I'll have to figure all of that out over the course of this week though. I'm going to work on them all in parallel, but will probably try and finish up the character tool first.<br><br>

Additionally, I do also want to restructure the current combat module! We will see what I need to do this, but I will probably work on that. For instance, I really don't like how I made my turn queue handle most of the canvas interaction ;-;<br><br>