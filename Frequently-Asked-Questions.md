## What is Darkstar Project / DSP?
Darkstar Project was the most-recent FFXI server codebase which Project Topaz forked from. It is no longer being developed.

## What works? Is quest X implemented?
https://github.com/project-topaz/topaz/wiki/What-Works

## Canary? Release?
Project Topaz maintains two long-term branches: `release` and `canary`. `release` is the default branch and contains changes that have been vetted and tested. Human error can always occur, but this is the most stable place to get code. `canary` ([origin](https://en.wiktionary.org/wiki/canary_in_a_coal_mine)) is based on `release`, but contains our `feature` branches and experimental content. It is for testing and is not guaranteed to be stable. Think of it as the "beta testing" branch.

## When will feature X arrive?
We practice [clean room engineering](https://en.wikipedia.org/wiki/Clean_room_design), which means we have to implement everything from scratch. As such, progress is slow. We are also trying to balance feature development, bugfixes, performance improvements, exploit resolution, code review, and testing.

## Can I pay someone to implement feature X?
We will never accept financial or material incentives for our work. This is a hobby project. External incentives would drive developer and staff time in a way that makes it no longer a hobby.

## The code for feature X is available in the community, why haven't you taken it?
Features in Project Topaz are those that have been submitted to us, meet our standards for quality and accuracy, and that we have had the time to review and integrate with the rest of the codebase. It is very rare that we will accept code on someone else's behalf. While there is technically nothing stopping us, it would undermine our position in the community.

## I heard Topaz is interested in modules and customization?
_"When the rest of the codebase isn't on fire."_ ~ibm2431

## Can I change job X to play like job Y?
No.
<details>
<summary>Read more</summary>
<p>

You can check in the #customization channel, but _many many_ things are enforced by the game client.
For instance; you can set your jobs to be 75NIN/75BLM but you won't be able to equip Lv75 BLM gear - this is enforced by the client.
Bypassing these restrictions would need heavy client modification (which we don't support) or support scripts.

</p>
</details>

## Where is fishing?
Not yet implemented. See: [What Works?](https://github.com/project-topaz/topaz/wiki/What-Works)

## When can I play "Classic" Dynamis?
You can't, it isn't in the game anymore.
<details>
<summary>Read more</summary>
<p>

"Classic" Dynamis was removed from the game in 2011. The spawn mechanisms as you remember them are gone from the game, and those zones no longer act the way they used to.
The overall project goal is to emulate the retail game as closely as possible, so a massive custom solution to approximate "Classic" Dynamis is not on our roadmap.

However, in 2017 Dynamis Divergence was released, a content level 149 version of the "Classic" Dynamis players wanted to experience again.
If we were to support a custom Dynamis solution, it would be the implementation of Dynamis Divergence and a set of mods or switches that scale it down to level 75 era difficulty.

Keep in mind that we haven't completed all content up to 2007, so a full implementation of content from 2017 with mods on top isn't coming any time soon. 

</p>
</details>

## Why is the airship in Sauromugue Champaign skidding along the ground like a land speeder?
[It's a feature, not a bug.](http://project-topaz.com/issues/10) 👀
