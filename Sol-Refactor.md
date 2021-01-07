**Not yet live**

## Introduction
After months of talk, hinting at "something huge" coming soon, and a lot of uncertainly; the first part of the Sol Refactor effort has been released. There are a lot of things enabled by this work that might not be easily digestible by non-developers, so this article is an attempt to explain why this work has taken priority over everything else, and why you'll soon be reaping the benefits!

#### Technical Details
There is a mini technical guide to using Sol [here](https://github.com/topaz-next/topaz/wiki/Sol-Lua-Binding-Library). 

## Motivation

### Runtime Safety
<img src="https://user-images.githubusercontent.com/1389729/103868903-38b9ff80-50d2-11eb-985d-cf0e567ae285.png" width="600" height="300" />

Unless handled very carefully, if an error is encountered in C++; it will kill the server. Unless you're debugging or you're set up correctly to capture crash information this crash will be difficult to explain to devs. Even if you catch the crash, it can be hard to explain or understand unless you're comfortable with C++.

The more errors we can catch in the Lua layer before they make it into C++, the less crashes there'll be. If an error is encountered in Lua it will log all the information it has and then bail out of the current script; allowing the C++ execution to continue underneath it.

An added benefit of using Sol is that it validates the use of bindings at the Lua level. If you call `mob:takeDamage(x)`, but `mob` or `x` are nil/invalid; it won't make it into the C++. It'll log an error and operation will continue.

### Runtime Performance
<img src="https://user-images.githubusercontent.com/1389729/103868923-41aad100-50d2-11eb-80b7-abd2f6d29afa.png" width="600" height="300" />

Historically, a fast iteration time while writing scripts was preferred over performance. Every time a script is run (for the most part), it will be read off the disk. You can read about the comp-sci details [here](https://en.wikipedia.org/wiki/Memory_hierarchy), but briefly; reading a file off disk is much much slower than reading it from memory. If we have 10 players, each in different zones, every mob in each of those zones will be calling `OnMobRoam` multiple times per second, each call linked to a file read. This is why performance is so heavily linked to your disk speed. Upgrading from HDD to SSD is the biggest improvement you can make to your server. SSD to Ramdisk is probably another good boost, but I've never tested it.

<img src="https://user-images.githubusercontent.com/1389729/103680388-c8ef2c00-4f8e-11eb-8632-f589d0d9f9b6.png" width="400" height="300" />

### Developer Quality of Life
<img src="https://user-images.githubusercontent.com/1389729/103868938-47a0b200-50d2-11eb-8557-c4c3b9319cfe.png" width="600" height="300" />

All interaction between Lua and C++ before was handled manually. You would have to push and pull items off of the Lua stack, make sure you left the stack in a sane state when you were done, register function pointers, validate all arguments coming in and out of your bindings etc. It was scary for newcomers, and never got easier for people who were familiar with it.

Using Sol to handle C++/Lua interop is the difference between trying modify your car's engine while it's running to change gear, and asking your autopilot to take you to your destination. It's a night-and-day difference.

## What does this mean for my server?
This is a breaking change. Every single binding has been rewritten, every single mob script has been modified. We may or may not be changing every single effect/status script. We recommend you take the release and re-apply your changes over the top of it. Unless you have more time than sense, you won't be able to merge this into your current branches.

## Other Goodies
This work enables Lua modules. If you know what you're doing, you can start writing them _today_. If you're not sure, we'll have some examples out sometime soon.
