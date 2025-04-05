---
layout: post
title: "Skills and UIs - Weekly Update #2"
date: 2025-04-04
excerpt: "The fun art of prototyping UI and UX"
categories: [GameDev,Project,Update]
pinned: false
---

# UI? How Fun!
I hate you if you think that (not really (really (not really))). <br><br>

It may come as a surprise to some, as I do sometimes say that I am a graphics programmer, but I am absolutely AWFUL at design. I know what colors mix and match but putting them together to make pretty images? It's way above my league! I really do respect artists for that - I genuinely think it is the most difficult and underappreciated aspect of Game Design. Any graphics programmer can just plug in ray tracing and make pretty lighting for whatever (not that it'll be good), but we'd be nothing without you artist and modelers. I am a great example of that. <br><br>

Now, before I go on a further tangent, I spent this week mostly implementing the UI for combat! I completed three main things on my to-do list:<br>
  \- Set up option buttons<br>
  \- Create skill UIs<br>
  \- Create health UIs<br><br>

While the end result does not look all that pretty, I am honestly happy with how it came out in the end! <br>
![Here's an overview](images/week_in_review_2/overview_showcase.png) <br><br>

## The Option Buttons
Now, now, I know everything does not look AAA game-ready - but I do have texture loading support. I'm only really focusing on functionality regardless, and I think these option menus are a great example of such. <br><br>

So, as a brief overview of my UI system, we have a general UI class that handles everything that that specific UI is rendering (at the moment, there's only ever one UI on the screen). At the start of this week, this UI class knew basically nothing about anything besides what it wants to draw. These were passed to the UI as classes that implemented event interfaces. If a class wanted to draw something, it would create a class that implemented the corresponding event (ITextureEvent, ITextEvent or both) and filled out what it wanted to be drawn, then send that information to the ui through UserInterface.ActivateEvent(IBaseEvent). For deletion, these events have an EventHandler called OnCompleted that the UserInterface listens to. When this event is invoked, boom! It deletes all the necessary resources detected during event activation! And if the class wanted to refresh it's draw infromation (say, it's a moving object across the screen), it would simply tell the original event to change the drawing rectangle!<br><br>

Hopefully that blurb was not confusing. Here! I'll use my excellent photoshop skills to give a little diagram: <br>
![Diagram!](images/week_in_review_2/option_ui_diagram_showcase.png) <br><br>

It's pretty easy to see that there are defined roles for front end and backend here. It is helpful to note that the UserInterface class is **not** the only class responsible for drawing, as it only handles drawing components that are not entities! <br><br>

However, to update it to work with my options menu, now it also knows what menus it wants to draw. It does this through a system called Contexts, in which basically act as the active menus currently being displayed (This isn't necessarily true; a better explaination is that Contexts are UI events that take input from a Controller, but for now just think about them as menus!). This context system is the basis of the action menu UI. <br><br>

### Contexts!
Context are really simple in honesty. The main idea is that there can only be one focused context at a time. This context is the context that is currently recieving input. Contexts know what menu they're currently drawing over (if there is one), so it's really easy to swap back and forth. This is super helpful for things like nested menus (E.g. Options -> Controls -> Keybinds). If you have multiple contexts on the screen, you can also click into one to focus that context, in which it will perform linked-list operations to put itself on top (this is probably the only example of linked-list you will ever see in your LIFE). <br><br>

### That's Great and All, but Selecting Text?
Yes, the context system has nothing to do with selecting the text. Looking back, you are probably guessing that the option menu (or I call it action menu) is a ITextureEvent and ITextEvent, so it handles both the texture and the text. While it certainly handles both the texture and the text, it is not an ITextEvent. This may seem counter-intuitive, but remember what I said about what the structure is supposed to be! More specifically, "if a class wanted to draw something, it would create a class that implemented the corresponding event". This is saying that the structure of the action menu is recursive - it wants to draw text information that is not going to be static (think about the red and green highlighting to show your current options!). This means it creates children events ActionMenuHeaderText and ActionMenuOptionText. The ActionMenuHeaderText is what is displayed and highlighted in green at the top. The options are in the middle and highlight in red. <br><br>

The actual difficult part of the option menu is not selecting options (once we have contexts set up, it simply listens to controller input and responds accordingly), but making sure we don't waste resources when swapping between the Action and Skill menus. We don't want to actually *all* of the information, we just want to remove it from the draw queue. This is because creating, deleting, then recreating the information is wasteful when the action menu is not actually moving or the text isn't changing. In order to accomidate this, I created additional functions in UserInterface, SendToQueue and RemoveFromQueue! <br><br>

Now, the next step was creating the skill uis when you actually selected the skill. <br><br><br>

## The Skill UIs
Binding the skills to spawn the indicator UI was as simple as binding the call. However, actually creating the indicator UI was not! <br><br>

I learned that Monogame does not have built-in support for drawing circles. That means I had to do this myself. Even worse, I had to face my dreaded enemy to do this: math. <br><br>

Now it would be reasonable to assume that, with my minor in math and my experience in graphics programming, drawing this wire-frame indicator would be a BREEZE for me, but it unfortunately was a messy process that led to many crashes and funny graphical issues. <br><br>

In all my infinite wisdom, I did not actually save these funny issues to share because I can't think ahead past dinner. But! I can show you how the circle is drawn:<br>
<p align="center">
  <img src="{{ site.baseurl }}images/week_in_review_2/circle_draw_example.png" alt="Circle" width="300">
</p>
<br><br>

I got the draw line code from online since I was not going to figure out rotating a line myself, but I used that to make a pseudo-circle by what is essentially spinning a point around in a circle and drawing a line between intermediate moments. It let me come up with this indicator to showcase range: <br>
![Range Showcase!](images/week_in_review_2/range_showcase.png)<br><br>

You'll also notice a line coming out to the edge of the circle - this is because the ability I'm showcasing is a targeted dash. This line follows your cursor up until the edge of the border. You can't see my cursor because the silly windows screenshot actually hides it when you take screen shots - but this is actually done through setting the positions of the end and start point to anonymous functions! This allows the indicator to constantly follow the mouse without having to subscribe to an update call (as we would like to keep the draw and update calls as seperate as possible). You can click to confirm casting the skill or right click to cancel casting the skill. <br><br><br>

# Health UIs!
By now you have noticed the very pretty health uis underneath the character. Much like Unity, these health UIs are actually just a loading bar - more specifically IFillBar! This event actually has three children: the fill texture, empty texture, and border texture. In this case, these textures are simply green, red, and grey respectively. <br><br>

The difficult issue with health bars was actually just placing them. They all depend on the character and are offsetted from them - but also have their own concerns. For example, the fill bar has to offset itself based on the health percentage to be thinner. Each of these bars also have to listen to the characters movement and health display. <br><br>

Listening to the character's parameters is actually really easy. For every single stat, there is an event handler that fires when it's changed. The character uses this to see if the change was damage taken or healed, but our health bar can hijack it to just update itself. The movement event is used for collisions, but it can also listen to it. <br><br>

All of these event listeners does pose the issue that I always forget to unsubscribe to them - and that was certainly an issue. In fact, I unknowingly had used up a gigabyte of RAM just because I forget to clean up those listeners, meaning that both the character and health bar didn't actually get cleaned up when they were no longer rendered! <br><br>

Anywho, you can see the fancy health bars in action:<br>
<p align="center">
  <img src="{{ site.baseurl }}images/week_in_review_2/health_bar.png" alt="Health Bar" width="300">
</p>
<br><br>

### Why No Text?
This is actually funny to me - the main reason that there are no numbers to display the text is that they render horribly under 12 point font. Obviously, you don't want your text being too small, but 12 point font was way too big for what I needed. <br><br>

I actually set up a whole system and edited to render the text correctly, only to not use it. I'm sure I'll use what I implemented later, but at the moment it remains unused. <br><br>

# Further To-Do
Since I don't think I actually shared it before, this is the updated to-do list I currently have and you can expect to see:<br>
\-Create more skills (particular cast time)<br>
   \-Finish Eclara<br>
   \-Create Alata<br>
\-Create ephemeral turns (and cast times!)<br>
\-Create turn projections<br>
\-Create Highlighting follow actions<br>
\-Create simple animations (pull from RPG Maker animations for now)<br>
\-Create more complicated damage (can be done anytime really)<br>
\-Create final two characters that will be used in demo:<br>
   \-Lattice<br>
   \-Lyscander<br>
\-Create resources (mana/charge)<br>
\-Create skill modification with charge<br>
\-Create basic AI to fight back!<br>
\-Threat indication<br>