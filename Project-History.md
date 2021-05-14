**Info dump from Topaz Next migration:**

Readme TLDR
```
TLDR:
- Project Topaz shut down. Previous owners can't be contacted. We're moving on assuming they aren't coming back.
- Open source is important, that's why I've forked Project Topaz and rebranded as Topaz Next.
- It is important to have a repo and project that isn't tied to an active server.
- AGPL was causing too much heartache and too many fights. We're GPL. Just like the projects that we've forked from and rely on.
- Not accepting feature development right now, please work on your cool things in your own forks for a while.
- Go read the rest of the migration-read-only pages.
```

Why did Project Topaz fail?
```
Project Topaz is gone
I've been emailing back and forth with Discord help. I'm waiting to hear back from a supervisor of some sort; but it looks like the Project Topaz discord isn't coming back. I've tried to reach out to Zircon and Ibm, but I've only gotten radio silence back. From this point onwards I'm carrying on as if Project Topaz is dead and not coming back. I've backed up all of the information from Project Topaz git (repo, history, wiki, issues, PRs, patches). The scripts I wrote to take these backups will soon be available on GitHub and the backups themselves will live there too.

Since there are no other open source projects for providing FFXI server software; if I want to continue I'll have to fork a new one from Project Topaz.

I think it's very important to have a software option that isn't paired with an active server.

Why did Project Topaz die?
Many reasons. I wholly agree with the sentiment that DSP wasn't a nice place towards the end of its life, and that a lot of the behavior there was toxic. Project Topaz was spun up as an alternative option where those sorts of toxic behaviors wouldn't be allowed, and where people would feel welcome to come and develop. For a time that worked. 

Unfortunately, inter-server/inter-project drama, license fights, script-kiddy exploiters, demanding users, and even more demanding contributors led to an environment where staff got to do nothing apart from deal with unaligned incoming submissions and other people's inter-personal drama. It was very common for us to say to each other "I've gotten to do nothing this week apart from deal with this project drama". If you forced yourself past the project drama and added in the work you wanted to be doing on top, you'd be pulling 6+ hours a day. I did this for a few months, not sustainable even slightly.

This was too much for Zircon and ibm and they nope'd out, taking all of their things with them. I'm 1000% done with all of this crap and just want to move past it.
zach2good10/12/2020
Lost work
In the final month of Project Topaz we had a private dev-only repo where we were working on our stuff in peace. Me and Ibm got quite far. I've integrated my groundwork for swapping out our Lua binding system, and will shortly begin on rewriting all the bindings. Ibm was working on the fabled "20x performance improvement", which was ready to roll out in the days before he bailed. His work was planned on being AGPL-only, as bait to get people to start playing with the new license. I'm not, and will never be; comfortable releasing someone else's work under a different license. So the only option is to start from scratch.

Luckily, once my binding work is in, an implementation of the concepts behind his work will be sufficiently different, and will count as a standalone non-derivative work and can be under GPL. Unfortunately, this will take a long time as it was 30k+ lines of code.
zach2good10/12/2020
Licensing & Open Source
Open Source. It's what's for breakfast. Project Topaz had signed CLA's allowing it to relicense all submissions in the previous year from GPL to AGPL. This would have been incredibly powerful and, since a lot of the work was original and non-derivative, would have worked. Since I can't get ahold of Zircon to get him to allow me to represent Project Topaz, all of those CLA's are useless and all submissions default to being GPL3 (as stated in the license). 

I will not be expending extra energy trying to execute the "relicense to AGPL over time" maneuver. Unless you're willing to chase someone into court over a license breach, AGPL doesn't impart any additional benefits. I am entirely unwilling to go to court over any aspect of this project. AGPL is only sufficient, plausible and defendable if you've been AGPL from the first line of code onwards.

I could rant for hours about people passing off upstream work as their own, erasing contribution information, holding on to features "to get an edge" over other servers, claiming "security through obscurity" as a defense against bad actors, etc., but it would be wasted breath. Go read "the famous WoW post": https://github.com/FrancescoBorzi/why-I-hate-wow-private-servers/blob/master/ENGLISH.md
zach2good10/12/2020
AGPL
If you're interested, I did speak briefly with a lawyer from the FSF, asking about the interplay between GPL and AGPL in the same codebase. It is... not clear:
https://gist.github.com/zach2good/7fb3cde808ae5316e52861082e80f46d
```

Topaz Next
```
Topaz Next
Open source development is a heart-breaking slog through the trenches with very little reward, only taken on by masochists. 

We're working towards feature parity with the final released FFXI version. Since there currently isn't a final version, we'll keep chasing the current live version.

If you want to chase a different goal, you're encouraged to fork off. More competitors in the open source space makes better and more complete software for everyone, especially if we're all operating under the same license. 

We will continue to not approve of the passing around out-of-date DAT files. If you want to deal with old or custom DATs, please do it somewhere else.
zach2good10/12/2020
Repo
 Currently private, there are a few operations I want to run on it and a few settings I want to tweak before I open it. Rain or shine, it'll be public this weekend. 

Link in #resources
zach2good10/12/2020
This Discord
Drama, "stirring the pot", random speculation about Project Topaz, trying to get a rise out of anyone etc. will be met with a swift ban.
```

Logos + Names
```
zach2good08/12/2020
From the Topaz License
    c) MISREPRESENTATION.
    The origin of this Program must not be misrepresented. You
    shall not claim, suggest, nor imply you wrote this Program, 
    in whole or in part, unless you are the original author for 
    the distinct part for which you claim to be the author.

    If you convey modified versions of this Program, you may not 
    misrepresent that modified Program as being "Project Topaz", 
    unless that modified Program is being conveyed back to 
    Project Topaz with the intention of the modification's inclusion 
    into the project.
    
    If you convey modified versions to recipients other than Project 
    Topaz, you shall mark the material such that any users interacting 
    with the Program are given notice - through an applicable player 
    interface of your choosing - that the Program has been modified 
    from its original version, unless that modification was necessary 
    for the basic operation of the server.
zach2good08/12/2020
For sure this means we'd need new name and logos
zach2good09/12/2020
Found a nice placeholder logo
zach2good09/12/2020
Quite keen on TopazNext, allowing us to keep all "topaz" internal branding
If you convey modified versions of this Program, you may not misrepresent that modified Program as being "Project Topaz"
^ We won't be, it'll be Topaz by TopazNext, including the same program names (with different icons)
zach2good10/12/2020
Paying a designer friend in pizza and beer to design new logos, but I really like the random one I found online. Might look at how much it costs to buy it...
```

Code + Development
```
zach2good10/12/2020
Paraphrased from my "community statement" in the end days of Topaz:

How open source works:
I’m not a fan of “memeing” on people in place of having an actual discussion over things that are wrong. Sarky comments in PR descriptions and whining in shared Discords doesn’t solve problems.“Poop emoji” on an unpopular statement helps nobody. However, all of the problems I’ve been listed are summed up so perfectly in this TikTok, I can’t help but want to post it every time someone makes unreasonable demands of us:

https://twitter.com/EmilyKager/status/1321603336051789824

Our tech vs a full rewrite:
There is often bashing of our current technology stack (C++/Lua/SQL), saying that it’s bad and we can do xyz better with another shiny set of technologies. Stating that a nuclear rewrite is better than progressive rewrites and some sustained engineering. I question the motives of anyone making these claims. Our stack can 100% take us all the way to the “finish line”, if such a thing is fathomable. I’m not saying that other technologies aren’t up to the task, but there is no reason other than vanity to consider a full rewrite. 

There are however usage patterns that are crippling us.

The way we call Lua scripts - garbage.
The way we pass data between Core and Lua - horrible.
Abuse of global state for Lua scripts - laughable.
Performance and safety of Core - abysmal.
How people have to write quests split across different NPCs - a joke.
How it’s impossible to keep large customizations safe from upstream pulls - very poor. 
Constant bouncing between Core and Lua - awful.
Database access patterns and hammering the disk - real bad.
Development
Starting priorities will be setting up the new repo and making headway into fixing these usage patterns which are crippling us. If you want to work on cool new features or things for your own servers, by all means please continue to work on what you enjoy - in your own fork. Please remember that if you submit that work to us, it will be heavily de-prioritized (to the point of being ignored) if it is going to take any resources away from the important work.

- Version updates, exploit fixes and dangerous/repeatable crashes are always important.

- We will consider obvious and easy to understand bugfixes, that have been well-documented, well-explained, coded cleanly, and well-tested.

- In no particular order, the following are not important (for now): Fights being unbalanced, adding new fights, balancing/expanding Trusts, filling in content (records, shops, spells), quests not being completable, new features, etc.

Bugs and issues
It's taking a while to figure out a good and clean way to import all of the backed up issues from Project Topaz into the new project. Please don't open any new ones until I've figured this out!

Exploits
The private exploit discord is still active, message me if you're a server operator and need access. One member per server, unless you're massive like Eden.

Support through PMs
I will continue to aggressively forward private support requests back into #development, the only stupid questions are ones that nobody else can learn from.
zach2good10/12/2020
Contributing
Since there is only the smallest of skeleton crews at the moment, there is very little manpower available for reviews and testing. Please limit your PRs to things I've listed above.

It's also ALWAYS incredibly helpful for people to jump onto retail and capture things. Damage, mechanics, resistance testing, quests, missions, move IDs etc. Always welcome. Link to capture discord in #resources
```

TODO + Roadmap
```
zach2good10/12/2020
TODO

Repo
- Maybe change the name, I've seen people have to make forks as topaz-1 - Nah, too late now
- Clear out remaining Project Topaz specific things
- Finalize clang-format rules, run on entire codebase
-  potentially using clang-format-11 for lambda rules) - Doesn't work :(
- Take small subset of clang-tidy "auto-fix" rules, run on entire codebase (braces, override, nullptr etc.)
- Set up sonar again 
- Clear out remaining vulnerabilities and security hotspots
- Fix builds for all platforms and update CI
- Open the repo to the public (by this weekend, even if <conditions> aren't met or it isn't ready)
- Cut an end-of-year release
- Import issues from Project Topaz
- Restore and rebrand Wiki
- PacketGuard has been running on two servers for a while with no bugs, turn on by default.
- Rebuild canary from tidy'd, updated and formatted release
- Clarify what's in release vs canary (Looks like just Magian and formatting...)

Discord
- Roles
- Bots
- Sweet emojis
- Mandatory landing page

Meta
- Rules
- Code of Conduct
- CLA
- License Clarifications (GPL vs AGPL vs old-Topaz License)
- Roadmap
- Submission rules
- Better guidance on what submissions can/should be made right now
- Define when "Open submissions" will be considered
- "Doomsday" plans

Drama
- No, bad dog, not addressing any of this. Good vibes only.
zach2good14/12/2020
Roadmap
High level project roadmap is now available to view on GitHub:
https://github.com/LandSandBoat/server/projects/1
```