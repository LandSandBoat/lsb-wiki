NOTES: Image sizes: 720x300

_As always, remember that all private server software is maintained by teams of volunteers, for free, as a hobby._

![image (5)](https://user-images.githubusercontent.com/1389729/146537901-c29c2239-3df7-4d8f-bc8a-99ef0e556691.png)

`The eponymous Land-Sand-Boat, in case you were wondering`

Hi there! It's me, zach2good, here to talk about what LandSandBoat (LSB) been up to over the last year and what we have planned for the future. I'll be talking about a mix of things that have landed, things that are in-progress, and things that are planned.

Before we begin, I'd like to thank everyone who contributed to LSB this year. Code, knowledge, debugging, reporting about balance, reporting bugs. It's all important! (in no particular order, taken on March 2022)

TODO: Refresh this list
```
59blargedy, Bope, Brierre, Chris Manigan, Corey Sotiropoulos, Daniel Papenburg,
David Norris, DropletXI, EpicTaru, Era-Lusiphur, FFXI Wings, Flam99, Fleme,
FuzzyWereBeast, Ganiman, George and Wendy, Helix Hamin, InoUno, Ixion, Kain,
Kietsu3756, KnowOne134, Kreidos, Marian Arlt, Mark Klara, MrHappyAsthma,
MrSent, NeuromancerXI, Prathen, RAIST5150, Shiyo, Skerxan, Snuggles, Snugglesffxi,
Sylvain Santucci, Tal Ben-Eliezer, TeoTwawki, Tokenr, Twilight, Tyler Schneider,
Vaughan Hilts, Velyn, Vinny M, Xaver-DaRed, Zach Toogood, beauxq, bope12,
claywar, gweivyth, hookstar, jefferyrlc, kain, kaincenteno, mikeyuzu, rude-jerk, wrenffxi
```

Special thanks to:
```
atom0s, Thorny, Rubenator, TheWhaler, Nyu, xenonsmurf, Velynn, jmcmorris, Godmode, Wiggo, Ashenbubs, eyes-and-brain,
Everyone who uploads captures, Everyone who reports bugs, Everyone who plays
```

# General Stats

TODO: Refresh this

| <!-- -->    | <!-- -->    |
|-------------|-------------|
| Files Changed | 58,822    |
| Lines Added   | 438,930   |
| Lines Deleted | 297,898   |
| Commits       | 2,621     | 

_*NOTE: These stats are taken from the start of the year and include contributions from Topaz-Next. The majority of contributors came over when Topaz-Next closed and continued their projects with LSB, so I feel like these stats are fair. Lines-of-code isn't a good measure of much anyway :)_
 
# Content & Balance

## Content Rewrites

With a new interaction framework (more on this later), we figured it was time to pull apart most of the mainline missions that we currently have and rewrite them to fit this newer, more understandable, and easier to maintain format.

These include:
- All Sandoria Missions
- All Bastok Missions
- All Windurst Missions
- All Rise of the Zilart Missions
- About half of Chains of Promathia Missions
- Nearly all Treasures of Aht Urghan Missions (45/48)
- Chapters 1 & 2 of Seekers of Adoulin
- Rhapsodies of Vana'diel Missions up to start of Chapter 2

## Wings of the Goddess

![image (6)](https://user-images.githubusercontent.com/1389729/146539932-149aaa7e-625a-4c6a-88c8-b4827d3bb8d7.png)

- Mainline missions 01-13 ([#128](https://github.com/LandSandBoat/server/pull/128), [#486](https://github.com/LandSandBoat/server/pull/468), [#1101](https://github.com/LandSandBoat/server/pull/1101))
- Some packet work for Campaign ([#174](https://github.com/LandSandBoat/server/pull/174))

## A Moogle Kupo d'Etat

![image (7)](https://user-images.githubusercontent.com/1389729/146540652-2bb2a106-41de-4a27-8688-65f336c6b35b.png)

- Missions 01-08 ([#278](https://github.com/LandSandBoat/server/pull/278]))
- char_history, and plumbing for AMK quiz game ([#267](https://github.com/LandSandBoat/server/pull/267))

## Abyssea

We have a branch for Abyssea being worked on by claywar, building on the work of TheWhaler and MrSent, currently sitting a +10,800 lines of code. It's now being pulled apart to be drip-fed into the main branch.

## Seekers of Adoulin

![image (2)](https://user-images.githubusercontent.com/1389729/146524090-7cba22c6-bf1b-4c2a-a345-c9dbb9337883.png)

- Missions 1-1 to 2-7-3 (Chapters 1 & 2)
- (in progress) Colonization Reives [(PR)](https://github.com/LandSandBoat/server/pull/1091)
- Runefencer (we rescued some abandoned work from old projects and started [](https://github.com/LandSandBoat/server/issues/1340)
- Geomancer (some geomancer aura work, but nothing for the job :()

## Battle Content

-

## Hobbies

### Crafting Recipes

Back in Topaz times, many recipes were disabled, for several reasons, like... Recipe levels or resulting items not matching wikis, several being non-retail/custom recipes and even some obscure recipes used to exploit the system and level up skills easily.
The idea behind it was to slowly audit them while also saving some trouble to server operators.
Many recipes have been audited and re-enabled since then and many more will come.

### Mannequins

![image (4)](https://user-images.githubusercontent.com/1389729/146525229-d96b695e-ea98-47f9-ac8d-5e55a753bb4d.png)

Even though you can't obtain all the pieces of a Mannequin through natural play, the quest exists and you can have one in your Moghouse - if you so please. [#429]((https://github.com/LandSandBoat/server/pull/429)

### Chocobo Raising

![image (3)](https://user-images.githubusercontent.com/1389729/146524881-bb10ff30-1624-4380-a632-5f146281af1a.png)

A heavy work in progress, but the building blocks are coming together nicely. I won't put a timeframe on when I'll push this into the main branch, but at this pace, it'll be before 2023 :eyes:. [#1058](https://github.com/LandSandBoat/server/pull/1058)

## Additional Effects Rework

We had the same set of redundant function calls and conditional logic in 158 scripts, and the future problem of augments granting additional effects. It didn't make sense to continue doing them per item and then have every item ask "am I augmented? should I consult a doctor developer?" so now that is all one script and nobody has to copy paste to add new items - just set the modifiers!

[#730](https://github.com/LandSandBoat/server/pull/730)

# Technology & Tooling

I feel like this has been the area where we have focused most of our efforts. We are hellbent on transforming this codebase into something that is clean, easily maintained, easily built, and will support developers, operators and players long into the future.

## Important Fixes
- CS Blackscreens (fixed as part of the interaction framework)
- Navmesh latency reduction (48%-82%) [#294](https://github.com/LandSandBoat/server/pull/294)
- Reduce packet pressure in high-entity-density areas [#597](https://github.com/LandSandBoat/server/pull/597)

## Sol Refactor
- Link to article, mention performance gains and benefits of the Lua Cache

## Stability

There were many many crashes

Packet sizes [](https://github.com/LandSandBoat/server/issues/1253) [](https://github.com/LandSandBoat/server/pull/1255)


## Module System

A work in progress for many months, it finally landed in the last few weeks. This allows simple, runtime overriding of any scripting function we have, while retaining access to the original. This means you can disable, replace, or extend anything that goes through the scripting layer.

## Dynamic Entities

Following on from our work on Trusts, and with some guidance from atom0s, it is now possible to rename any entity in the game without needing any plugins. We are also no longer bound to overwriting existing NPCs or Mobs if we want to make custom content. We can spin them up on the fly and insert them into any zone, at any time. `!fafnir`.

## Instance Refactor
Unstable and hard to 

## Interaction Framework
[repo](https://github.com/InoUno/interaction-framework)

## Improved update tooling

## Improved CI and Build Tooling

![image (8)](https://user-images.githubusercontent.com/1389729/146542397-a092b42d-1614-4856-b956-a96de01324ee.png)

The program is useless unless it builds and runs. It's just as useless if it builds and runs with a sea of errors on startup. That's why we've automated these checks for every build of every commit.

- OSX Support
- Incoming upgrades to ZMQ
ZMQ is fabulous, and will be the subject of a deep dive article some time next year.
- Incoming upgrades to LuaJIT

## HeadlessXI

In addition to checking that the server starts up OK, there is a lot of logic that fires when a player logs in. Thats why we adapted [bope12's PacketFFXI](https://github.com/bope12/PacketFFXI) into [HeadlessXI](https://github.com/zach2good/HeadlessXI) - a headless client written in Python that allows us to log into the server without a full client. It is still very barebones, but has been invaluable for catching issues.

## Lua Linting

TODO: Factcheck

This year we re-enabled luacheck. It has apparently been set up in the repo for many years with all the checks turned off. We switched as many of the sane ones back on as we could stand and we got to work. claywar has been diligently hammering away at the warnings and has taken them from 9000 all the way down to around 16.

## Logging improvements

Logging is important. You should be looking at your logs. When you write a feature, it should have lots of logging (with options to filter it out if needed :eyes:). But, what if that logging was slow? What if it took longer to print a single log line than it did to update some information about a character's battle state?

Thats why we swapped out our logging solution for something industry-standard, fast, and battle-tested. Netting a logging latency reduction of **over 99%!**

[#522](https://github.com/LandSandBoat/server/pull/522)

## Stacktrace logging on Windows

If you do encounter a hard crash, it can be hard to track down what was going on at the time so you can report it. That's why we've hooked up pretty printing of stacktraces on Windows.

![image (9)](https://user-images.githubusercontent.com/1389729/146544008-0bd9b703-7d31-4aeb-8377-f56d77041a4f.png)

## Refreshed update tooling

Every month a dark shadow looms over us. A monthly update lands and proceeds to stop us in our tracks for an undetermined amount of time. Sometimes it's just some ID shifts, sometimes packet definitions change and we have to scramble to stop clients from crashing.

Our old update tooling was written in Java, PHP, bash, and a myriad of other languages. Split between multiple people, or sometimes just one person was the sole owner of a vital tool we needed to handle updates.

We've rewritten the majority of our tooling in Python and we're no longer _quite so scared_ of what horrors the monthly update will bring us.

[repo](https://github.com/zach2good/UpdateExtractor)

## xiloader

Poor xiloader has been left to rot. We recently picked it up and started combing through it for easy wins. It won't take us long to give it the refresh it deserves and add features that have been missing for a long time, including:
- Building depenencies from source
- TLS support for secure communication
- Additional support for multiboxers

[repo](https://github.com/LandSandBoat/xiloader)

# Meta & Support

## GitHub

We are pretty tied to GitHub, and we have no plans of going anywhere else. If there is a limit on the amount of CI time you are given, we've never gotten close to hitting it. We never have to wait for instances. We like the PR workflow. The integrated wikis are pretty good. Discussions are still a work in progress, but we prefer it to the alternative.

## Documentation

### ADLs

Starting with the sol refactor, we started writing ADLs (Architectural Design Logs).
- ZMQ
- Sol + Lua (LuaJIT)
- Dynamic Entities

### Support Docs

In the last couple of months we have noticed that some of our documentation is out of date and needs a refresh. This is very much on our radar and we'll tackle it in the new year. We want to clarify:
- What platforms we support
- What platforms _might_ work
- What content works, and to what extent
- How to set up your server for a couple of people vs hundreds of people

## Public Discord

We don't have one, and we will continue to not have one.

## Move towards being brandless

We think there is no place for branding in this project. It is tasteless and vain to leave your name all over a public codebase that is already backed by git.

### Commands Used
`git shortlog -s --since="01 Jan 2021"`

`git log --shortstat --since "1 year ago" | grep "files changed" | awk '{files+=$1; inserted+=$4; deleted+=$6} END {print "files changed", files, "lines inserted:", inserted, "lines deleted:", deleted}'`

`git rev-list --count --after="Jan 1 2021" --all --no-merges`
