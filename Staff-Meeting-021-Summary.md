# Roll Call
aether, cocosolos, ibm2431, Zircon
# Opening Remarks
> I have no Opening Remarks for today.

# Staff Updates

**aether**: Testing Backoo branch; researching Limbus to answer remaining questions

**cocosolos**: Almost finished working on database tool

**ibm2431**: Began work on resolving inconsistent elemental ID ordering

**Wiggo**: Progressing in capture of mythic quest line

# General Remarks
- Zircon intends to consult Consul before removing "crafting myth" settings

# Reviewed Pull Requests (11)
1. [#548 - Pathfind fix for Novalmauge](https://github.com/project-topaz/topaz/pull/548)
    - Held (cocosolos): Desired changes
    - Held (ibm2431): Desired changes
2. [#698 - Additional geomancy bubbles](https://github.com/project-topaz/topaz/pull/698)
    - Held (ibm2431): Desires changes; will develop them
    - Held (cocosolos): Intends to review changes
3. [#730 - Adds "All in the Cards" repeatable quest to Chululu](https://github.com/project-topaz/topaz/pull/730)
    - Held (cocosolos): Desires changes
4. [#735 - Fixes pet not despawning in combat when master dies.](https://github.com/project-topaz/topaz/pull/735)
    - Held (ibm2431): Desires changes
5. [#738 - Fix Half Partition synth level requirements](https://github.com/project-topaz/topaz/pull/738)
    - Held (cocosolos): Desires changes
6. [#749 - Updated item_basic.sql to match with Lelia](https://github.com/project-topaz/topaz/pull/749)
    - **Merged into `release`**
7. [#754 - Updates for item_equipment.sql, item_latents.sql, item_weapon.sql](https://github.com/project-topaz/topaz/pull/754)
    - **Merged into `release`**
8. [#771 - Added Gyre-Carlin](https://github.com/project-topaz/topaz/pull/771)
    - Held (cocosolos): Desires changes
9. [#778 - Fix double-free errors in exit/crash](https://github.com/project-topaz/topaz/pull/778)
    - **Merged into `release`**
10. [#791 Trust Melee Balancing](https://github.com/project-topaz/topaz/pull/791)
    - **Merged into `trust`**
11. [#793 Update timeoffset GM commands](https://github.com/project-topaz/topaz/pull/793)
    - **Merged into `time-mage`**

# Unreviewed Pull Requests (24)
1. [#572 - Add effects rework](https://github.com/project-topaz/topaz/pull/572)
    - Opened: May 2
2. [#578 - Trust animations](https://github.com/project-topaz/topaz/pull/578)
    - Opened: May 3
3. [#651 - [WIP] Refactor effort](https://github.com/project-topaz/topaz/pull/651)
    - Opened: May 23
4. [#720 - Update Vulcan Shot Mob WS to reflect retail DMG](https://github.com/project-topaz/topaz/pull/720)
    - Opened: Jun 13
5. [#723 - Geomancer abilities, merits, and adjustments](https://github.com/project-topaz/topaz/pull/723)
    - Opened: Jun 14
6. [#726 - Last Genkai + Prelude Quest](https://github.com/project-topaz/topaz/pull/726)
    - Opened: Jun 15
7. [#734 - Add ordering to status effects](https://github.com/project-topaz/topaz/pull/734)
    - Opened: Jun 16
8. [#743 - Implement Eco-Warrior quests](https://github.com/project-topaz/topaz/pull/743)
    - Opened: Jun 17
9. [#744 - Fix BRD song overwrite bug](https://github.com/project-topaz/topaz/pull/744)
    - Opened: Jun 18
10. [#751 - Added Scholar AF quest Seeing Blood-Red](https://github.com/project-topaz/topaz/pull/751)
    - Opened: Jun 20
11. [#755 - Adjusted Switchstix Relic wait time to current retail](https://github.com/project-topaz/topaz/pull/755)
    - Opened: Jun 22
12. [#762 - Entity positioning](https://github.com/project-topaz/topaz/pull/762)
    - Opened: Jun 23
13. [#764 - Adding capability for cross-server commands (lua)](https://github.com/project-topaz/topaz/pull/764)
    - Opened: Jun 23
14. [#773 - [WIP] Setzor's fishing](https://github.com/project-topaz/topaz/pull/773)
    - Opened: Jun 25
15. [#774 - Full Speed Ahead: Various Improvements](https://github.com/project-topaz/topaz/pull/774)
    - Opened: Jun 26
16. [#775 - Trust Spawn/Despawn/Death/Synergy Messages](https://github.com/project-topaz/topaz/pull/775)
    - Opened: Jun 26
17. [#779 - Implement crafting skill limitation and various other fixes](https://github.com/project-topaz/topaz/pull/779)
    - Opened: Jun 28
18. [#780 - Trust Advanced Gambits](https://github.com/project-topaz/topaz/pull/780)
    - Opened: Jun 28
19. [#781 - Add Shiva's Claws lua script provided by Gweivyth](https://github.com/project-topaz/topaz/pull/781)
    - Opened: Jun 28
20. [#784 - Extensions to the Lua system + Correct Item Code for Magian Trials](https://github.com/project-topaz/topaz/pull/784)
    - Opened: Jun 30
21. [#785 - A Moral Manifest](https://github.com/project-topaz/topaz/pull/785)
    - Opened: Jun 30
22. [#786 - tpz.zone referenced in casket_loot](https://github.com/project-topaz/topaz/pull/786)
    - Opened: Jun 30
23. [#789 - Flyers for Regine: Act III (Finale)](https://github.com/project-topaz/topaz/pull/789)
    - Opened: Jul 1
24. [#790 - Infill nm_spawn_points for all existing lottery mobs](https://github.com/project-topaz/topaz/pull/790)
    - Opened: Jul 1


# Feature Branches (15)
1. [`adventuringfellow`](https://github.com/project-topaz/topaz/tree/adventuringfellow)
    - Basic adventuring fellow and initial quests
    - **Merge date:** Unknown
    - **Not in `canary`. Downstream servers should _not_ pull this branch.**
2. [`apoc-nigh`](https://github.com/project-topaz/topaz/tree/apoc-nigh)
    - Implements Shadows of the Departed
    - Implements quest and reward logic for Apocalypse Nigh
    - Partially implements Apocalypse Nigh BCNM
    - **Merge date:** Unknown
3. [`backoo`](https://github.com/project-topaz/topaz/tree/backoo)
    - Implements NM "Backoo"
    - **Merged into `release`**
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
    - **Merged into `release`**
6. [`geo`](https://github.com/project-topaz/topaz/tree/geo)
    - Implements Geomancer job
    - **Merge date:** Unknown
    - **Not in `canary`. Downstream servers should _not_ pull this branch.**
7. [`hunt-system`](https://github.com/project-topaz/topaz/tree/hunt-system)
    - Implements NM hunts
    - **Merge date: Next week**
8. [`limbus`](https://github.com/project-topaz/topaz/tree/limbus)
    - Updates Limbus entry and chest mechanics
    - Adds all level 75 Apollyon BCNMs
    - Adds all level 75 Temenos BCNMs
    - **Merge date:** Unknown
9. [`mystery`](https://github.com/project-topaz/topaz/tree/mystery)
    - Basic daily tally accruing
    - Capability to use dials to obtain items from most goblins
    - Capability to trade keys to goblins for free dial spins
    - **Merge date:** Unknown
10. [`rampart`](https://github.com/project-topaz/topaz/tree/rampart)
    - Adjusts Paladin ability "Rampart" to match current retail
    - **Merged into `release`**
11. [`ranperre-rest`](https://github.com/project-topaz/topaz/tree/ranperre-rest)
    - Adjusts NPCs related to San d'Oria mission "Ranperre's Final Rest"
    - **Merge date: Next week**
12. [`raptor-speed`](https://github.com/project-topaz/topaz/tree/raptor-speed)
    - Implements Jeuno quest "Full Speed Ahead!"
    - Implements packet 0x3A
    - Implements packet 0x75
    - Implements packet 0x77
    - **Merge date:** Unknown
13. [`rov`](https://github.com/project-topaz/topaz/tree/rov)
    - Rhapsodies of Vana'diel 1-1 to 1-18
    - **Merge date: Next week**
14. [`time-mage`](https://github.com/project-topaz/topaz/tree/time-mage)
    - Allows changing the current vana'diel date
    - **Merged into `release`**
15. [`trust`](https://github.com/project-topaz/topaz/tree/trust)
    - Basic trust summoning and behavior
    - Capability to quest starting trusts; enabled by default with setting
    - Basic capability to script trusts to use magic and job abilities
    - **Merge date:** Unknown

# Closing Remarks
> I will include the question to Consul regarding the removal of the crafting settings with this week's digest.

> I have no other Closing Remarks.