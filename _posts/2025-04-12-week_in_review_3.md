---
layout: post
title: "The Combat System - Weekly Update #3"
date: 2025-04-12
excerpt: "Explanation of the Combat System and Ephemeral turns"
categories: [GameDev,Project,Update]
pinned: false
---
# What Combat System?
Last week, I attached my to-do I had made in discord to the end of the post, and a lot of it I realize probably made no sense to you guys. Forgoing the characters (I'll explain them in seperate posts), I'm going to assume the term "ephemeral turns" was made no sense at all! Don't worry - I'm here to save the day and explain my super awesome combat system I am prototyping! I also hope that this will put things into light before I showcase what I did this week. <br><br><br>

## Basic Overview
The super short simple explanation of the combat system is that it is a Grid-Based Turn-Based Timeline-Based combat system (Wow! Three based type tags! Talk about buzzwords!). <br><br>

What this actually means is that the combat system is almost parallel to the older titles of the game series "The Legends of Heros" (or just Trails). If you have never heard of that series, think about the grid combat you'd do in a game like Fire Emblem - that is what the combat takes place in. Then it's turn based (Side note: what is with the push to real-time? Turn based games are so underratted (no bias)), so think of a game like Baldurs Gate 3 (I mean - FE also works). Finally, it's timeline-based too. While almost all of these games showcase a timeline so you can visualize the order, I say timeline based as in that order is not consistent in rotation like it would be in BG3. This more mirrors games like Ruined King, Digimon Cyber Sleuth, Pokemon Legends of Arceus, or what have you! <br><br>

This, however, is the high-level explanation of each system. There are tweaks to each of these systems to be unique in it's own way. We'll go in order, but it's convienent that the modifications get more complicated as we go on. <br><br><br>

### The Grid
I mentioned that the grid is like Fire Emblem, and overall this is true. However battlefields/grids have quite the modifications to them that pull from other games. The biggest thing is that there are (or at least going to be - lay off me!) a lot of environmental considerations. The major one is cover - which works a lot like XCOM's system. While this does not matter for our beautiful melee attackers, ranged attackers and spells will have reduced accuracy when aiming at enemies affected by cover. Like XCOM as well, there is full cover, which allows you to hide from line-of-sight damaging spells, and half-cover, which reduces accuracy and damage from range attacks and spells. <br><br>

Adding onto that, I'm planning on adding elevation. This may or may not happen (I'll have to see how the primitive AI handles it), but I would like this to add additional modifiers! <br><br>

Other than that, the grid can contain environmental hazards and aids, ranging from rivers to traps!<br><br><br>

### The Turns
Unlike most turn based games that give you one overall action per-turn (or multiple if you have items/spells/modifiers), actions are split into the following categories:<br>
\-On-Turn Actions <br>
&nbsp;	&nbsp;   \- Moving <br>
&nbsp;	&nbsp;   \- Basic Action <br>
&nbsp;	&nbsp;   \- Extra Action <br>
&nbsp;	&nbsp;   \- Follow Action <br>
\-Off Turn Actions <br>
&nbsp;	&nbsp;   \- Turn Break <br>
&nbsp;	&nbsp;   \- Reaction <br><br>

For the astute of you, you'd see that the the On Turn Actions and Reaction mirrors DnD/BG3. This is true! I love BG3 combat so I wanted initially to mirror it, without the Time-Line magic explained in the next section. I made quite a number of mechanics around that BG3 esque combat and I'm super excited to see how they mesh with the timeline aspect. For those of you familiar with Trails games, turn breaks are a lot like S-Breaks, so they interact directly with the timeline. Don't worry for those completely lost! I'll explain each of these actions. <br><br>

Moving is pretty self explanitory. This is your basic move action, which includes things like running, jumping, and what have you. There isn't much more to it. <br><br>

Basic Actions encompass the bread of each character's kit. This is not only their skills, but their main attacks, guards, and rests. Unlike BG3 and DnD, Basic Actions *do not* include simple actions like throwing and dashing. Basic Actions are always going to be combat related. <br><br>

Extra Actions are what may not be combat related. This includes actions like throwing and dashing. The main purpose for Extra Actions is to use items, like potions. If you use a firearm, you also use your Extra Action to reload (kinetic weapons) or cooldown (energy weapons). Extra Actions are probably the least used, as they can cost a lot of Timeline presence (better explained later). <br><br>

Follow Actions are probably unfamiliar. These can only be used immediately after a Base Action. These are normally skills but also include actions like a second attack if you are dual weilding (or Eclara). These are partically useful for Ephemeral turns, but otherwise are helpful to self-combo, burst, or keep combat momemtum. Still, they are extremely integral to characters. If Basic Actions are the bread of a kit, Follow Actions would consist of the butter. <br><br> 

Turn Breaks do exactly what they sound like they do. They rely on a resource called Charge, which acts a lot like Craft Points in Trails (I am NOT calling it Charge Points). Put quite simply, turn breaks disrupt the turn order to place you first on the timeline. This can be done during any turn so long as you have enough Charge (and some specific instances). <br><br>

Reactions are to allow your character to react to things that happen when it is not their turn. These act a lot like Reactions in DnD. <br><br><br>

### The Timeline
The timeline is the biggest part of the combat system! Basically, depending on how many (and what) actions you used during your On-Turn actions, you will either be place further up or further down on the timeline. This means that it probably isn't the best idea to exhaust every possible action every turn, as it makes you extremely slow. <br><br>

This isn't the only other consideration. The main difference is the existence of the elusive Ephemeral turns. These turns are specifically for certain spell casts that take a moment to cast (think of arts in Trails). What's special about these turns is that their turn order is absolute - they cannot be turn-broken. This doesn't *just* mean you can't break their turn during it, but turn breaks don't edit their turn projection. As a small example, say you have character a, b, and c in the order [a, b, c]. If c breaks a's turn, normally the timeline will be: [c, a, b]. However, if b's turn is Ephemeral, it will be: [b, c, a]. This is a double-edged sword, as it can aid your spell cast but it also makes it harder to react to enemy's spell casts. <br><br>

Additionally, a side-effect of charge is that you can change the power of a spell cast by using it. This acts a lot like the lanes in Ruined King; you can either reduce the power and cast it faster, cast the spell normally, or increase the power and take longer to cast the spell. It is helpful to note that the choice made here will not affect your recovery time (your placement of your next non-ephemeral turn). <br><br>

Finally, ephemeral turns also do not recover your turn actions, but you can take one extra action you havent made before ending an ephemeral turn (this is almost always going to be a Follow Action). Keeping in mind of what I said above, this is very helpful! It basically means that your follow actions *will not* put you farther down on the turn order, as your next turn (which is going to be non-ephemeral) cannot be moved by anything that happens during your ephemeral turn! <br><br>

A final consideration (that doesn't relate to ephemeral turns) is that Turn Breaks reset your actions and timeline. So if you know you're going to turn break, there's not much of a reason to not use all possible actions! <br><br><br>

# Now, Project Updates!
Wow! That was a long preface (maybe should have been it's own post). It's okay though, now we can get to what I accomplished this week (I hope you're proud of me!): <br>
\- Create more skills (particular cast time) <br>
&nbsp;	&nbsp;   \- Finish Eclara <br>
&nbsp;	&nbsp;   \- Create Alata <br>
\- Create ephemeral turns (and cast times!) <br>
\- Create turn projections <br><br>

Honestly, there isn't much to show since I am too lazy to make gifs, but I can talk about creating the turns and turn projections! <br><br><br>

## Turn Projections
Surprisingly, I did the turn projections first (I didn't come up with Alata's kit until Thursday which was why - so not surprising). This was actually A LOT more trouble I anticipated. Before I get into that though, you can look at what exactly the turn projections do here!:<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_3/projection_showcase.png" alt="Turn Projection">
</p>  <br><br>

You can see that when hovering or trying to use the skill, the turn order shifts to highlight what it'll be when/if you use said skill. It's a very simple concept, but I had a lot of trouble implementing it because of how my turn queue was behaving originally. <br><br>

The first issue I ran into was that my TurnQueue class created TimelineBars based solely on who was in the base priority queue. This is a bit of an issue, as the base priority queue is made to hold a single instance of any character, as it is solely meant to be used by the Combat Manager to know who's turn it currently is. <br><br>

Clearly, I had to restructure my class in someway. I didn't really want to change the uniqueness property of the main priority queue as I didn't want to introduce possible issues or edge cases (think about what would happen if a character gets a speed increase - you'd have to rebuild the whole queue which kinda sucks just to have it work for the display). In this way I made specific functions to handle creating the actual TimelineBars and have the TurnQueue not manage them but the actual CombatManager (I will probably move this to a CombatContext once I build more pieces of the UI). This works by basically taking the current speed variable of the TurnQueue and iterating through the characters to determine their predicted placement. This TurnQueue display is redrawn each time a new turn is started. <br><br>

Now, the issue when it came to trying to project only the character occurs due to the fact that we're projecting the turn order as a "what-if" when highlighting a skill. This meant that we had to forgo only redrawing the time-line on a new turn but to whenever we highlighted or chose to use a certain skill. This also meant that we needed to save that speed and modify the turn projections to use the updated speed (this is ALSO why I opted to make dummy priority queues). <br><br>

It wasn't even over yet. I had a bug where turn order was inconsistent. I had no idea why at first, then I realized that the queue was absolutely freaking out when two character's speeds were equal. Of course, I needed to make my own priority object. This wasn't too bad to do, but I had to add an "entity ID" to each IEntity in order to achieve this. This means that speed-ties are always broken by entity ID. I debated using something like "entered combat order", but I'd have to keep a dictionary to keep track of that, so I decided against it. I'm also imagining that the entity ID will come in use later. <br><br>

As a bit of an aside, since I didn't know much about C# priority queues, I asked ChatGPT what I needed in a TPriority. It gave me a helpful suggestion of adding an epsilon when that occurs. Thanks ChatGPT! (I hate generative AI) <br><Br> 

## Ephemeral Turns
Anywho, once I finished the turn projections, I had to make ephemeral turns. This was actually really easy. The character has a property call CastingSkill that it uses to cast ephemeral skills on turn start. Since I was already checking the character's team to draw the TimelineBar color, I simply added a check to see if that was null. Of course, I had to make sure it would only draw it once, but that's also pretty easy to do. <br><br>

At the moment, ephemeral turns are represented by being shorter than other turns. I don't really want this as a final UI decision, but it's helpful at the moment for prototyping. <br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_3/ephemeral_turn_showcase.png" alt="Ephemeral Turn">
</p>  <br><br>

The last thing would be that I made Alata's skills, but I'll save that for when I do a character post about her.

# What's Next!
If you remember my to-do list, I had quite a bit after: <br>
\-Create Highlighting follow actions <br>
\-Create simple animations (pull from RPG Maker animations for now) <br>
\-Create more complicated damage (can be done anytime really) <br>
\-Create final two characters that will be used in demo: <br>
&nbsp;	&nbsp;   \-Lattice <br>
&nbsp;	&nbsp;   \-Lyscander <br>
\-Create resources (mana/charge/wane) <br>
\-Create skill modification with charge <br>
\-Create basic AI to fight back! <br>
\-Threat indication <br><br>

You'd correctly assume that next week I'm going to do Highlighting follow actions, but I actually have to do something entirely different before even attempting that. <br><br>

I don't have a camera class. <br><br>

I unfortunately need a camera class. <br><br>

So that will be what I'm working on next week (sobbing). <br><br>

Here is that todo!: <br>
\-Add following a character <br>
\-Add camera panning <br>
\-Add zooming in and out <br>
\-Create focus changing <br><br>

Hopefully I can do all of that. <br><br>

Regardless, see y'all next week! Thanks so much for reading! <3