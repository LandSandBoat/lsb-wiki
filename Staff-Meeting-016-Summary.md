# Roll Call
cocosolos, ibm2431, Wiggo, Zircon
# Opening Remarks
> I hear the Return to Vana'diel campaign has already begun. Let us get through this meeting swiftly.

# Staff Updates
**aether**: Reviewing Pull Requests; testing branches

**cocosolos**: Reviewing Pull Requests; working on developing and testing small things

**ibm2431**: Reviewing Pull Requests, preparing for free period; will spend period capturing; will not be available on Discord

**Wiggo**: Started Limbus captures

# General Remarks
- Discussed merging of project focus branches into release prior to the focus's full completion; current work may be merged so long as it is stable, feature complete, and verified accurate to retail

# Pull Requests (1)
1. [#548 - Pathfind fix for Novalmauge](https://github.com/project-topaz/topaz/pull/548)
    - Held (ibm2431): Desires changes

# Feature Branches (23)
1. [`adventuringfellow`](https://github.com/project-topaz/topaz/tree/adventuringfellow)
    - Basic adventuring fellow and initial quests
    - **Merge date:** Unknown
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
4. [`casket`](https://github.com/project-topaz/topaz/tree/casket)
    - Adds treasure caskets to all applicable zones
    - **Merged into release**
5. [`chain-fix`](https://github.com/project-topaz/topaz/tree/chain-fix)
    - Fix chain exp applying to non-chained kills
    - **Merged into release**
6. [`cop-log`](https://github.com/project-topaz/topaz/tree/cop-log)
    - Fixes log handling for Chains of Promathia
    - **Merged into release**
    - **Requires migration**
7. [`crafting`](https://github.com/project-topaz/topaz/tree/crafting)
    - Crafting fixes related to HQ and desynth rates
    - **Merged into release**
8. [`dual-wield`](https://github.com/project-topaz/topaz/tree/dual-wield)
    - Work on improvements to how dual wielding players and mobs are handled
    - **Merge date:** Unknown
9. [`faded-promise`](https://github.com/project-topaz/topaz/tree/faded-promise)
    - Implements the Bastok quest "Faded Promises"
    - **Merged into release**
10. [`feature/mob-gil-multiplier`](https://github.com/project-topaz/topaz/tree/feature/mob-gil-multiplier)
    - Adds configurable multiplier for gil dropped from mobs
    - **Merged into release**
11. [`kohlo`](https://github.com/project-topaz/topaz/tree/kohlo)
    - Scripting improvements to Kohlo-Lakolo
    - **Merged into release**
12. [`limbus`](https://github.com/project-topaz/topaz/tree/limbus)
    - Updates Limbus entry and chest mechanics
    - Adds all level 75 Apollyon BCNMs
    - Adds all level 75 Temenos BCNMs
    - **Merge date:** Unknown
13. [`login-code`](https://github.com/project-topaz/topaz/tree/login-code)
    - Makes login error messages more descriptive
    - **Merge date:** Two weeks
14. [`mono-nchaa`](https://github.com/project-topaz/topaz/tree/mono-nchaa)
    - Duplicated sale items removed from Mono Nchaa
    - **Merged into release**
15. [`mystery`](https://github.com/project-topaz/topaz/tree/mystery)
    - Basic daily tally accruing
    - Capability to use dials to obtain items from most goblins
    - Capability to trade keys to goblins for free dial spins
    - **Merge date:** Unknown
16. [`rov`](https://github.com/project-topaz/topaz/tree/rov)
    - Rhapsodies of Vana'diel 1-1 to 1-18
    - **Merge date:** Unknown
17. [`rse-ammo`](https://github.com/project-topaz/topaz/tree/rse-ammo)
    - Adds the capability to obtain RSE satchets
    - **Merged into release**
18. [`skillchain`](https://github.com/project-topaz/topaz/tree/skillchain)
    - Reworks skillchain mapping to make formations more accurate
    - **Merged into release**
19. [`sub-ratio`](https://github.com/project-topaz/topaz/tree/sub-ratio)
    - Implements capability to change sub-job ratio with setting
    - **Merged into release**
20. [`teamwork`](https://github.com/project-topaz/topaz/tree/teamwork)
    - Basic trust summoning and behavior
    - Capability to quest starting trusts; enabled by default with setting
    - **Merge date:** Two weeks (2020/05/28)
21. [`trust`](https://github.com/project-topaz/topaz/tree/trust)
    - Basic trust summoning and behavior
    - Capability to quest starting trusts; enabled by default with setting
    - **Merge date:** Unknown
22. [`tuning-in`](https://github.com/project-topaz/topaz/tree/tuning-in)
    - Implements Windurst quest "Tuning In"
    - Implements Windurst quest "Tuning Out"
     - **Merge date:** Two weeks (2020/05/28)
23. [`ziphus`](https://github.com/project-topaz/topaz/tree/ziphus)
    - Adds capability to spawn NM "Ziphus
    - **Merge date:** Two weeks (2020/05/28)

# Closing Remarks
> The Return to Vana'diel campaign has begun. We will not be meeting next week. As we did during the previous campaign, official Project Topaz activities will be paused for its duration to allow staff to maximize the time they have access to retail. Furthermore, to ensure that all staff have had opportunity to review Pull Requests, merges into `release` and `canary` will be disabled during the duration of the campaign. Community members are welcome to submit Pull Requests during this time! However, please give us your patience while waiting for a review.