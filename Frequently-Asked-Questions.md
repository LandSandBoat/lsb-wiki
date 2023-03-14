## What works? Is quest X implemented?

[What Works?](What-Works)

## How can I help the project?

[How can I help?](How-Can-I-Help)

## Do you have a Discord I can join?

We prefer to work through GitHub [Issues](https://github.com/LandSandBoat/server/issues), [Pull Requests](https://github.com/LandSandBoat/server/pulls), and [Discussions](https://github.com/LandSandBoat/server/discussions).

## Can anyone run their own private server for Final Fantasy XI?

While technically yes, anyone can run their own server as the software required is entirely free and open source, it is not recommended. In order to create your own server, you will be required to understand how to install and use several various tools that are needed in order to run the server. This includes things such as running tools from the command line, understanding how to use and operate an SQL database, understanding how to compile source code, and more. In order to make any kind of changes to the server once its setup, you will also need to understand how to do some level of programming depending on the changes you wish to make.

## What programming languages are used to work on a private server?

The current core languages used with the main fork of the server software are:

  - C/C++ - Used for the main server core code and other core tooling such as the boot loader.
  - Lua - Used for the server scripting system.
  - SQL - Used for the database.
  - Python - Used for additional tooling.

_While you do not need to know every one of these languages, depending on what you are looking to modify you will need some experience in them at least. Additional languages may be required for individual private servers that you may look to help in regards to things such as their own websites, launcher, etc._

## What is the current software used for creating a Final Fantasy XI private server?

Private servers for Final Fantasy XI are made entirely through homebrew code (using mixes of the above aforementioned programming languages). **We do not have any kind of official source code or other material from SE.**

The current actively maintained fork of the private server emulation software is called: **LandSandBoat** (you are currently reading the wiki for **LandSandBoat**).

## I need help setting up my server!

Firstly, please understand that we **DO NOT** encourage for everyone to make their own private server. If you are not familiar with the requirements to setup the server or do not understand how to follow the instructions given, then we do kindly ask that you play on an existing server instead.

If you do feel as though you understand what you are doing and potentially have hit an issue with the given instructions, then you should first ask for help directly on the **LandSandBoat** [Discussions](https://github.com/LandSandBoat/server/discussions) page.

You can also ask for help within the **#dev-support** channel of the Final Fantasy XI Private Servers [Discord](https://discordapp.com/invite/msACzWV). But please be aware, if you are asking extremely basic/general questions in regards to setting up the server software that show you do not actually know what you are doing, you will most likely be ignored.

## Where can I find servers to play on?

Check out the Final Fantasy XI Private Servers Community [List of Servers](https://github.com/XiPrivateServers/Servers/tree/main/servers). You can also head to the [Discord](https://discordapp.com/invite/msACzWV) & [Reddit](https://www.reddit.com/r/FFXIPrivateServers/).

## Is there a GM command that does X?

All available GM commands, with descriptions and the level of GM they require, can be found [here](https://github.com/LandSandBoat/server/tree/base/scripts/commands).

## When will feature X be completed, when will bug Y be fixed?

We practice [clean room engineering](https://en.wikipedia.org/wiki/Clean_room_design), which means we have to implement everything from scratch. As such, progress is slow and difficult. We are also trying to balance feature development, bugfixes, performance improvements, exploit resolution, code review, and testing.

This project is maintained entirely by volunteers in their spare time. We can't and won't ever guarantee any timelines for features or bugfixes. Sometimes the maintainers have lots of time to work on the project, sometimes they have none, sometimes they just don't feel like it and want to go outside and touch grass instead.

The fastest way to get new features or bugfixes is to roll up your sleeves, get in there, and start working on them :)!

## Can I pay someone to implement feature X?

We will never accept financial or material incentives for our work. This is a hobby project. External incentives would drive developer and staff time in a way that makes it no longer a hobby.

## The code for feature X is available in the community, why haven't you taken it?

Features in LandSandBoat are those that have been submitted to us, meet our standards for quality and accuracy, and that we have had the time to review and integrate with the rest of the codebase. It is very rare that we will accept code on someone else's behalf. While there is technically nothing stopping us, it would undermine our position in the community.

Similarly, sending us code snippets creates more work and strain on staff and developers. If you have code you want to contribute, please speak to us with GitHub Issues, Discussions, and open a Pull Request.

## Can I use Trust: X, why doesn't Trust: Y do anything?

Go check their status [here](Trusts).

## When can I play "Classic" Dynamis?

You can't - it isn't in the game anymore.

<details>
<summary>Read more</summary>
<p>

"Classic" Dynamis was removed from the game in 2011. The spawn mechanisms as you remember them are gone from the game, and those zones no longer act the way they used to.

The overall project goal is to emulate the retail game as closely as possible, so a massive custom solution to approximate "Classic" Dynamis is not on our roadmap.

</p>
</details>

## Can I change job X to play like job Y, Can I create an entirely new job?

No.

<details>
<summary>Read more</summary>
<p>

There are _many many_ things are enforced by the game client.

For instance; you can set your jobs to be 75NIN/75BLM but you won't be able to equip Lv75 BLM gear - this is enforced by the client.

Bypassing these restrictions would need heavy client modification (which we don't support) or support scripts and changes in core.

</p>
</details>

## Why isn't Yell/Trust/Auction House etc. available in every zone?

What's available to use per-zone is controlled with the `misc` flags column in `zone_settings.sql`. These flags correspond to the `ZONEMISC` enum in `zone.h`. A query to modify those flags can be found in [Useful SQL queries](Useful-SQL-queries#enable-zonemisc-features-everywhere).

<details>
<summary>Read more</summary>
<p>

```cpp
enum ZONEMISC
{
    MISC_NONE       = 0x0000,   // Able to be used in any area
    MISC_ESCAPE     = 0x0001,   // Ability to use Escape Spell
    MISC_FELLOW     = 0x0002,   // Ability to summon Fellow NPC
    MISC_MOUNT      = 0x0004,   // Ability to use Chocobos and mounts
    MISC_MAZURKA    = 0x0008,   // Ability to use Mazurka Spell
    MISC_TRACTOR    = 0x0010,   // Ability to use Tractor Spell
    MISC_MOGMENU    = 0x0020,   // Ability to communicate with Nomad Moogle (menu access mog house)
    MISC_COSTUME    = 0x0040,   // Ability to use a Costumes
    MISC_PET        = 0x0080,   // Ability to summon Pets
    MISC_TREASURE   = 0x0100,   // Presence in the global zone TreasurePool
    MISC_AH         = 0x0200,   // Ability to use the auction house
    MISC_YELL       = 0x0400    // Send and receive /yell commands
};
```

</p>
</details>

## What is Darkstar Project (DSP), Project Topaz (TPZ), or Topaz Next (TPZN)?

These are the predecessor projects that LandSandBoat is derived from, which are archived and no longer maintained or supported.

## Why did the airship in Sauromugue Champaign used to skid along the ground like a land speeder?

It's the project namesake. It's a feature, not a bug. 👀

You can re-enable this using the [lsb_mascot.sql](https://github.com/LandSandBoat/server/blob/base/modules/custom/sql/lsb_mascot.sql) module.
