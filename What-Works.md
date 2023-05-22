This list is not the final word on what works in the project, or how well it works. Your best bet is always to check the code and check in-game.

**NO SPOILERS, NO MISSION NAMES, NO IN-DEPTH DETAILS etc.**

| Mark | Status |
|---|---|
| ✅ | Verified (As close to retail as possible) |
| ✔️ | Implemented (A fair approximation of retail) |
| ⚠️ | Partially Implemented = Playable |
| ⛔ | Partially Implemented = Unplayable / Broken |
| 🐤 | In progress |
| ❌ | Unimplemented |
| ❔ | Status Unknown |
| No Mark | Status Unknown |

# Jobs

Note: All jobs are working and playable up to Lv75. It is unknown how much Lv99, i119, and Quest content is complete for all jobs. 

| Job | 75-era | 99-era | 119-era | Quests | Notes |
|-----|---|-|-|-|--------------------|
| WAR | ✔️ | | | | Needs confirmation |
| MNK | ✔️ | | | | Needs confirmation |
| WHM | ✔️ | | | | Needs confirmation |
| BLM | ✔️ | | | | Needs confirmation |
| RDM | ✔️ | | | | Needs confirmation |
| THF | ✔️ | | | | Needs confirmation |
| PLD | | | | | Needs confirmation |
| DRK | | | | | Needs confirmation |
| BST | | | | | Needs confirmation |
| BRD | | | | | Needs confirmation |
| RNG | | | | | Needs confirmation |
| SAM | | | | | Needs confirmation |
| NIN | | | | | Needs confirmation |
| DRG | | | | | Needs confirmation |
| SMN | | | | | Needs confirmation |
| BLU | 🐤 | | | | Needs confirmation |
| COR | 🐤 | | | | Needs confirmation |
| PUP | 🐤 | | | | Needs confirmation |
| DNC | 🐤 | | | | Needs confirmation |
| SCH | 🐤 | | | | Needs confirmation |
| GEO | 🐤 | | | | Needs confirmation |
| RUN | 🐤 | | | | Needs confirmation |

# Missions

Playable missions are marked in the following file with `--+--` after their names<br>
https://github.com/LandSandBoat/server/blob/base/scripts/globals/missions.lua

We have a new format for missions. Newly written/rewritten missions can be found here:<br>
https://github.com/LandSandBoat/server/tree/base/scripts/missions

| Status | Name | Notes |
|---|---|---|
| ✔️ | Bastok | |
| ✔️ | San d'Oria | |
| ✔️ | Windurst | |
| ✔️ | Rise of the Zilart | |
| ✔️ | Chains of Promathia | |
| ⚠️ | Treasures of Aht Urhgan | Completable. Retail accurate up to Mission 18. Rest in need of confirmation. |
| 🐤 | Wings of the Goddess | Up to WOTG 54 (mainline missions only, nation quest status unknown, missing a lot of fight content) |
| 🐤 | Seekers of Adoulin | Up to SOA 5-5-1 (missing a lot of fight content) |
| ⛔ | A Crystalline Prophecy | Up to ACP 04 |
| 🐤 | A Moogle Kupo d'Etat | Up to AMK 08 |
| ⛔ | A Shantotto Ascension | Up to ASA 03 |
| ⛔ | Rhapsodies of Vanadiel | Up to ROV 2-25 (missing a lot of fight content) |
| ❌ | The Voracious Resurgence | Will not implement, go play retail. |

# Quests

Playable quests are marked in the following file with `--+--` after their names<br>
https://github.com/LandSandBoat/server/blob/base/scripts/globals/quests.lua

We have a new format for quests. Newly written/rewritten quests can be found here:<br>
https://github.com/LandSandBoat/server/tree/base/scripts/quests

# Battle Content (by era)

## Pre-Item Level

### Base Game & Rise of the Zilart ⚠️

| Status | Name | Notes |
|---|---|---|
| ⚠️ | BCNMs | Unusable fights are commented out with `--`:<br>https://github.com/LandSandBoat/server/blob/base/scripts/globals/bcnm.lua |
| ❌ | Garrison | |
| ✔️ | HNMs - Land Kings | |
| ❌ | "Classic" Dynamis | [Will not be implemented.](Frequently-Asked-Questions#when-can-i-play-classic-dynamis) |
| ⚠️ | "Neo" Dynamis | City and Dreamworld zones farmable, some unimplemented NMs |
| ✔️ | Sky NMs | |

### Chains of Promathia ⛔

| Status | Name | Notes |
|---|---|---|
| ✔️ | HNMs - Wyrms | |
| ⚠️ | Sea NMs | Some NMs unimplemented: Jailer of Justice / Jailer of Love / Absolute Virtue |
| 🐤 | Limbus | |
| ❔ | Empty Notorious Monsters (ENM) | Tracked the same way as BCNMs:<br>Unusable fights are commented out with `--`:<br>https://github.com/LandSandBoat/server/blob/base/scripts/globals/bcnm.lua |

### Treasures of Aht Urhgan ❔

| Status | Name | Notes |
|---|---|---|
| 🐤 | Assault | |
| ❌ | Besieged | |
| ❌ | Einherjar | |
| ✔️ | HNMs - ToAU Zones | |
| ❔ | Imperial Seal Notorious Monsters (ISNM) | |
| ❌ | Nyzul Isle Investigation | |
| ❌ | Salvage | |
| ❔ | Zeni Notorious Monsters (ZNM) | Some NMs scripted (accuracy unverified) |

### Wings of the Goddess ❌

| Status | Name | Notes |
|---|---|---|
| ❌ | Allied Notes Notorious Monsters (ANNM) | |
| ❌ | Campaign | |
| ❌ | HNMs - WoTG Zones (Sandworm and Dark Ixion) | |
| ❌ | Moblin Maze Mongers | |
| ❌ | Stronghold Notorious Monsters (SCNM) | |
| ❌ | Walk of Echoes | |

### Abyssea Era  ⛔

| Status | Name | Notes |
|---|---|---|
| 🐤 | Abyssea  | Can enter zones. Normal mobs and time-spawned NMs are up, but do not respawn if killed. Everything else not implemented. |
| ❌ | Bastion | |
| ❌ | Legion | |
| ❌ | Meeble Burrows | |
| ❌ | Voidwalker NM System | |
| ❌ | Voidwatch | |

## Post-Item Level ❌

### Seekers of Adoulin ❌

| Status | Name | Notes |
|---|---|---|
| ❌ | Skirmish | |
| ❌ | Delve | |
| ❌ | Incursion | |
| ❌ | Reives | |
| ❌ | Sinister Reign | |
| ❌ | Vagary | |

### Modern Era ❌

| Status | Name | Notes |
|---|---|---|
| ❌ | AMAN Trove | |
| ⛔ | Ambuscade | |
| ❌ | Domain Invasion | |
| ❌ | Dynamis Divergence | |
| ❌ | High-Tier Mission Battlefields | |
| ❌ | Geas Fete | |
| ❌ | Master Trials | |
| ❌ | Odyssey | |
| ❌ | Omen | |
| ❌ | Sacred Kindred Crest Notorious Monsters (SKCNM) | |
| ❌ | Sortie | |
| ❌ | Unity - Wanted | |

# Hobby & Misc Content

| Status | Name | Notes |
|---|---|---|
| ❌ | Adventuring Fellows | |
| ❌ | Ballista | |
| ❌ | Brenner | |
| ✔️ | Chocobo Digging | |
| ❌ | Chocobo Racing | |
| ❌ | Chocobo Raising | |
| ✔️ | Crafting | |
| ✔️ | Fields of Valor | |
| 🐤 | Fishing | |
| ✔️ | Gardening | |
| ✔️ | Gobbie Mystery Box | |
| ✔️ | Grounds of Valor | |
| ✔️ | HELM | |
| ✔️ | Hunt Registry | |
| ⚠️ | Job Points | |
| ✔️ | Login Campaign | |
| ⚠️ | Magian Trials | |
| ✔️ | Mannequins | |
| ❌ | Mog Garden | |
| ✔️ | Mog House 2nd Floor | |
| ❌ | Monstrosity | |
| ✔️ | Mounts & 'Full Speed Ahead' Minigame | |
| ❌ | Pankration | |
| ✔️ | Records of Eminence | ~300 records + Timed challenges |
| ✔️ | Soultrapping, Soul Plates & Zeni | Works, but Zeni values are placeholders |
| ❌ | Synergy | |
| ⚠️ | Trusts | Trust status:<br>Trusts |

# Mechanics

| Status | Name | Notes |
|---|---|---|
| ✔️ | Aura Effects | |
| ⚠️ | Basic PVP | |
| 🐤 | Confrontation Effects | |
| ⚠️ | Stagger Effects | Neo-Dynamis and Abyssea proc systems implemented |
