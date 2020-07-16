# Roll Call
aether, cocosolos, ibm2431, Zircon
# Opening Remarks
> Starting this week, I would like to add a new section to our meeting format - "Pull Request Remarks". This section will occur after "Unreviewed Pull Requests", and is when I will solicit general input on any open Pull Request which Staff members might like to share.

# Staff Updates

**aether**: Intends to implement a quest; hopes to verify remaining Limbus questions

**cocosolos**: Finished work on database tool; reviewing Pull Requests

**ibm2431**: Finished work on resolving inconsistent elemental ID ordering; working on resolving duplication exploits; reviewing Pull Requests

**Wiggo**: Progressing in capture of mythic quest line; capturing other subjects

# General Remarks
- Project Topaz will open for viewing the currently hidden Discord channel discussing duplication exploits when more general safeguards have been applied
- Discussed difficulties in ensuring that code has sufficient citations and potential methods of addressing this; discussed need for improved capture library discoverability

# Reviewed Pull Requests (14)
1. [#548 - Pathfind fix for Novalmauge](https://github.com/project-topaz/topaz/pull/548)
    - Held (ibm2431): Pending review
2. [#578 - Trust animations](https://github.com/project-topaz/topaz/pull/578)
    - Held (ibm2431): Desires changes
3. [#698 - Additional geomancy bubbles](https://github.com/project-topaz/topaz/pull/698)
    - Held (ibm2431): Desires changes; will develop them
    - Held (cocosolos): Intends to review changes
4. [#720 - Update Vulcan Shot Mob WS to reflect retail DMG](https://github.com/project-topaz/topaz/pull/720)
    - Held (ibm2431): Desires discussion on source for changes
5. [#730 - Adds "All in the Cards" repeatable quest to Chululu](https://github.com/project-topaz/topaz/pull/730)
    - Held (cocosolos): Desires changes
6. [#734 - Add ordering to status effects](https://github.com/project-topaz/topaz/pull/734)
    - Held (ibm2431): Desires changes
7. [#735 - Fixes pet not despawning in combat when master dies.](https://github.com/project-topaz/topaz/pull/735)
    - Held: Author's repository access status unknown
8. [#775 - Trust Spawn/Despawn/Death/Teamwork & Error Messages](https://github.com/project-topaz/topaz/pull/775)
    - **Will be merged into `trust`**
9. [#796 - I Can Hear a Rainbow: scripts/globals to scripts/quests](https://github.com/project-topaz/topaz/pull/796)
    - Held (ibm2431): Desires changes
10. [#799 - Fix climbpix spawn conditions and THF AF2 script](https://github.com/project-topaz/topaz/pull/799)
    - **Merged into `thick-thieves`**
11. [#803 - Guild shop always open](https://github.com/project-topaz/topaz/pull/803)
    - Held (ibm2431): Desires changes
12. [#810 - Missing Divine_bijou drop in Dynamis Windurst](https://github.com/project-topaz/topaz/pull/810)
    - **Merged into `release`**
13. [#833 - Trusts - Consider Trusts for Samba Dazes](https://github.com/project-topaz/topaz/pull/833)
    - **Merged into `trust`**
14. [#839 - Mob group and pool QC](https://github.com/project-topaz/topaz/pull/839)
    - **Merged into `release`**

# Unreviewed Pull Requests (22)
1. [#572 - Add effects rework](https://github.com/project-topaz/topaz/pull/572)
    - Opened: May 2
2. [#651 - [WIP] Refactor effort](https://github.com/project-topaz/topaz/pull/651)
    - Opened: May 23
3. [#723 - Geomancer abilities, merits, and adjustments](https://github.com/project-topaz/topaz/pull/723)
    - Opened: Jun 14
4. [#726 - Last Genkai + Prelude Quest](https://github.com/project-topaz/topaz/pull/726)
    - Opened: Jun 15
5. [#743 - Implement Eco-Warrior quests](https://github.com/project-topaz/topaz/pull/743)
    - Opened: Jun 17
6. [#751 - Added Scholar AF quest Seeing Blood-Red](https://github.com/project-topaz/topaz/pull/751)
    - Opened: Jun 20
7. [#762 - Entity positioning](https://github.com/project-topaz/topaz/pull/762)
    - Opened: Jun 23
8. [#764 - Adding capability for cross-server commands (lua)](https://github.com/project-topaz/topaz/pull/764)
    - Opened: Jun 23
9. [#773 - [WIP] Setzor's fishing](https://github.com/project-topaz/topaz/pull/773)
    - Opened: Jun 25
10. [#780 - Trust Advanced Gambits](https://github.com/project-topaz/topaz/pull/780)
    - Opened: Jun 28
11. [#784 - Extensions to the Lua system + Correct Item Code for Magian Trials](https://github.com/project-topaz/topaz/pull/784)
    - Opened: Jun 30
12. [#785 - A Moral Manifest](https://github.com/project-topaz/topaz/pull/785)
    - Opened: Jun 30
13. [#802 - Magian Trials](https://github.com/project-topaz/topaz/pull/790)
    - Opened: Jul 3
14. [#791 - Trust Melee Balancing](https://github.com/project-topaz/topaz/pull/791)
    - Opened: Jul 1
15. [#812 - Fix for LoadPet iteration not working with gaps in pet_list ID's](https://github.com/project-topaz/topaz/pull/812)
    - Opened: Jul 6
16. [#819 - [WIP] Adding the mods from Lelia](https://github.com/project-topaz/topaz/pull/819)
    - Opened: Jul 7
17. [#820 - Add database tool](https://github.com/project-topaz/topaz/pull/820)
    - Opened: Jul 7
18. [#823 - Implement Eco-Warrior quests](https://github.com/project-topaz/topaz/pull/823)
    - Opened: Jul 7
19. [#828 - Puppetmaster NPC and Attachment Additions](https://github.com/project-topaz/topaz/pull/828)
    - Opened: Jul 8
20. [#831 - Add distinction between days and elements + fix elemental ordering](https://github.com/project-topaz/topaz/pull/831)
    - Opened: Jul 10
21. [#840 - Some silly quest in Windy Waters S](https://github.com/project-topaz/topaz/pull/840)
    - Opened: Jul 12
22. [#851 - [WIP] [Blue Mage] Fix assimilation merit](https://github.com/project-topaz/topaz/pull/851)
    - Opened: Jul 15

# Pull Request Remarks
- ibm2431 requested review of [#831 - Add distinction between days and elements + fix elemental ordering](https://github.com/project-topaz/topaz/pull/831) due to difficulties keeping it current
- ibm2431 expressed importance of community involvement in reviewing [#651 - [WIP] Refactor effort](https://github.com/project-topaz/topaz/pull/651) due to fundamental changes in project

# Branches (15)
1. [`adventuringfellow`](https://github.com/project-topaz/topaz/tree/adventuringfellow)
    - Basic adventuring fellow and initial quests
    - **Merge date:** Unknown
    - **Not in `canary`. Downstream servers should _not_ pull this branch.**
2. [`apoc-nigh`](https://github.com/project-topaz/topaz/tree/apoc-nigh)
    - Implements Shadows of the Departed
    - Implements quest and reward logic for Apocalypse Nigh
    - Partially implements Apocalypse Nigh BCNM
    - **Merge date:** Unknown
3. [`blue-mage`](https://github.com/project-topaz/topaz/tree/blue-mage)
    - Fixes to Blue Mage spell damage and attack type classifications
    - Implements "Omens" quest
    - Implements "Transformations" quest
    - Adds capability to craft Blue Mage Artifact armor
    - Add Pinecone Bomb spell
    - **Merge date:** Unknown
4. [`breakshell`](https://github.com/project-topaz/topaz/tree/breakshell)
    - Adjustments to breaking linkshells
    - **Merge date: Next week**
5. [`compiler-updates`](https://github.com/project-topaz/topaz/tree/compiler-updates)
    - Adds more Raspberry Pi flags and updates cmake
    - **Merge date: Next week**
6. [`deoffset-ability`](https://github.com/project-topaz/topaz/tree/deoffset-ability)
    - Removes built-in ability ID offsets to align with retail
    - **Merge date: Next week**
7. [`enhance-execution`](https://github.com/project-topaz/topaz/tree/enhance-execution)
    - Modifies !exec command to always include player and target variables
    - **Merge date: Next week**
8. [`geo`](https://github.com/project-topaz/topaz/tree/geo)
    - Implements Geomancer job
    - **Merge date:** Unknown
    - **Not in `canary`. Downstream servers should _not_ pull this branch.**
9. [`hunt-system`](https://github.com/project-topaz/topaz/tree/hunt-system)
    - Implements NM hunts
    - **Merge into `release`**
10. [`limbus`](https://github.com/project-topaz/topaz/tree/limbus)
    - Updates Limbus entry and chest mechanics
    - Adds all level 75 Apollyon BCNMs
    - Adds all level 75 Temenos BCNMs
    - **Merge date:** Unknown
11. [`mystery`](https://github.com/project-topaz/topaz/tree/mystery)
    - Basic daily tally accruing
    - Capability to use dials to obtain items from most goblins
    - Capability to trade keys to goblins for free dial spins
    - **Merge date:** Unknown
12. [`ranperre-rest`](https://github.com/project-topaz/topaz/tree/ranperre-rest)
    - Adjusts NPCs related to San d'Oria mission "Ranperre's Final Rest"
    - **Merge into `release`**
13. [`raptor-speed`](https://github.com/project-topaz/topaz/tree/raptor-speed)
    - Implements Jeuno quest "Full Speed Ahead!"
    - Implements packet 0x3A
    - Implements packet 0x75
    - Implements packet 0x77
    - **Merge date:** Unknown
14. [`regine-final-form`](https://github.com/project-topaz/topaz/tree/regine-final-form)
    - Improvements to the San d'Oria quest "Flyers for Regine"
    - **Merge date: Two weeks**
15. [`rov`](https://github.com/project-topaz/topaz/tree/rov)
    - Rhapsodies of Vana'diel 1-1 to 1-18
    - **Merge date: Next week**
16. [`song-overwrite`](https://github.com/project-topaz/topaz/tree/song-overwrite)
    - Fixes issue in which Bard songs did not properly overwrite
    - **Merge date: Two weeks**
17. [`synth-science`](https://github.com/project-topaz/topaz/tree/synth-science)
    - Removes various crafting myths
    - Adds crafting limitation system; configurable
    - Corrects skillup rates and amounts
    - **Merge date: Two weeks**
18. [`trust`](https://github.com/project-topaz/topaz/tree/trust)
    - Basic trust summoning and behavior
    - Capability to quest starting trusts; enabled by default with setting
    - Basic capability to script trusts to use magic and job abilities
    - **Merge date:** Unknown

# Closing Remarks
> I would like to thank Staff for their handling of the duplication exploit which was reported to us. You worked diligently to investigate, communicate, and resolve the issue. You have the gratitude of many downstream server administrators as well. While you may have seen some expressions of gratitude for how Project Topaz handled the situation, you have not seen those which were expressed to me privately. Multiple server administrators -- including those which have not adopted Project Topaz -- expressed that they were impressed by our process. One administrator even likened the rollout to that of professional web service firms.

> Secondly, due to the level of trust we established, I have begun receiving reports of other potential exploits. I do not believe this would be the case had it not been for your hard work. I will engage with Staff to investigate these possible exploits in the future.