---
layout: post
title: "Skills! - Weekly Update #6"
date: 2025-05-03
excerpt: "Working on and creating support for skills!"
categories: [GameDev,Project,Update]
pinned: false
---

# Didn't You Already Do Skills?
Yes! I did! Wow. I have readers that have read more than one post of my blog ;-; <br><br>

Actually, looking back at my five amazing posts, I don't actually think I went over how skills work or are implemented. I might have been hesistant because, at the moment, I don't think they're implemented all that well, but since this week is going to be talking all about skills I'll go over it! <br><br>

Before going into anything, I will want to remind everything that I don't really know what I'm doing! Also, the UI interaction is a bit complicated - at least I think so. Regardless, it's really easy to set up. <br><br><br>

# So, Let's Create a Skill!
I'll will be going over a lot of implementation details for Lattice's skills. I know I haven't introduced her yet, but I'll explain when it's important! <br><br>

To start, the overall skill structure looks like so:<br><br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/skills_structure.png" alt="">
</p>  <br><br>

Essentially, skills get registered by Character.InitSkills() on Character initialization. They also inherit from IAction, ISkill, and SkillBase. This allows it to behave like a basic attack action - which is beneficial for our GUI. The SkillBase function is literally only there to remind me to make a constructor for the skills - I didn't have it originally and kept forgetting which kept breaking things haha. <br><br>

Regardless, the next step would be to let the player know that they can use the skill on the skill GUI. This is luckily already set up for you! The skill GUIs all look at the characters RegisteredSkills property in read-only mode. This keeps control of the skills to the Character. On selection, the GUI doesn't actually immediately invoke the skill, it brings up the skill's UI for users to check the potential effect of their skills. You can see this in my previous gifs, it gives indicators and ranges which is helpful to know where you are aiming! <br><br>

You might think that means the skill sets all of this up itself, but no. The skill actually just creates and activates the context after passing in what it wants the context to display. How do we know what context to display? Well, we can look at the skill description for it! Let's look at Eclara's Umbral Dash, which has the following description:<br><br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/umbral_dash_desc.png" alt="">
</p>  <br><br>

Oh! Well, uhm, this description isn't TOO helpful of what we want to display - but we know we are targeting someone in a radius *around our position*. I stress that because where we center our UI will be important later. We also know that this will be single targeted, so it may be helpful to preview the raycast to ensure we're hitting what we want. Luckily, there's a really useful Context that sets this all up named CircleIndicatorContext! Literally all we have to do is pass in the skill and radius. The skill is important so that the context can invoke it (remember - contexts hijack the controller). This is *the only UI interaction we need to do*. Very concise and nice! <br><br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/umbral_dash_show_skill.png" alt="">
</p>  <br><br>

The next step would be actually setting up the Invoke() call on the skill. I will not go over that because I am about to go over a whole lot of implementations of those for Lattice. But, just know that the SkillContext calls this on activation. For Ephemeral Skills, this Invoke also calls the Ephemeral Invoke (or, more accurately, tells the character to call the Ephemeral invoke on their next turn).<br><br><br>

# Well, What Is This Kit We're Implementing?
Good question! If you haven't noticed (it's only been two character reveals, so all will be forgiven), each character is centered around a specific unique feature. For Eclara, it's her Eclipse damage. Alata is the Dream and Ephemeral turns stuff. Lattice's whole thing is crystals - she's a long-ranged assassin mage that does better with the longer the fight goes on. This is because she applies the status Fragmented on hit, and enemies that die with this status turn into a crystal. These crystals are the corner stone to her kit, and basically every ability of hers relies on them in some way! <br><br>

That is just a brief overview, but the first task was to actually spawn these crystals. You may have noticed that I was working on status effects last weekend - that was for Lattice's kit! Essentially, on attack she applies the Fragmented condition, which spawns a crystal when the enemy dies. You can see this in action here: <br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/lattice_attack_anim.gif" alt="">
</p>  <br><br>

You may also notice that I finally used basic attacks! This was actually not implemented before this week, but they work similarly as skills. Attacks are done through raycasts - which means you will have to have line of sight of the target. I don't have walls yet, but we'll get to that once we get there! <br><br>

Anywho, the first issue was an ability called Fracture. You can see the description here: <br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/fracture_desc.png" alt="">
</p>  <br><br>

I don't know why I do this to myself, but I made the ability have conal based collisions and I had no conal based collisions implemented - nor had an idea on how to do it effectively. Luckily, I remembered some things about geometry. After all, cones are just subsets of cirlces or spheres - I just needed to know the arc length of what I wanted. From that, I can just add a simple check to the CircleAroundPoint cast:<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/cone_check.png" alt="">
</p>  <br><br>

So, I imagine that this isn't intuitive. As a brief explanation, to_point is simply the direction from the center of the circle to closest point of the object to the circle. We check to see if the angle from the center is within range of our arc angle. If it is - it hit! If you're not convinced, here's a helpful little diagram: <br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/cone_collision_diagram.png" alt="">
</p>  <br><br>

You can see from this diagram what exactly is happening. The distance check is still the same as the circle collision, but we're bounding collisions to a specific section of the circle. To do this, we compare the angle created by the distance vector and the to_point vector and comparing it to see if it's within bounds of our angle. It's divided by 2 because the dot product will only return a positive value, meaning that we only need to consider one section of our arc length. Math! (P.s I'm sorry for being so math heavy, but it's probably only to get worse). <br><br>

Anywho, I also needed to display this. Without reiterating what I just went over, I did something similar to my circle-drawer. Boom! Now I needed to get the skill context to draw what I wanted! <br><br>

To do this, I first had to actually *figure out* what I wanted the display to be for the skill. I ended with with the idea that you would want to hover a specific crystal and then see it's arc outline, instead of the alternative of showing every single arc outline all the time. This meant I had to create a new SkillContext: ShowOnHoverContext and ConeHoverContext. The ShowOnHoverContext is an abstract generic class that derives from the base SkillContext. ConeHoverContext is also generic and derives from ShowOnHoverContext! <br><br>

You may ask, miss Noellva, why are these classes generic? Well, this is so that you can limit what you can hover on. I did say that I only wanted this to happen for crystals - so there's no point to show the cone on enemies - that would also be misleading! And if you want to limit your choices, you can additionally pass in a predicate function, which passes the object in to for improved filtering! <br><br>

Well - you may be thinking, couldn't you just pass in a list of the objects you want to be hoverable? Why, you can do that, but then you'll have to iterate over the list of alive entities to see which one you are currently hovering *and then* check to see if that one is in the list. Instead, this function is just O(n), becuase I paid attention in algorithms (I saved 2 milliseconds of execution time). <br><br>

Moving on, this got this amazing functionality on hover: <br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/bad_cone.png" alt="">
</p>  <br><br>

Now, I don't know about you, but I thought that cone looked a little weird. To be quite blunt, I wasn't sure were you'd put the ice cream for it to hold. It did look cool, but was definitely not what I was looking for. <br><br>

Believe it or not, I spent a while trying to debug this. The issue turned out to be that I thought it was doing these Cos and Acos functions in degrees. Nope - it was radians. That is why the variable in my cone collision function is called arc_angle_radians - it was originally just arc_angle. Regardless! Once I fixed that, I got this functionality:<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/fracture_anim.gif" alt="">
</p>  <br><br>

This is MUCH better and exactly what I wanted! I was able to use this to implement a few more abilities, like Rupture, which targets an enemy and has the closest crystal or Lattice attack it:<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/rupture_anim.gif" alt="">
</p>  <br><br>

# Is That It?
Wow! Rude! Believe it or not, implementing skills is hard! But no, actually I want to go over a bit of a plans. <br><br>

I talked a lot about skills, but honestly they're a pain in the ass to do. This isn't neccessarily because they're hard to implement; they're much more tedius than difficult. I have been workshopping a seperate tool using Avalonia UI that will streamline not only the skill creation process for me, generating and registering classes as I need them, but other things like Characters and quests as well. This *should* also really help with balancing, because at the moment I'm throwing a bunch of random variables in without thinking too much about that. Because they're more or less hardcoded and I don't have an editor like Unity or Godot, it will get quite difficult to shift through everything while fine tuning. In fact, you can see how big the project is right now: <br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_6/project_size.png" alt="">
</p>  <br><br>

I'll go into more detail when I make the tool, but that will not be for a while. My biggest priority is developing a vertical slice before anything else, which I have mentioned before. Once that is done, I will almost certainly recode the engine with what I need in mind. I'll make the tools while I'm doing that and go over that process with you all. <br><br>

Additionally, I have been scouring for more art for the game. That and music. I'm waiting for a solid artstyle before going for music, but I have ideas for the art style I can go over once I get artists involved - artists that are at least better than me. <br><br>

Finally, Expedition 33 came out and I am quite eager and inspired by that game. It's very similar to what I'm going for in story, composition, and mood, and I'm super glad to see that turn-based games are still popular. I am a bit intimidate by how visually impressive their stuff is, but that's to be expected. I did also learn that France gives money for media like Video Games to try and sponsor French culture, which honestly is something I was very surprised to hear about. If only the US did the same! (Please tax payers fund my aspirations). <br><br>

Regardless, I'm hoping to have the vertical slice done in roughly two years. That may seem like a long time, but I only work on this project around 14 hours a week. That is also much more than just the combat system, whose prototype I'm hoping to have finished by the end of July. I'll keep everyone updated on estimated timelines, but just a general idea for what I'm shooting for. I'm also hoping to start marketing in around a year - and I'm hoping it'll be easier when people can look and see these old/first blog posts. <br><br>

People may worry about the scope and scope creep I set on myself - but I'm perfectly aware how outrageous most of it is. It's not really a deterent for me anyway. The caveat is that I try to keep scope creep to a mimimum - the systems I have planned are the systems and things that are in place. Even the story is pretty much planned!
