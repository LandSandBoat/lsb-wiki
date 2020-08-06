# Roll Call
aether, Wiggo, Zircon
# Opening Remarks
> As of the start of this meeting, this channel will not be publicly viewable until we conclude.
>
> I feel that community input on the contents of meetings while they are still occurring creates distraction. I am pleased that Community Members feel invested in our meeting contents! However, comments outside this channel on subjects which we are still in the process of discussing can lead -- and has led -- to diversionary discussions outside of this channel.
>
> This distracts Staff, increases difficulty for future readers following discussion, and prolongs our meeting duration. I cherish the time that I am with you! However, I suspect Staff would like to keep meetings as brief as possible!
>
> Additionally, discussions created by the community during these meetings may give the impression that decisions we make are subject to concurrent debate. They are not. Community input is valued and Project Topaz will always strive to take it into account! However, it is ultimately Staff which decides the undertakings of Staff.
>
> Community Members who wish to be active participants in Staff meetings are encouraged to apply! Should they be successful they will receive the additional privileges -- and responsibilities -- of the role.
>
> This channel will again be viewable by the entire community once we conclude.

# General Remarks
- Discussed how to handle ibm2431's departure from Staff; holds will be removed, reviewed Pull Requests will be mentioned, but such Pull Requests will not be automatically merged
- Acknowledged the start of another Return Home to Vana'diel campaign; official project activities will be paused during its duration
- Discussed concerns over lack of Staff capacity; may continue discussing the subject after conclusion of Return Home to Vana'diel campaign

# Reviewed Pull Requests (14)
1. [#548 - Pathfind fix for Novalmauge](https://github.com/project-topaz/topaz/pull/548)
    - Held: Status unknown
2. [#572 - `Add effects rework`](https://github.com/project-topaz/topaz/pull/572)
    - Held: Status unknown
3. [#685 - `Abyssea Lights system`](https://github.com/project-topaz/topaz/pull/685)
    - Held: Status unknown
4. [#730 - Adds "All in the Cards" repeatable quest to Chululu](https://github.com/project-topaz/topaz/pull/730)
    - Held (cocosolos): Desires changes
5. [#734 - Add ordering to status effects](https://github.com/project-topaz/topaz/pull/734)
    - **Will be merged into `status-effect-order`**
6. [#735 - Fixes pet not despawning in combat when master dies.](https://github.com/project-topaz/topaz/pull/735)
    - Held: Author has requested community assistance
7. [#812 - Fix for LoadPet iteration not working with gaps in pet_list ID's](https://github.com/project-topaz/topaz/pull/812)
    - Held (cocosolos): Desires further review
8. [#823 - Implement Eco-Warrior quests](https://github.com/project-topaz/topaz/pull/823)
    - **Merged into `eco-warrior`**
9. [#831 - Add distinction between days and elements + fix elemental ordering](https://github.com/project-topaz/topaz/pull/831)
    - **Merged into `fix-elements`**
10. [#851 - [Blue Mage] Fix assimilation merit](https://github.com/project-topaz/topaz/pull/851)
    - Held: Status unknown
11. [#869 - add scripts for usables](https://github.com/project-topaz/topaz/pull/869)
    - **Merged into `usables`**
12. [#870 - `RoE System + Sparkshop + Early Records`](https://github.com/project-topaz/topaz/pull/870)
    - Held: Status unknown
13. [#895 - `Check for sharpshot frame on automaton ranged attack.`](https://github.com/project-topaz/topaz/pull/895)
    - Held: Status unknown
14. [#914 - `Guild Reset at JP midnight`](https://github.com/project-topaz/topaz/pull/914)
    - Held: Status unknown

# Unreviewed Pull Requests (9)
1. [#651 - [WIP] Refactor effort](https://github.com/project-topaz/topaz/pull/651)
    - Opened: May 23
2. [#751 - Added Scholar AF quest Seeing Blood-Red](https://github.com/project-topaz/topaz/pull/751)
    - Opened: Jun 20
3. [#762 - Entity positioning](https://github.com/project-topaz/topaz/pull/762)
    - Opened: Jun 23
4. [#773 - [WIP] Setzor's fishing](https://github.com/project-topaz/topaz/pull/773)
    - Opened: Jun 25
5. [#785 - A Moral Manifest](https://github.com/project-topaz/topaz/pull/785)
    - Opened: Jun 30
6. [#802 - Magian Trials](https://github.com/project-topaz/topaz/pull/790)
    - Opened: Jul 3
7. [#840 - Some silly quest in Windy Waters S](https://github.com/project-topaz/topaz/pull/840)
    - Opened: Jul 12
8. [#867 - Beginning support for Ansible, Docker, and Jenkins](https://github.com/project-topaz/topaz/pull/867)
    - Opened: Jul 18
9. [#881 - Create MOD for "Resistance to All Status Ailments"](https://github.com/project-topaz/topaz/pull/881)
    - Opened: Jul 23

# Pull Request Remarks
- Scholar AF quest Pull Request may only be partially implemented; BCNM is not implemented

# Branches (22)
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
    - **Merged into `release`**
4. [`dbtool`](https://github.com/project-topaz/topaz/tree/dbtool)
    - Adds python-based database tool to assist with database updates and migrations
    - **Merged into `release`**
6. [`deoffset-ability`](https://github.com/project-topaz/topaz/tree/deoffset-ability)
    - Removes built-in ability ID offsets to align with retail
    - **Merge date:** Unknown
7. [`eco-warror`](https://github.com/project-topaz/topaz/tree/eco-warrior)
    - Adds "Eco Warrior" quests
    - **Merge date:** Unknown
8. [`enhance-execution`](https://github.com/project-topaz/topaz/tree/enhance-execution)
    - Modifies !exec command to always include player and target variables
    - **Merge date:** Unknown
9. [`geo`](https://github.com/project-topaz/topaz/tree/geo)
    - Implements Geomancer job
    - **Merge date:** Unknown
    - **Not in `canary`. Downstream servers should _not_ pull this branch.**
10. [`limbus`](https://github.com/project-topaz/topaz/tree/limbus)
    - Updates Limbus entry and chest mechanics
    - Adds all level 75 Apollyon BCNMs
    - Adds all level 75 Temenos BCNMs
    - **Merge date:** Unknown
11. [`lua-item`](https://github.com/project-topaz/topaz/tree/lua-item)
    - Extends to Lua system to allow fetching information about items
    - Corrects item code for Magian Trials
    - **Merge date:** Unknown
12. [`mercantilism`](https://github.com/project-topaz/topaz/tree/mercantilism)
    - Corrects static guild shops to behave more accurately to retail
    - **Merge date:** Unknown
13. [`mystery`](https://github.com/project-topaz/topaz/tree/mystery)
    - Basic daily tally accruing
    - Capability to use dials to obtain items from most goblins
    - Capability to trade keys to goblins for free dial spins
    - **Merge date:** Unknown
14. [`rainbow`](https://github.com/project-topaz/topaz/tree/rainbow)
    - Numerous fixes to Summoner unlock quest "I Can Hear a Rainbow"
    - **Merge date:** Unknown
15. [`raptor-speed`](https://github.com/project-topaz/topaz/tree/raptor-speed)
    - Implements Jeuno quest "Full Speed Ahead!"
    - Implements packet 0x3A
    - Implements packet 0x75
    - Implements packet 0x77
    - **Merge date:** Unknown
16. [`regine-final-form`](https://github.com/project-topaz/topaz/tree/regine-final-form)
    - Improvements to the San d'Oria quest "Flyers for Regine"
    - **Merged into `release`**
17. [`rov`](https://github.com/project-topaz/topaz/tree/rov)
    - Rhapsodies of Vana'diel 1-1 to 1-18
    - **Merged into `release`**
18. [`song-overwrite`](https://github.com/project-topaz/topaz/tree/song-overwrite)
    - Fixes issue in which Bard songs did not properly overwrite
    - **Merged into `release`**
19. [`synth-science`](https://github.com/project-topaz/topaz/tree/synth-science)
    - Removes various crafting myths
    - Adds crafting limitation system; configurable
    - Corrects skillup rates and amounts
    - **Merge date:** Unknown
20. [`thick-thieves`](https://github.com/project-topaz/topaz/tree/thick-thieves)
    - Corrects spawn conditions for NM "Climbpix" during "Thick as Thieves" quest
    - **Merge date:** Unknown
21. [`trust`](https://github.com/project-topaz/topaz/tree/trust)
    - Basic trust summoning and behavior
    - Capability to quest starting trusts; enabled by default with setting
    - Basic capability to script trusts to use magic and job abilities
    - **Merge date:** Unknown
22. [`usables`](https://github.com/project-topaz/topaz/tree/usables)
    - Adds item scripts for 57 usable items.
    - **Merge date: Two weeks**

# Closing Remarks
> I recognize that this is a very difficult time for Project Topaz.
>
> Please always remember that I have the utmost faith and confidence in your abilities.
>
> However, please be certain to take care of yourselves!
>
> None of you are being paid for the time you volunteer to the community. Do not feel obligated to devote more time than you would care to give.
>
> On that subject, official project activities are paused for the duration of the Return Home to Vana'diel campaign.
>
> You may use this as an opportunity to acquire information from retail -- or take a well-deserved break!