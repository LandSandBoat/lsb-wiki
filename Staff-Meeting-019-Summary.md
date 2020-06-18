# Roll Call
aether, cocosolos, ibm2431, Nyu, Wiggo, Zircon
# Opening Remarks
> I have no Opening Remarks for today.

# Staff Updates

**aether**: Submitting Pull Requests; researching treasure coffer gil rates

**cocosolos**: Reviewing Pull Requests; submitting fixes; will work on hunts and database tools

**ibm2431**: Reviewing Pull Requests; primarily focusing on Geomancer Pull Requests

**Wiggo**: Pursuing automation to assist with capture process

# General Remarks
- Discussed when Pull Requests should be merged into `release` versus when they should be merged into new feature branches
- Zircon informed of minor additional changes to Pull Request review process; for consideration during Staff Meetings, the age of a Pull Request less than 1,000 additions will be three days since the last commit, or three days since it has been marked as ready to review, whichever is later
- Additionally, when official project activities are paused, the submission date of a Pull Request opened during the pause will be considered to be the date which official activities resume
- Zircon informed Staff of intent to have all Staff members reviewed every six months; and intention to have Staff other than cocosolos be the subject of a community survey; actual survey design not yet finalized
- Discussed potential changes in how Pull Requests are reviewed and merged to ease Staff burden and allow Staff to better focus on project goals, including the potential removal of the "automatically merge if not held" rule; Zircon will consider feedback from the community

# Pull Requests (6)
1. [#548 - Pathfind fix for Novalmauge](https://github.com/project-topaz/topaz/pull/548)
    - Held (ibm2431): Desires changes
2. [#638 - [FIX] Remove 1 day wait for Ranperre's Final Rest quest](https://github.com/project-topaz/topaz/pull/638)
    - Held (cocosolos): Desires changes
3. [#699 - Add geomancer -ra spells and scrolls](https://github.com/project-topaz/topaz/pull/699)
    - Merged into `geo`
4. [#720 - Update Vulcan Shot Mob WS to reflect retail DMG](https://github.com/project-topaz/topaz/pull/720)
    - Held (ibm2431): Free
5. [#722 - Add var and binding for isDualWielding + remove presumptuous granting of mod to all NIN NMs](https://github.com/project-topaz/topaz/pull/722)
    - Will be merged into `release`
6. [#725 - Double-up cooldown adjustments](https://github.com/project-topaz/topaz/pull/725)
    - Merged into `release`

# Feature Branches (19)
1. [`adventuringfellow`](https://github.com/project-topaz/topaz/tree/adventuringfellow)
    - Basic adventuring fellow and initial quests
    - **Merge date:** Unknown
    - **Not in `canary`. Downstream servers should _not_ pull this branch.**
2. [`apoc-nigh`](https://github.com/project-topaz/topaz/tree/apoc-nigh)
    - Implements Shadows of the Departed
    - Implements quest and reward logic for Apocalypse Nigh
    - Partially implements Apocalypse Nigh BCNM
    - **Merge date:** Unknown
3. [`artisan-moogle`](https://github.com/project-topaz/topaz/tree/artisan-moogle)
    - Implements Mog Sacks
    - Implements Artisan Moogles giving Instant Warp scrolls
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
    - **Merge date: Delayed, tenatively next week**
6. [`curio`](https://github.com/project-topaz/topaz/tree/curio)
    - Adds Curio Vendor Moogles which sell items
    - **Merged into `release`**
7. [`despot`](https://github.com/project-topaz/topaz/tree/despot)
    - Fixes spawn behavior for NM "Despot"
    - **Merged into `release`**
8. [`dual-wield`](https://github.com/project-topaz/topaz/tree/dual-wield)
    - Work on improvements to how dual wielding players and mobs are handled
    - **Merge date: Next week**
9. [`geo`](https://github.com/project-topaz/topaz/tree/geo)
    - Implements Geomancer job
    - **Merge date:** Unknown
    - **Not in `canary`. Downstream servers should _not_ pull this branch.**
10. [`hunt-system`](https://github.com/project-topaz/topaz/tree/hunt-system)
    - Implements NM hunts
    - **Merge date:** Unknown
    - **Not in `canary`. Downstream servers should _not_ pull this branch.**
11. [`limbus`](https://github.com/project-topaz/topaz/tree/limbus)
    - Updates Limbus entry and chest mechanics
    - Adds all level 75 Apollyon BCNMs
    - Adds all level 75 Temenos BCNMs
    - **Merge date:** Unknown
12. [`mystery`](https://github.com/project-topaz/topaz/tree/mystery)
    - Basic daily tally accruing
    - Capability to use dials to obtain items from most goblins
    - Capability to trade keys to goblins for free dial spins
    - **Merge date:** Unknown
13. [`rampart`](https://github.com/project-topaz/topaz/tree/rampart)
    - Adjusts Paladin ability "Rampart" to match current retail
    - **Merge date: Next week**
14. [`regine`](https://github.com/project-topaz/topaz/tree/regine)
    - Fixes related to San d'Oria quest "Flyers for Regine"
    - **Merged into `release`**
15. [`rov`](https://github.com/project-topaz/topaz/tree/rov)
    - Rhapsodies of Vana'diel 1-1 to 1-18
    - **Merge date:** Unknown
16. [`time-mage`](https://github.com/project-topaz/topaz/tree/time-mage)
    - Allows changing the current vana'diel date
    - **Merge date: Next week**
17. [`traits-update`](https://github.com/project-topaz/topaz/tree/traits-update)
    - Updates several job traits to match current retail
    - **Merged into `release`**
18. [`trust`](https://github.com/project-topaz/topaz/tree/trust)
    - Basic trust summoning and behavior
    - Capability to quest starting trusts; enabled by default with setting
    - Basic capability to script trusts to use magic and job abilities
    - **Merge date:** Unknown
19. [`winsock-updates`](https://github.com/project-topaz/topaz/tree/winsock-updates)
    - Various updates to winsock
    - **Merged into `release`**

# Closing Remarks
> I will listen to Staff and community input regarding our current review process, and take such input into consideration.