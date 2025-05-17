---
layout: post
title: "Silly AI - Weekly Update #7"
date: 2025-05-11
excerpt: "AI systems! GOAP FTW!"
categories: [GameDev,Project,Update]
pinned: false
---

# Heya friends!
To be perfectly honest, I have been a bit low on steam this week, so this weekly log will probably be not as fleshed out or as fun as the others. That isnt to say I didn't do much, but just that Im lazy and didn't really want to write this out. In fact, Im writing this out while on a train to DC (EW!) since I dont have much else to do! <br><br>

Also happy Mothers Day! God knows someday Ill be able to celebrate it for myself (sobbing). <br><br><br>

# AI! AI!

Anywho, the main thing I did this week was creating my fabulous AI. You can see them performing their silly little actions here: <br>
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_7/ai_example.gif" alt="">
</p>  <br><br>

I honestly thought that the AI would take longer to implement. When I did Behavior Trees for another game they took almost a month, and the framework was arguably a lot more simple. But! The framework took me all of 4 hours - with the hardest thing being making the whole thing operate asynchronously so it wouldnt stall the main drawing and processing thread. <br><br>

I wish I could explain how I made it asynchronous and everything, but my experience with asynchronous stuff is throwing together a bunch of random stuff and praying to god it works well. Still, the main idea is that when the AI detects that it's its turn (its its! English is such a weird language), it passes itself off to a static AI controller class. This class uses a TaskCompletionSource that fires once the AI Agent finishes its turn. Everything after registering this source is handled asynchronously.<br><br>

Well, how exactly is this mythical AI implemented? It's not behavior trees, its actually GOAP (goo-ap. Pronounce it right!) <br><br>

GOAP, which is goal-oriented action planning, is a pretty nifty AI system that basically boils down to a few things. First, the AI has a set of beliefs about the world state. This can be things it knows for certain, like if it has a basic action or not. It can also be things it is assuming, like where a player that is outside its vision range is. The AI basically takes a snapshot of its beliefs and passes them into its Agent, which, importantly, is not the actual controller! <br><br>
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_7/beliefs.png" alt="">
</p>  <br><br>

Now, the AI also has a set of actions it can do. These actions range from moving to using a skill. Actions are defined by a set of required beliefs the AI needs to know are true or false to use the action (like, if the action is swinging a sword, you need to know that holding_sword=true!), a set of beliefs the AI will beliefs change due to the action, and the cost of the action. It is extremely important to note that the set if believes that the AI will believe come true are not guaranteed to come true. For instance, the “MoveTowardsPlayer” belief has that “player_in_range=true” as its believed outcome of the action. This is not guaranteed, because the player might be too far for the AI to get in range during its turn!  <br><br>

<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_7/actions.png" alt="">
</p>  <br><br>

In fact, this is really useful for repeating actions. For instance, there is an “Idle” function that has the belief that it will set the state “nothing” to true, but it doesn't actually do anything. <br><br>

Why does this matter? Well, the last piece I haven't mentioned are the Goals. Goals have a set of beliefs that it wants to be true or false and a priority. For instance, if the goal was to attack the player, the AI would want the aforementioned “player_in_range” belief to be true! For our aforementioned Idle action, it has a related Idle goal which wants nothing to be true. <br><br>

<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_7/goal.png" alt="">
</p>  <br><br>

This goes into our planning phase, where the Agent chooses a goal based on priority, aggregates all the actions, and tries to devise an action plan to turn the set of beliefs it currently has into the set of beliefs it needs to obtain this goal. This algorithm is probably the most complicated part of the whole thing, but its still really not that bad! Im using BFS through a priority queue as you can see here:<br><br>

<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_7/plan_function.png" alt="">
</p>  <br><br>

Now, once it has its plan and list of actions, the AI will go and execute that plan. If it cant find a plan to execute or fails its execution immediately, it defaults to idling. <br><br>

<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_7/plan.png" alt="">
</p>  <br><br>


This is all done asynchronously! <br><br><br>

# Targeting!

Another interesting thing that I implemented was the AI targeting logic. There are a good amount of enemies for it to target (a whole 4!), but for it to be smart, it cant really just choose the closest one or, even worse, one randomly. To resolve this, they choose a target based on the targets Focus Level. It devices this by (at the moment at least): <br>
\- The distance away the character is <br>
\- The health the character is at <br>
\- The inherent threat level of the character <br>
\- The realized threat level of the character <br><br>

The difference between the inherent and realized threat level of the character is that each character has an inherent threat score based off of what the AI thinks the character is capable of. At the moment, Eclara has the highest threat score followed by Alata. The realized threat level is determined by how much damage a specific character has dealt to not only the AI (although, that's the main weight), but how much damage the character has done to its friends. It also takes into account who is healing the enemy. <br><br>

Im planning to determine the character's inherent threat level to be weighting by the AIs own role. So, tank shredders will actually target the tank instead of trying to kill the healer, but that's a worry for future me! <br><br>

# Characters - Again!
When I said I finished my characters, I was lying. A big fibber (okay, to be fair to me, I implemented what I could at the time). I went back and implemented passives and focused on finishing up Lyscander. He has his fun Wane resource that made implementing his skills a little more than annoying. <br><br>

The main premise is that when anyone uses a skill around them, he absorbs that energy to charge his wane. This meant that I had to listen to each action used, then have him react to it. This is all well and good, but I had no idea where to put this event so that he could subscribe to it. The scene? The combat manager? In characters? <br><br>

I ended up just putting it in the combat manager. The main problem with this is that I had to reroute the on action use for characters to call this event. The thing was, actions aren't called through an easy “use action” button, theyre called by an action class which the character knows very little about (just what actions it has). So it was a bit of trouble, but I had to rework a lot of that logic in order for Lyscander to listen to that stuff. <br><br>

# Future Stuff!

That was the gist of this week! Im debating putting monthly videos on YouTube (idk if I've mentioned this before) but I had my voice too much to edit it. Such are the woes of self hatred! Regardless, I might do that this coming week if I have time. The week I just went over was really busy for me, surprisingly. I did things everyday but Friday! <br><br>

My current idea for next week is to just finish up characters then create charge - then it'll be fine tuning the AI and implementing turn breaks. 

