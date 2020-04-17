# Roll Call
aether, ibm2431, Nyu, Wiggo, Zircon
# Opening Remarks
> I have no opening remarks for today.
# Staff Updates
**aether**: Worked on Pull Request for Creeping Doom; reviewing some others

**ibm2431**: Reviewing Pull Requests; will work on Limbus

**Nyu**: Correcting base sell prices and item model IDs; testing trust branch

**Zircon**: Developed survey to query community for input on Project Focus progress

# General Remarks
- Discussed establishing a more rigorous testing process for feature branches; merging feature branches into release will be paused until then
- Decided to create a feedback channel on the Discord server
- Discussed versioning; will require further evaluation; interested community members are encouraged to provide input
- Discussed setting up process for performance testing; will evaluate after completion of Limbus and Dynamis
- Discussed if Setup Guide Project Focus is complete; staff indicated it is not; staff will evaluate and work on it over the course of the next week
- Affirmed focus into implementing Dynamis and Limbus so more servers may migrate to Topaz

# Pull Requests (6)
1. [#474 - Hopper](https://github.com/project-topaz/topaz/pull/474)
    - Merged into `prince-hopper`
2. [#478 - Updated Mammets in DB](https://github.com/project-topaz/topaz/pull/478)
    - Merged into `release`
3. [#479 - Phomiuna Acqueducts - Fixed Oil Lamps and Doors](https://github.com/project-topaz/topaz/pull/479)
    - Merged into `release`
4. [#482 - Add family column to spell_list](https://github.com/project-topaz/topaz/pull/482)
    - Merged into `spell-family`
5. [#483 - Check if enmity list is empty for unclaimed mobs](https://github.com/project-topaz/topaz/pull/483)
    - Merged into `claim`
6. [#486 - Add geomancer unlock quest 'Dances with Luopans'.](https://github.com/project-topaz/topaz/pull/486)
    - Held (ibm2431): Requested changes

# Feature Branches (12)
1. [`adventuringfellow`](https://github.com/project-topaz/topaz/tree/adventuringfellow)
    - Basic adventuring fellow and initial quests
    - Unknown merge date
2. [`apoc-nigh`](https://github.com/project-topaz/topaz/tree/apoc-nigh)
    - Implements Shadows of the Departed
    - Implements quest and reward logic for Apocalypse Nigh
    - Partially implements Apocalypse Nigh BCNM
    - Unknown merge date
3. [`bcnm-phase`](https://github.com/project-topaz/topaz/tree/bcnm-phase)
    - Fixes to multi-phase BCNMs
    - Unknown merge date
4. [`blue-mage`](https://github.com/project-topaz/topaz/tree/blue-mage)
    - Fixes to Blue Mage spell damage and attack type classifications
    - Omens Quest
    - Add Pinecone Bomb spell
    - Unknown merge date
5. [`claim`](https://github.com/project-topaz/topaz/tree/claim)
    - Changes to claim mechanics
    - Unknown merge date
6. [`cotr`](https://github.com/project-topaz/topaz/tree/cotr)
    - Implements RUN unlock quest "Children of the Rune"
    - Unknown merge date
7. [`limbus`](https://github.com/project-topaz/topaz/tree/limbus)
    - Updates Limbus entry and chest mechanics
    - Unknown merge date
8. [`mystery`](https://github.com/project-topaz/topaz/tree/mystery)
    - Basic daily tally accruing
    - Arbitrix - capability to use dials to obtain items
    - Unknown merge date
9. [`prince-hopper`](https://github.com/project-topaz/topaz/tree/prince-hopper)
    - Implements TOAU quest "Prince and the Hopper"
    - Unknown merge date
10. [`rov`](https://github.com/project-topaz/topaz/tree/rov)
    - Rhapsodies of Vana'diel 1-1 to 1-18
    - Unknown merge date
11. [`spell-family`](https://github.com/project-topaz/topaz/tree/spell-family)
    - Adds a "spell family" column for spells
    - Unknown merge date
12. [`trust`](https://github.com/project-topaz/topaz/tree/trust)
    - Basic trust summoning and behavior
    - Unknown merge date

# Closing Remarks
> Please review our current work for the Project Focus - [Meta] Setup Guide before our next meeting. Should we then decide that the work is complete in scope, I will send out the survey for final sign-off by the community. I would also be appreciative if staff would preview the survey and share any concerns they may have with the survey prior to our next meeting. As the Google Form is not currently accepting responses, you will need to be logged into an account with Edit access to our Google Drive to be capable of viewing the survey. If you have ideas for other Project Focuses which might fit into the "Meta" category, please do not hesitate to share them!

> This week we have also asked questions of how we may handle versioning, branch testing, and server performance testing. Extra thinking on these subjects would be appreciated, and any non-staff reading these meetings are encouraged to share their ideas with us!