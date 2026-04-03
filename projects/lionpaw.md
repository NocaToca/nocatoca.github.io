---
layout: project_page
title: Lionpaw
permalink: /projects/lionpaw/
---
<div class="content-row">
    <div class="text-block">
        <h2>Brief Overview</h2>
        <p>Lionpaw is a Discord Bot made within C#. Its purpose is to help with the management of roleplay servers and provide tools to drive member engagement. The bot features moderation tools, character parsing, user role playing statistics, among other fun features like a built in gacha system. At its peak, the bot managed around five different discord servers for a total user base of around five hundred people.
        </p>
        <p>Some technical features include:</p>
        <ul>
            <li>Async C# with DSharpPlus.</li>
            <li>Basic persistent JSON data storage.</li>
            <li>Discord, Google, and real-world Weather API integration.</li>
            <li>Document parsing to bring unstructured data into a structured format, utilizing regexes, language structure, and a fallback template-structure.</li>
            <li>Event driven architecture to respond to events in real-time.</li>
        </ul>
        <p>Some design features include:</p>
        <ul>
            <li>Customizable plugin/feature boggling.</li>
            <li>Multi-server scaling.</li>
            <li>Optional opt-in per user features .</li>
            <li>User retention tackling.</li>
        </ul>
    </div>
    <div class="image-block">
        <img src="/images/gpu_bht_rt.jpg" alt="Lionpaw">
    </div>
</div>

<div class="content-row togglable-row">
    <div class="image-block">
        <img src="/images/lionpaw_overview.jpg" alt="Lionpaw">
    </div>

    <div class="text-block">
        <div class="toggle-controls">
            <button class="toggle-btn active" data-target="design">Design</button>
            <button class="toggle-btn" data-target="technical">Technical</button>
        </div>

        <div class="view-content design-view">
            <h2>Synopsis</h2>
            <p>I built Lionpaw originally to help one of my friends flesh out their Warrior Cats RP server - hence the name “Lionpaw”. The actual substance of the roleplaying content became inconsequential once I ported the framework to another friend's Pokémon themed server, but the name stuck since it became a joke within our group.</p>
            <p>For those unfamiliar with role-playing, a helpful correlation that is mainstream is that it's a lot like Dungeon and Dragons. Users create their own character(s) and interact with each other to create a developing story playing as those characters. While this can be done through voice, the medium that is more popular (and the medium Lionpaw was created for) is text. These laid the foundation of what Lionpaw did.</p>
        </div>

        <div class="view-content technical-view" style="display: none;">
            <h2>Synopsis</h2>
            <p>I used C# and DSharpPlus since I was already familiar with it (see Mistwalkers) and C# is by far my favorite language. The specific version I used was Nightly 4.0.0, since it had just come out. This did also cause a good amount of challenges, since documentation on the new version was limited. I relied a lot on browsing through their example code as well as reading through what API features NuGET provided.</p>
            <p>Despite running on five different servers, I did not utilize shards (which is a discord term for splitting the bot into multiple processes). The bot was hosted on a single process within my server computer. The bot would adapt the given commands and choice providers based on the Guild (or Server) that the interaction context was spawned from.</p>
        </div>
    </div>
</div>

<div class="content-row togglable-row">
    <div class="image-block">
        <img src="/images/lionpaw_overview.jpg" alt="Lionpaw">
    </div>

    <div class="text-block">
        <div class="toggle-controls">
            <button class="toggle-btn active" data-target="design">Design</button>
            <button class="toggle-btn" data-target="technical">Technical</button>
        </div>

        <div class="view-content design-view">
            <h2>Core Features</h2>
            <p>Lionpaw's features were sectioned off into modules, of which server owners could enable or disable to customize their experience. For instance, Lionpaw had built in moderation features, but if server owners already had a more popular moderation bot (E.g. Carl Bot), they can disable this module entirely. This can be done at any time, but was typically recommended when it was first added to a server.</p>
            <p>The core features that defined Lionpaw include character management as well as automatic document parsing. These two features were the most utilized features of Lionpaw, as it streamlined user management within the server.</p>
            <p>Most roleplay servers have users submit character ideas and concepts for approval. The most common practice was to create all your character information in a Google Document or PowerPoint, of which the server's staff team can review for accuracy or any offensive behavior. As it can be imagined, this can be a time consuming process, and it can be hard to track characters that have already been approved and that have yet to be approved.</p>
            <p>Lionpaw alleviates both of these issues by automatically parsing the Google Document and grabbing all relevant information about the character before categorizing them and stashing them in its database. Lionpaw stores standard fields like the character's name, gender, and owner, all of which can be queried by anyone by interacting with Lionpaw. This can also be helpful for server administrators, as they can very easily see statistics regarding guild coverages, user characters, as well as if a name is already taken.</p>
            <p>Lionpaw also had a weather feature, which server owners could set to monitor a specific weather station on Earth. Lionpaw would then query that station before deciding pseudo randomized weather that would make sense for that area. This helped users have more to roleplay around, as they can refer to Lionpaw's given weather to have an idea on how to create a scene.</p>
        </div>

        <div class="view-content technical-view" style="display: none;">
            <h2>Core Features</h2>
            <p>Server owners can adaptively enable or disable different commands and features of Lionpaw. This reduced bloat for servers and allowed for server owners to request more specific commands, since discord only allows 50 guild specific commands. Because Lionpaw was not a general discord bot (meaning that all commands required context around the Guild it was in), all commands besides setup and these module enabling commands are registered as guild-specific commands. Guilds could also set a ‘theme’ for any given server, which would change Lionpaw's behavior.</p>
            <p>The most used feature that Lionpaw provided was document parsing. Core fields that were included for every server included name, age, gender/pronouns, and birthplace. Lionpaw approached each of these in a unique manner. For instance, Lionpaw would search for a character's name by categorizing each discovered noun, then filtering based on known lore (E.g. locations that server owners defined) and then concluding that the leftover most used noun has to be the character's name. Of course, Lionpaw would sometimes make mistakes. To combat this, it would preview the information that it was going to put into its database so that server admins could verify and make any necessary changes beforehand.</p>
            <p>Based on the theme of the server, Lionpaw would search for additional information. For instance, in a Pokémon server, Lionpaw would find what Pokémon the character was by using regexes on nouns to find potential Pokémon. Guild owners could also add information on what to search for, of which they can define how Lionpaw would search for it. For example, if you had a Harry Potter server, you can add a “school” parameter and have Lionpaw search based on keywords like “Ravenclaw”. Lionpaw would fallback to regex based searching, where it would search for instances where "school" and any noun were mentioned in the same sentence, then choose the noun.</p>
            <p>Server owners could have Lionpaw monitor a weather station on Earth and set a date that they wanted Lionpaw to mimic. Lionpaw would then query that day across various years and use a standard distribution to generate random temperature, humidity, rainfall, and cloud coverage for the area. It would also occasionally generate storms based on this information.</p>
        </div>
    </div>
</div>

<div class="content-row togglable-row">
    <div class="image-block">
        <img src="/images/lionpaw_overview.jpg" alt="Lionpaw">
    </div>

    <div class="text-block">
        <div class="toggle-controls">
            <button class="toggle-btn active" data-target="design">Design</button>
            <button class="toggle-btn" data-target="technical">Technical</button>
        </div>

        <div class="view-content design-view">
            <h2>User Experience</h2>
            <p>Another big aspect of Lionpaw is that it gives users an easy way to track their own statistics and roleplays. Users that opt-in to statistics tracking can see fun stats like their favorite words and punctuation to use, their most played and played with character/user, and how many words they have typed. Another feature was that it would notify users when it was their time to respond to a roleplay, and remind them according to their preference.</p>
            <p>One server also requested a gacha system, of which users can use tokens they obtain by participating to roll for characters. This became probably the most popular user feature of Lionpaw, as people really enjoyed pulling and comparing their database of characters. Players could also use their pulls in integrated games. An example is that a user's pulled characters could be assigned to manage a shop, of which other users could interact with. </p>
        </div>

        <div class="view-content technical-view" style="display: none;">
            <h2>User Experience</h2>
            <p>Users can see their roleplaying statistics per server and across all servers that use Lionpaw. Upon sending a roleplay message in an active roleplay, Lionpaw would spawn a thread to parse that roleplay. It would store each word to a dictionary as it deciphered additional information about the reply. Then, it would retrieve the user's current information, append it, and then save it. Since this operation was memory intensive, only three threads were allowed to work at any given time - with the rest being put in a semaphore.</p>
            <p>The gacha system was, in its entirety, pretty simple. Upon creating a character or sending a roleplay message of sufficient length (configurable by server owners), it would give users a token which would then allow them to pull any registered gacha character from the database. Since some users were uncomfortable with the idea of their character being pull-able, this was also an opt-in experience.</p>
        </div>
    </div>
</div>

<div class="content-row">
    <div class="text-block">
        <h2>Moderation Features</h2>
        <p>Lionpaw held a database of problematic users that servers could report, and then notify other server owners if those problematic people joined. Other moderation features included hateful language detection as well as tracking nickname and profile picture changes. </p>
    </div>
    <div class="image-block">
        <img src="/images/gpu_bht_rt.jpg" alt="Lionpaw">
    </div>
</div>