---
layout: post
title: "Camera - Weekly Update #4"
date: 2025-04-19
excerpt: "I was lazy this week"
categories: [GameDev,Project,Update]
pinned: false
---
# Progress Is Progress!
So, if I am honest, the camera system was a lot easier to implement than I thought it would be. Like a lot easier. All I had to do was add a MainCamera property to my main game class, then update the SpriteBatch.start() call in order to accept the camera offset, zoom, and rotation matrix. Since I had *some* experience creating renderers with Vulkan, this honestly was not that difficult to do! <br><br>

The main difficult thing was that all of my textures were set up to be worldspace textures. While this isn't a theorically hard separation, it was a tedius one because I had to decide which texture was screen space (like the timeline) and worldspace (like characters and the healthbars). After I untangled those though, it allowed me to create this easy to set-up draw queue order:<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_4/drawbatch_order.png" alt="Draw Order">
</p>  <br><br>

This is a pretty simple concept I overlooked, but it was actually what took most of my time this week. I finished my camera to-do in two-days aside from that. Now I'm able to do silly neat effects like this!:
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_4/CameraActions.gif" alt="Camera">
</p>  <br><br>

Now, now, obviously this isn't all impressive, but it does showcase zoom, movement, and the other thing I did this week: setting up a Time class! Also, clap clap Noellva, you set up gifs on your blog. <br><br><br>

# Camera
So, like as I mentioned before, setting up the camera was actually not that difficult. The theory was really simple, and it can be seen with this one function - which as you may notice is what the SpriteBatch actually calls: <br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_4/get_transform.png" alt="Get Transform">
</p>  <br><br>
Focus is the current focus of the camera in world-space. This can be anypoint, but the easiest concept is that it's equivalent to a character's position. Now, an amazing question to have is on why the focus is negative. The idea seems unintiutive, but it is probably because you're thinking that the camera moves for the world and not the other way around. As far as I'm aware, most camera systems are actually static, the camera isn't the one moving, the world is the one that's moving. This means we want to make the focus negative since we want to move the world over to focus on that point. <br><br>

That was probably a bunch of mumbo-jumbo, so here's a nice little diagram to help showcase what I mean:<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_4/diagram_1.png" alt="Diagram">
</p>  <br><br>

Basically, if you want to move the character focus to the Camera focus, you can do these two operations:<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_4/diagram_2.png" alt="Diagram">
</p>  <br><br>

The whole reason behind this is that you're moving **the character focus point** and **not the camera focus point**. You're essentially moving the world to conform to the camera. <br><br>

That's all well and good, but what about the rotation? Matrix.CreateRotationZ simply rotates everything around the Z axis. Since we're in 2D, our plane is the X and Y plane, so the Z obvious rotation pivot. <br><br>

A similar idea is shared for the Zoom, as we only really want to zoom in on the X and Y parts of the plane. The Z does not matter for us, since we're 2D.<br><br><br>

## Cameras Are Hard Game Design!
So, the actual issue I was having was that what I thought would be nice camera control actually turned out to be AWFUL. For example, my first thing on my to-do list was setting up following a character. Well, when I did that, actually doing the combat became really annoying. This was because when I moved my character, my camera just started to focus on their movement, which was not what I cared about at all! It is nice to see that it is following my orders - but I can do that without focusing! <br><br>

This trend is pretty typical for me, as I tend to not have the best game design out there. But it really showcased in my camera work. Another one was how I initially set up panning the camera, with the camera moving in the direction your mouse is when it is out of the screen. While this was not awful, it was annoying when trying to target characters on longer-ranged spells. This was because my targeting is mouse centric while I made my camera movement mouse centric, which basically meant I was throwing my mouse all over the screen. For this reason, I implemented WASD camera movement which made it feel much better, as I could keep my mouse in one place and use my second hand to move my camera. <br><br>

# Time
Another issue I had was that everything thing I was currently doing was reliant on when it's OnUpdate was called, independent to considerations of relative time, just the raw delta time. This meant that I did not have an actual means of pausing or slowing down the game, which I amended by creating a simple Time static class. While the implementation is really tedius, it is going to be really helpful for animations, as if I want the time to slow down to handle the animation, I have the framework for it. And yes, animations are next! <br><br>

I am planning to use spritesheets I have used and maybe made (I forget) for my RPG Maker games before moving onto creating actual animations. 
