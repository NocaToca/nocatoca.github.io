---
layout: post
title: "Elemental Damage - Weekly Update #8"
date: 2025-05-18
excerpt: "Elemental attacks and damage system!"
categories: [GameDev,Project,Update]
pinned: false
---
# Water. Earth. Fire. Air.
Or as it is in this game - Nature damage! You know, maybe I should change it to avatar damage... <br><br>

I'm sorry if this is the first post you're reading of mine. I'm cringey.<br><br>

Anywho, this week is going to be a lot of words - not a lot of pictures or fun diagrams that I am absolutely famous for. The thing was that this was mostly a code and design decision, one I am honestly not that settled on. I'll get into everything and why, but for now let's talk about how it currently works in-game!<br><br>

I'll provide my core concerns upfront, as I do ramble a bit here. You can think about a TLDR is me going over these three things:<br><br>
- Should I keep this elemental system?<br>
- Should I simplify or modularize it?<br>
- Is it worth keeping just for Eclara?<br><br>

# Overview!
The main gist is that damages have different damage types. These types are split by two main categories: physical and magical. Magical is what we're focusing on here, as that is then split into multiple other types. These base types include:<br>
- Fire<br>
- Ice<br>
- Water<br>
- Earth<br>
- Wind<br>
- Light<br>
- Dark<br>
- Celestial<br><br>

These base types can then be combined to make a combined type. At the moment, these combined types include:<br>
- Nature (Water + Earth + Fire + Air)<br>
- Eclipse (Light + Dark)<br>
- Frozen (Ice + Earth)<br>
- Cinder (Dark + Fire)<br><br>

I'll explain what each of these do and what their special applied effect is in a moment, but the first question is how these are applied. The answer to that is actually pretty simple. When a character deals damage, they send over the information of the raw damage they do. Any listeners (typically just weapons) add to that damage dictionary. Then, the damage is all added together and applied to the character that they're damaging. Before it's finished, it counts how many appearances of a certain damage type exist. So, if you are damaging through a skill that adds fire damage and your weapon deals extra fire damage on that skill type's hit, that'd be two fire appearances. This then passes that information to the character's ElementalHandler, who adds those to the list of elements, checks to see if it can combine anything, and then updates the stacks of each element. In this case, if it was empty, the character would have 2 stacks of Fire.<br><br>

If the character had one instance of Dark, however, the ElementalHandler then combines the fire and dark to create Cinder and keeps the extra fire. So it'd be one Cinder and one Dark.<br><br>

There is a huge issue that the above introduces, and it's not one I really am keen on tackling. Let's say that we have a character that is dual wielded and both weapons have on apply effects. Let's say these effects are Fire and Earth. Additionally, let's say that a character then has a buff that adds Dark and Air damage. Finally, let's also say that the character is already afflicted with water. Thanks to this super complicated scenario, we get to see just how flimsy a system like this is. Realistically, the second weapon does not matter too much because that's done on a follow action. However - if the character's build for some reason relies on doing that Fire and Earth combo, it reduces their agency in this situation. Furthermore, when they apply the fire damage, it'll turn to Cinder before turning to nature. If we want to make it more complicated, if the character is already afflicted with earth and water, what will the resulting type be?<br><br>

There are solutions to this, I know that for sure. The issue is that I'm not sure what I want the solution to be. Additionally, if the character has a lot of OnAttack listeners that edit the damage information, technically the order of that is undefined and unknown to the player. I can potentially fix that issue by creating my own event handler, but all of this is seriously complicating a system that doesn't need to be so core to the game.<br><br>

## So, gut it?
I'm kind of debating how much I want to have an elemental damage system from a game design perspective at this rate. It was in my original prototype, but I'm kind of thinking that it might be more damaging than aiding. My biggest worry is agency - I do think elemental systems are more rewarding to pull off but you run a lot of risks I haven't really debated before. Say a weapon’s passive ability is great, but it also deals Fire damage. Suddenly, that great weapon becomes near-useless against enemies resistant to Fire-which undermines the fun and flexibility of your build. Additionally, you need to spend a lot more time grinding for weapons and armors for specific situations. Having trouble with a boss that deals a bunch of water damage because you didn't spec into it? You have two options: either over level yourself or grind for a kit you are going to use once. Both of these options are not good. It's like a kid playing pokemon and running all fire types, except you had no choice in that matter because you only rolled good fire types.<br><br>

I'm not saying that this problem is unsolvable or unbalanced - I'm more so weighing if I want to face it. I already have a load of balance concerns. Adding in a system like this could seriously cause headaches down the road. Add that to the combined element types, you're getting in the realm of overcomplication on a system I'm not too too married to.<br><br>

## But Eclara?
My main tie to it is, as I have mentioned a lot of times, Eclara's kit relying on it. I could redesign it, but her thematic would be drastically different as well. I could also change the system so that she applies status effects rather than element effects. Regardless, those are the design choices I'm weighing at the moment!<br><br>

There is also a big thing that I do like element types. However, I think the current issue is that I have two many. I don't like systems that rigidly define a single damage and resistance stat, as it also feels stiff in terms of gameplay. I do really like complicated element systems - Warframe being what I am trying to model after. It also greatly enhances customization, and I can alleviate agency issues through a system similar to the mod system in Warframe. What persists there are the balancing issues. I'm not sure!<br><br>

I'll stop here and move on to how this is all actually implemented.<br><br>

# In one file - that is!
Yes, all element damage is handled in a massive 1.5k line file! This was a poor organizational decision that stubborn little ol' me didn't want to falter on (oh naive me).<br><br>

Regardless, there are a few records that represent different elements. The main one is Element, which takes an ElementType enum as well as an ushort for the amount. The reason for a ushort is that I like only using what I need within memory, and I don't think that people will be able to stack high enough to overload the ushort. Additionally, I don't need negative stacks, so it makes sense for it to be unsigned.<br><br>

The ElementHandler also has an ElementalEffect private abstract class. Each elemental effect inherits from this. Whenever the ElementalHandler receives new element types, it will update each elemental effect's stacks. Most of these elemental effects act as buffs or OnStart effects. What each of them do is pretty simple:<br>
- Fire - Health DoT<br>
- Ice - Slow decrease<br>
- Water - Resource/Mana DoT<br>
- Earth - Physical Res decrease<br>
- Wind - Physical Atk decrease<br>
- Light - Magical Res decrease<br>
- Dark - Magical Atk decrease<br>
- Celestial - Nothing!<br>
- Nature - Applies Fire/Water/Earth/Wind and has a special effect<br>
- Eclipse - Applies Light/Dark at a stronger rate<br>
- Frozen - Removes actions based on number of stacks<br>
- Cinder - Spreads to enemies<br><br>

Nature's special effect is that, on turn start, if the character's health percentage is greater than their resource percentage, they can only use actions. If it's the opposite, they can only use skills. They're unaffected if its equal, as it's balanced.<br><br>

Anywho, this all sounds really simple but it took a while to set everything up! For one, buffs weren't working properly at first, so I had to change a lot about that. I also had to update DamageInformation to know when and when not to track elemental information, which meant I also needed to update the attack functions. Needless to say, it was a bit of work! But at least it all works!<br><br>

# Next Week!
Unfortunately, this week wasn't all that fun. I'm sorry I didn't have any visuals to look at! Regardless, next week I'm planning to actually finish Eclara and work on charge. Once I get that I'll update the UI to show status effects and then work on AI designs a bit. Yipee!<br><br>
