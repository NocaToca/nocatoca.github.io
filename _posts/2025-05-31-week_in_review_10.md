---
layout: post
title: "Tools - Weekly Update #10"
date: 2025-05-31
excerpt: "Started Tooling!"
categories: [GameDev,Project,Update]
pinned: false
---
# No More Game Work!
Well, that's not entirely true. Also depends on how you look at it. Technically, tooling is working on the game - it's basically working on the engine - but, to me, it feels like I'm not making progress. Not that tooling is bad - it'll enhance the workflow for later - but, you know! It's not the same as just working on the actual game!<br><br>

Gosh, how I ramble. I don't even know how it's possible when I'm typing. Jeez! Or is it geez? <br><br>

Anywho, I spent the week setting up the Character tool, which will be used to edit and create not only characters but skills. It's already very handy, as it's a central place to edit all my characters and stuff for balancing. Balancing of which I have been completely ignoring.<br><br>

# The Tool!
A short overview of what I'm doing is using Avalonia UI to create a super easy interface to my code. I'm loading everything using Roslyn and then showcasing the variables I mark for edit. I'm marking the variables using attributes for easy metadata, although the skills just look within the "InitSkills" function that registers them. <br><br>

Before you ask, I was going to use a resource file to store everything, but resource files don't let me do everything I'd like. If it was *just* editing the values, they would've worked great! The issue is that's not the case. I need to create character classes when creating new ones and the same goes for skills. I need to use a language tree regardless, so I figured it'd be better and easier for me to not mix and match. Resource files are also slower, as my code would need to load the values on boot-up (granted, this would be a neglible performance impact). <br><br>

## Roslyn? What's That?
I really wanted to showcase this! I'm still learning the specifics of [Roslyn](https://github.com/dotnet/roslyn), but I do really think it's a neat tool. Quite ironically, it was pretty easy for me to pick up because it is essentially the same thing I've been doing at work. SyntaxTrees are really cool!<br><br>

While I can't speak for how Roslyn itself is exactly integrated, it will help to know how a syntax tree usually works. These syntax trees are essentially what make up languages - compilers and interpretors generally parse syntax trees in order to read the language itself. Let's say we have this block of code:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_10/class_example.png" alt="">
</p>  <br><br>

This is compiled into a tree like so:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_10/tree.png" alt="">
</p>  <br><br>

Obviously, super simple examples carry super simple trees. Roslyn trees, for example, contain information about everything - including whitespace. I'm obviously not showing everything - just hoping to give you a high level overview of what's occuring! In general, there are three main components to a syntax tree:<br>
\- Expressions<br>
\- Statements<br>
\- Declarations<br><br>

Expressions are, in simple terms, parts of the code that produce value. Literals, function calls, and arithmitic are examples expressions. <br><br>

Statements are actions that control flow, like your ifs and for loops. Assignments also count as statements.<br><br>

Declarations are like variable assignments. Everything shown in that tree is the definition portion of the method (aside from the return and block leaves - those are statements). <br><br>

Each major thing you can think about (that aren't keywords like "override" or "partial") are one of those three things! It's all very neat how it all comes together. In fact, I love all of it so much, I am high-key thinking about making my own language! Of course, I have other priorities right now, but it is something I like to design in my free time :3<br><br>

## Why the Explanation!
As I mentioned, I'm parsing through the language tree to find what I need. At the moment, I just have it editing stats and detecting skills. It detects stats through an attribute known as EditableStat, which looks like so:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_10/attribute.png" alt="">
</p>  <br><br>

The "Health" literal is the display name in the tool, which can differ to the display name in the game. The second one is the stat id, which is used to order the stat on the tool display. The last value is the actual value that is inputted into the character on startup. <br><br>

Skills are detected by looking for a method declaration called "InitSkills", going through the body to find the list initializer, then seeing what types are being created in said list. The method, for reference, looks like so:
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_10/init_skills.png" alt="">
</p>  <br><br>

All of this is really helpful, as now I have quick access with the tool!
<br>
<p align="center">
  <img src="{{ site.baseurl }}/images/week_in_review_10/tool_example.gif" alt="">
</p>  <br><br>

Obviously, it's pretty ugly right now - but it's a work in progress.<br><br>

# Game Updates
I did make updates to the actual game. The main one was that Stats werent a class before hand, so I condensed all of what I had to be a super simple stats class. I'm quite happy with how nice it all is now, and I honestly do not know why I did not do that from the start. I guess that usually happens in development, being in bewhilderment at what decisions you made in the past. In fact, I know I'm going to look at this tool and be like: "why did she even think about doing it this way!?" <br><br>

I say this because I have also decided to de-scope the game. Again. I'm relegating the whole story to a single region - not even the Yami Collective like I mentioned in (the worldbuilding post)[https://noellva.blog/gamedev/project/2025/04/01/world_building_post/]. It's the Huashan, which I still need to post about! I swear I will - you can totally trust me on that!<br><br>

With descoping comes character changes though. The only one I'd imagine be familiar is that Alata will be changed a bit. Everyone else you have seen so far (even though I didn't post about them all yet) haven't really changed too much. It does mean I have to create new characters too! So that'll be a fun process - good thing I have a character tool to use now!<br><br>