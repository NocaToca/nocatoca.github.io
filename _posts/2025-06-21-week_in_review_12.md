---
layout: post
title: "Time Skip! - Weekly Update #12"
date: 2025-06-21
excerpt: "A lot of updates, honestly! Might switch to bi-weekly updates?"
categories: [GameDev,Project,Update,New]
pinned: false
---
# Heya!!
So, yes I did miss last week! It wasn't on purpose - I had a long time friend come down and obviously wanted to prioritize his stay over updating my two readers. Now, it is fair to point out that I could have updated Monday to Friday - I really should of! But, unfortunately, I am a creature of habit. I have various other things slotted for those days that make it hard for me to make the time.

Regardless, I'm sure you didn't come here to read about my psyche - you want to hear about my game updates! Well, I have news that may be good or bad - depending on what you're coming for (maybe you're from the future too!). 

# Bi-Weekly Updates!
Honestly, when progress was quicker, I found it really easy to post something every week. But as things slowed, I kind of found myself trying to figure out how to regurgetate similar information to you guys while keeping it interesting. This week break made me realize it's much easier when I quite obviously have more to talk about. So, I am debating moving to bi-weekly updates, since I want these to be interesting to follow, and not like opening one up to see very small incremental progress that I have made. Maybe you like that - if so then sorry!

So, I probably will keep the Weekly Update title, but swap to posting them bi-weekly. Or, also whenever I feel like it. It's not like I can't just make another lore/character/aside post (YEAH WHERE ARE THOSE NOELLVA??) whenever I want anywho. 

# Updates On the RPG?
Another thing I realized after reading a bunch about "making successful games" (whatever your definition of that is), is that, while I don't really care about money, I do care a lot about clout. This matters because I currently have no following (my highest count was Twitter at like 1k which I deleted, now it's Bluesky at 150 or something). There's a lot of reasons for this - mostly that I'm just bad with social media - but it is something I realized I should remedy as well.

Another thing that tacked onto this is that when I was making the game jam game, I realized how fun it was to like... actually complete features and work with engines. Don't get me wrong - I love Monogame and working with frameworks! But I think I need to feel some sort of validation on myself before I slam my head into a wall for around a decade. I do get this with my current job (solving those problems are VERY satisfying!), but in a game dev sense, it was growing increasingly upsetting to me that I was experiencing road blocks that kept putting my production outline back and back, without anything really allowing it to move forward. I think the problems I was working with were fun, but it seemed like I was doing a lot less game design and a lot more engine design.

I love tooling as much as the next girl, but I started the project with the idea to make games, not make tools. 

All of this to say that I'm going to develop the RPG in the background, and going to work on another game idea I had in the foreground. Just figured I'd let you guys know, but there probably wont be much updates on that project for a while.

# Well - Then What Is This New Game!
I'm glad you asked and did so totally unprompted and unforced by reading through this text that you are definitely still reading through!

I have a very interesting friend group, which makes playing games with them actually really fun. They're not very serious and there are various skill levels that portray themselves. On top of that, we have been completely distraught over the lack of non-competitive games to play together. MOBAs, FPS games, and whatever else that comes out is always grounded in competitiveness. It was my main gripe with Omega Strikers, that I didn't really find out until after they released. 

If you're a competitive gamer, that's fine! Nowadays though, most of us find competitive games extremely discouraging to get into. Even if the onboarding is good, mastering a whole new set of mechanics and trying to outcompete other players is much more of a chore than fun. I also do not want to spend my hour a day gaming gambling whether we will have a fun match or not. 

The last concern is that we don't really have the same amount of time as we used to. All of us work. Some of us live in Europe. It's hard to schedule long term games we enjoy and can play together (like Stellaris).

Additionally, it's hard to try new games, since we all have to invest the buying cost with the concern that some of us might not really like it. For instance, I really enjoy games like Lethal Company and REPO, but no one else really does. On the otherside, they have been really enjoying REMATCH, but I absolutely do not like the game enough to pay 30 dollars for it. Meanwhile, my brother brought the deluxe edition or whatever it was called to play early. I also do not really enjoy Plate Up!! enough to pay for it, but they all love it. I do like watching though.

This leaves our group with surprisingly very limited choices to play together! The main games we do play together are like Helldivers 2, Golf With Your Friends, and Minecraft. Not a very big line-up! This made us debate making a game for a while (well, more like having me make a game they can all play. Talk about lazy!).

The main premise is a co-op ship management game that mixes FTL and Plate Up. However, you manage the ship through magic systems that mix sci-fi and magic elements to create a silly, fun, and unique gameplay experience!

That's my elevator pitch at least. Let me explain a bit better.

## Ship Management? Magic?
Yes, these two things are not typically things you think about mixing together. A lot of sci-fi co-op ship management games that are currently out (like Void Crew or Jump Ship) are very traditionally sci fi. I actually really enjoy these games! However, I'm a very technical person. I see complicated systems and get attached to figuring them out. On the opposite end, my one friend (who is a civil engineer), just sees it as doing his job when he's not working - which is very understandably not fun! Hence, came his idea to abstract the systems to be a lot more goofy, so he could get attached to the system without caring so much about the mechanics.

Originally, I did try to design the ship in a way that the magic was a toggle (so you could play traditionally and bizarrely), but as I read the GDD and developed the game, I realized that the magic toggle was actually just the soul of the game. The non-magic system read like the first sentence of the elevator pitch and that's it. You might have your own opinions on it, but it not nearly as interesting when you don't include the second sentence.

All in all, I came to the design conclusion to use these magic systems.

## What Do These Magic Systems Look Like?
These are still very much in the design phase, but I'll happily go over each one here! A helpful starting note will be that I did originally create the "non-magic" systems. I say this because it'll be a million times easier to understand them if you understand where they came from. These are as follows:
- Power Module
- Heating Module
- Life Support Module
- Shield Module
- Weapons Modules
- Engine Module
- Sensor Module

I made 7 modules because I plan for the game to be 4-6 players and always wanted the stress of not being able to always cover everything, so people wouldn't just stay in one room. Anywho, these quickly transitioned to the magic modules you see today.

## The Bar (Power Module)
The main idea of the bar is that you create alcoholic beverages to power each module system that needs power (since a lot are magical, some don't need power). You are essentially brewing your own beer to send to modules (yes you can also drink it! But I wouldn't recommend it. Drinking it can be really bad!).

There are a few components to "The Bar".

First, you have the Base Pantry, which provides the alcoholic base. At the moment, this is distilled on-the-spot for you. This is literal alcohol you have to add. Different systems want different bases:
- Life Support wants Whiskey (Wheat),
- Weapons want Rum (Molasses),
- Heating System wants Beer (Barley)
- Engines want Wine (Grapes)

The brewing process can be as simple as choosing the correct base and putting it in the correct module. However, you can improve your power consumption by brewing up your own concoctions. Generally, you will always want to do this, unless you really don't have the time. The benefits are immense! 

You can put literally anything into the blender and see its side effect - if you're a bit of an experimentalist. Alternatively, you can purchase and find recipes, which are randomly generated at the start of the run. Generally, there are no invalid recipies, but ingredients may have different side effects depending on the rng. E.g. a blueberry could provide +3 bonus weapon damage or +2 fish efficiency. You'll have to brew to figure it out each time. 

You can also prepare foods. Unwashed (and unsanctioned) foods can crash systems (also, over powering systems can crash them - monitor their BAC!!). Preparing foods amplifies its effects. Both preparing and washing force you to play a cooking mama - esque minigame. Same as the blender, where you blend everything together.

An additiona; thing to note is that you always need to blend with Astral Essence, which is easily obtained. It's just the magic stuff that makes it work with the magic system (and an in-universe write off).

## Fish Tank (Heat Module)
This is actually the main module I will be showcasing later on (next week, since this post is insanely long), as it is the one I started with. Now, it might seem completely insane that fish would be related to heat, but remember that these are space fish that are magical! This is also currently my favorite module! 

Basically, you have a fish tank of heating and cooling fish (named Aetheringlis and Aetherglacis respectfully), and you have to manage where they're going. This is like a traffic minigame, as if a heating fish collides with a cooling fish, they both lose hp until they die. Fish move along vents, but are in "Fish Liquid" systems above them, so they're not effected by any drops in oxygen.

Heating fish heat up the area around them while cooling fish cool down the area around them. They will stay in tanks until they are needed, although you can only hold 2 of each type in the tank at a time. When you send them out to a room, they follow a network known as "the fish network". This is randomly generated, but can be changed to your liking. It's important to consider speed and chokepoints when designing your network, as making too many chokepoints will make it hard to determine if fish will collide and kill each other while making it too slow will cause the fish not to reach the rooms in time. Additionally, each node can only have 2 incoming and outgoing connections. 

You can also fish for more fish in outerspace if you run out or need more. You can choose cool bait or heat bait. You play a minigame like stardew valley's fishing minigame to catch them. You can also name the fish.

## Bubble Center (Life Support)
The bubble center has a spot to fill bubble cans, of which you start out with 1 only one (with a max of three). Players must run around the ship and keep bubble concentration above a minimum amount - which acts a lot like basic oxygen. Bubbles do not like heat, and will pop when Heating Fish pass by. Low bubble count equals suffocation. You can "vent" rooms from the bubble core module, which will open an air duct, release all bubbles and all heat. This is useful for situations where your room is on fire - as fire cannot live without the bubbles!

Bubbles have a very simple mixing interface. You can choose a bubble base and a bubble scent, which has different effects like the power module. However, unlike the power module, the effect is based on the two mixed elements rather than the elements being additive. These can give bubbles more heat resistance, durability, longevity, or just a different color. The important thing is that you have to wait for the bubble center to refill the bubble blowers. 

Bubble concentration does not like closed doors. They will not move past closed doors - so either have an open door policy or ensure each room as a good amount of bubbles!

## The Orb (Sensors)
The Orb is a very helpful system that has the power of sensing. It gives the following benefits when activated:
- Displaying Enemy Ship Information to Weapons
- Seeing Current Fish Positions
- Increasing Ship Passive Evasion
- Seeing the Rooms the Enemy is Currently Targeting

The Orb is powered by Tarot Cards like any futureseerer. Each tarot card has three tags that provide different effects when activated. These can be beneficial or harmful. 

There is a table where these tarot cards go, containing three spots for three tarot cards. When the Orb can be activated, it places two tarot cards in random positions on this table, and waits for the player to place the last one. These placed cards cannot be moved!

Additionally, tarot cards activate their tag effect (the effect correlated to the tag) based on the position that the card was placed. So, being placed in the first position will activate the first tag, the second will activate the second tag, and the third will activate the third tag!

## Shields
Shields are SUPER simple! They are powered by the power of friendship! When shields go down, players have to go to the affected side and hug to recharge them.

## Weapons
So, I'm still not sold on anything for the weapons, but I'm thinking of it being a bit of a deck builder, with the person manning the weapons (at the time, everyone can do this whenever) creating combos from runes (so they'd be casting spells) to amplify the ships weapons and attack the enemy. I need to figure out the logistics for this, but this is where I'm leaning towards.

## Engines
I don't have anything for engines right now!

## That All Looks Really Fun! Is There Anything Else?
I'm so glad you think it's fun and are not just saying that because I am picturing everyone saying that and loving my idea! Yes, there are more elements to the game that I will gloss over (this blog post is already extremely long! And no images! How will Yuumi read!).

The first one is that there are narrative events that can be as mundane as filler text to changing interactions with systems. For instance, one event can make it so that fish can no longer die from collision, but instead need to recharge at the heat module. 

The other thing is that players progress through runs by earning traits. These traits can be game changing as well, but I'll leave examples of those for later.

The main design of all of this is that progression makes you feel like you are growing and getting stronger, but can make it start to feel like you're carrying a bigger and bigger burden due to the negative events and traits that ultimately make you lose your run.
