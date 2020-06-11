# Roll Call
aether, cocosolos, ibm2431, Nyu, Wiggo, Zircon
# Opening Remarks
> For community members who may not be aware, we have moved our meeting days to Wednesday to better fit in with staff's current schedules.

# Staff Updates

**aether**: Testing branches; will add numerous mob stats

**cocosolos**: Reviewing Pull Requests; submitting fixes; will work on hunts and database tools

**ibm2431**: Posted captures acquired during Return Home to Vana'diel campaign to Captures Discord; reviewing Pull Requests; broke up Geomancer Pull Request

**Nyu**: Capturing information from retail; has begun investigating Limbus

**Wiggo**: Assisting contributors with scripting; reviewing Pull Requests

# General Remarks
- Discussed need for moderating inappropriate animated GIFs which did not belong on Discord server, and if by the time Staff have been able to respond to these GIFs if damage has already been done
- Discussed possibility of preventing users from using `/tenor` and `/giphy`, and value those commands add to private server development
- Discussed Staff inherent reluctance to moderate messages and potentially upset community members
- Discussed automated moderation tools which may be employed to prevent usage of those commands, or automatically moderate messages which would begin divisive conversations in violation of server rules
- Discussed requirement for Staff having image embeds enabled adding more burden on Staff and upsetting Staff
- Discussed possibility of off-topic channel, or automated tools which can delete messages reported by community members
- Demonstration of automated moderation tools did not work during meeting, but was corrected after the meeting; automated tools will delete messages containing proper names of prominent political figures, religious groups, and racial slurs; automated tools do not take action on usage of `/tenor` and `/giphy` at this time
- Zircon informed of changes to Pull Request review process; Pull Requests with more than 1,000 net additions will not be brought up during a Staff meeting until at least two weeks old; free holds may be used up to four times on such Pull Requests; [community members encouraged to submit work more often or in multiple pieces](https://github.com/project-topaz/topaz/blob/release/CONTRIBUTING.md#pull-request-contributions)

# Pull Requests (6)
1. [#548 - Pathfind fix for Novalmauge](https://github.com/project-topaz/topaz/pull/548)
    - Held (ibm2431): Desires changes
2. [#638 - [FIX] Remove 1 day wait for Ranperre's Final Rest quest](https://github.com/project-topaz/topaz/pull/638)
    - Held (cocosolos): Desires changes
3. [#662 - Fixes crystal drops for parties](https://github.com/project-topaz/topaz/pull/662)
    - Held (cocosolos): Desires changes
4. [#672 - Winsock Updates](https://github.com/project-topaz/topaz/pull/672)
    - Merged into `winsock-updates`
5. [#688 - Compiler updates - cmake/makefile.am](https://github.com/project-topaz/topaz/pull/688)
    - Merged into `compiler-updates`
6. [#691 - Trust HP/MP/Stat/Skill Multiplier Settings](https://github.com/project-topaz/topaz/pull/691)
    - Merged into `trust`

# Feature Branches (21)
1. [`adventuringfellow`](https://github.com/project-topaz/topaz/tree/adventuringfellow)
    - Basic adventuring fellow and initial quests
    - **Merge date:** Unknown
2. [`apoc-nigh`](https://github.com/project-topaz/topaz/tree/apoc-nigh)
    - Implements Shadows of the Departed
    - Implements quest and reward logic for Apocalypse Nigh
    - Partially implements Apocalypse Nigh BCNM
    - **Merge date:** Unknown
3. [`artisan-moogle`](https://github.com/project-topaz/topaz/tree/artisan-moogle)
    - Implements Mog Sacks
    - Implements Artisan Moogles giving Instant Warp scrolls
    - **Merge date: Next week**
4. [`blue-mage`](https://github.com/project-topaz/topaz/tree/blue-mage)
    - Fixes to Blue Mage spell damage and attack type classifications
    - Implements "Omens" quest
    - Implements "Transformations" quest
    - Adds capability to craft Blue Mage Artifact armor
    - Add Pinecone Bomb spell
    - **Merge date:** Unknown
5. [`compiler-updates`](https://github.com/project-topaz/topaz/tree/compiler-updates)
    - Adds -Werror to builds
    - Various small Core fixes
    - **Merge date: Next week**
6. [`curio`](https://github.com/project-topaz/topaz/tree/curio)
    - Adds Curio Vendor Moogles which sell items
    - **Merge date: Next week**
7. [`despot`](https://github.com/project-topaz/topaz/tree/despot)
    - Fixes spawn behavior for NM "Despot"
    - **Merge date: Next week**
8. [`dual-wield`](https://github.com/project-topaz/topaz/tree/dual-wield)
    - Work on improvements to how dual wielding players and mobs are handled
    - **Merge date:** Unknown
9. [`fix-zmq-exit`](https://github.com/project-topaz/topaz/tree/fix-zmq-exit)
    - Fixes server hanging upon close on *nix hosts
    - **Merged into `release`**
10. [`flash-pan`](https://github.com/project-topaz/topaz/tree/flash-pan)
    - Adjusts Flash in the Pan to be 15 minute server cooldown
    - **Merged into `release`**
11. [`geo`](https://github.com/project-topaz/topaz/tree/geo)
    - Implements Geomancer job
    - **Merge date:** Unknown
12. [`hunt-system`](https://github.com/project-topaz/topaz/tree/hunt-system)
    - Implements NM hunts
    - **Merge date:** Unknown
13. [`instance-npc`](https://github.com/project-topaz/topaz/tree/instance-npc)
    - Fixes GetNPCByID to return instanced NPCs
    - **Merged into `release`**
14. [`limbus`](https://github.com/project-topaz/topaz/tree/limbus)
    - Updates Limbus entry and chest mechanics
    - Adds all level 75 Apollyon BCNMs
    - Adds all level 75 Temenos BCNMs
    - **Merge date:** Unknown
15. [`mystery`](https://github.com/project-topaz/topaz/tree/mystery)
    - Basic daily tally accruing
    - Capability to use dials to obtain items from most goblins
    - Capability to trade keys to goblins for free dial spins
    - **Merge date:** Unknown
16. [`rampart`](https://github.com/project-topaz/topaz/tree/rampart)
    - Adjusts Paladin ability "Rampart" to match current retail
    - **Merge date:** Two weeks
17. [`regine`](https://github.com/project-topaz/topaz/tree/regine)
    - Fixes related to San d'Oria quest "Flyers for Regine"
    - **Merge date: Next week**
18. [`rov`](https://github.com/project-topaz/topaz/tree/rov)
    - Rhapsodies of Vana'diel 1-1 to 1-18
    - **Merge date:** Unknown
19. [`traits-update`](https://github.com/project-topaz/topaz/tree/traits-update)
    - Updates several job traits to match current retail
    - **Merge date: Next week**
20. [`trust`](https://github.com/project-topaz/topaz/tree/trust)
    - Basic trust summoning and behavior
    - Capability to quest starting trusts; enabled by default with setting
    - Basic capability to script trusts to use magic and job abilities
    - **Merge date:** Unknown
21. [`winsock-updates`](https://github.com/project-topaz/topaz/tree/winsock-updates)
    - Various updates to winsock
    - **Merge date: Next week**

# Closing Remarks
> I will investigate our options in regards to any automatic moderation tools which may be available to us. This does not necessarily mean that we will use those tools or the extent at which they will be used, but so that we know what tools might be available to us moving forward.