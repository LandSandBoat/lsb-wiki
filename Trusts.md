# Trusts

| Mark | Status |
|---|---|
| ✅ | Verified (As close to retail as possible) (**Only Staff should mark this**) |
| ✔️ | Implemented (A fair approximation of retail, possible minor cosmetic defects) |
| ⚠️ | Partially Implemented (Playable, Some thing missing) |
| ⛔ | Partially Implemented (Playable, Most things missing) |
| ❌ | Unimplemented (Will just stand around) |

**This page is only for tracking Trust combat logic, not whether they obtainable or not. This assumes you have access to them through GM commands or otherwise (`!addalltrusts`).**

## General Notes

- All mages are very MP-hungry
- Spell selection is very simple and doesn't account for weaknesses/immunities/absorbs.
- Trusts don't track elemental resistances.
- As above, Trusts don't track if their spells were resisted, or if they might get resisted
- Melee trusts don't get access to TP skills that can form Light/Dark skillchains until Lv60, unless that's the only skill they have.
- The default TP/SC behaviour is ASAP + Random (Use TP ASAP, pick a random valid skill from your list).

***

### San d'Oria

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Excenmille | ✔️ | | | |
| Curilla | ✔️ | | | | |
| Trion | ✔️ | | | | |

### Bastok

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Naji | ✔️ | |
| Ayame | ✔️ | |
| Iron Eater | ⚠️ | | | Missing specific logic |
| Volker | ⚠️ | | | Missing specific logic |

### Windurst

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Kupipi| ✔️ | |
| Nanaa Mihgo | ✔️ | | | Despoil log message is broken |
| Ajido-Marujido | ✔️ | |
| Shantotto | ✔️ | |

### Jeuno

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Maat | ✔️ | | | |

### Chains of Promathia

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Cherukiki | ❌ | |
| Prishe | ❌ | |
| Ulmia | ❌ | |
| Shikaree Z | ❌ | |

### Treasures of Aht Urhgan

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Gadalar | ❌ | |
| Gessho | ✔️ | |
| Nashmeira | ❌ | |
| Zazarg | ❌ | |

### Wings of the Goddess

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Excenmille (S) | ❌ | |
| Klara | ❌ | |
| Lilisette | ❌ | |
| Rainemard | ✔️ | En-spell selection is hard-coded |
| Romaa Mihgo | ❌ | |

### Seekers of Adoulin

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Arciela  | ❌ | |
| August | ❌ | |
| Chacharoon | ❌ | |
| Ingrid II | ❌ | |
| Rosulatia | ❌ | |
| Ygnas | ❌ | |

### Rhapsodies of Vana'diel

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Abquhbah | ❌ | |
| Arciela II | ❌ | |
| Balamor | ❌ | |
| Halver | ❌ | |
| Iroha | ❌ | |
| Iroha II | ❌ | |
| Lilisette II | ❌ | |
| Lion II | ❌ | |
| Nashmeira II | ❌ | |
| Prishe II | ❌ | |
| Selh'teus | ❌ | |
| Semih Lafihna | ❌ | |
| Tenzen II | ❌ | |
| Zeid II | ⚠️ | | | Implemented very quickly, probably missing things |

### Unity Concord

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Aldo (UC) | ❌ | |
| Apururu (UC) | ❌ | |
| Ayame (UC) | ❌ | |
| Flaviria (UC) | ❌ | |
| Invincible Shield (UC) | ❌ | |
| Jakoh Wahcondalo (UC) | ❌ | |
| Maat (UC) | ❌ | |
| Naja Salaheem (UC) | ❌ | |
| Pieuje (UC) | ❌ | |
| Sylvie (UC) | ❌ | |
| Yoran-Oran (UC) | ❌ | |

### Repeat Login Campaigns

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Abenzio | ❌ | |
| Areuhat | ❌ | |
| Brygid | ❌ | |
| Darrcuiln  | ❌ | |
| D. Shantotto | ❌ | |
| Karaha-Baruha | ❌ | |
| Kuyin Hathdenna | ❌ | |
| Lehko Habhoka | ✔️ | |
| Lhe Lhangavo | ❌ | |
| Lion | ❌ | |
| Luzaf | ❌ | |
| Mayakov | ❌ | |
| Naja Salaheem | ✔️ | |
| Najelith | ❌ | |
| Robel-Akbel | ❌ | |
| Rongelouts | ❌ | |
| Rughadjeen  | ❌ |
| Shantotto II | ✔️ | | | |
| Star Sibyl | ❌ | |
| Teodor | ❌ | |
| Uka Totlihn | ✔️ | |
| Ullegore | ❌ | |
| Zeid | ❌ | |

### Records of Eminence

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Adelheid | ⛔ | | | No Scholar abilities/spells |
| Joachim | ⛔ | | | Song selection is hard-coded |
| Koru-Moru | ✔️ | |
| Mihli Aliapoh | ⚠️ | | | Implemented very quickly, probably missing things |
| Tenzen | ⚠️ | | | Implemented very quickly, probably missing things |
| Valaineral | ⚠️ | | | Implemented very quickly, probably missing things |

### Alter Ego Extravaganzas

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| Amchuchu | ❌ | |
| Cid | ❌ | |
| Elivira | ❌ | |
| Ferreous Coffin | ❌ | |
| Gilgamesh | ❌ | |
| Kayeel-Payeel | ❌ | |
| King of Hearts | ❌ | |
| Kukki-Chebukki | ❌ | |
| Leonoyne | ❌ | |
| Lhu Mhakaracca | ❌ | |
| Makki-Chebukki | ❌ | |
| Margret | ❌ | |
| Maximilian | ❌ | |
| Mildaurion | ❌ | |
| Morimar | ❌ | |
| Noillurie | ❌ | |
| Ovjang | ❌ | |
| Qultada | ❌ | |
| Rahal | ❌ | |
| Sakura | ⚠️ | | | Immortal, but still can get hit by things when it shouldn't |

### Other Events

| Name | Status | TP Behaviour | SC Behaviour | Notes |
|---|---|---|---|---|
| AAEV | ❌ | |
| AAGK  | ❌ | |
| AAHM | ❌ | |
| AAMR | ❌ | |
| AATT | ❌ | |
| Aldo | ❌ | |
| Babban | ❌ | |
| Cornelia | 💀 | | | Unsummonable: SE removed from the game |
| Fablinix | ❌ | |
| Kupofried | ❌ | |
| Matsui-P | 💀 | | | Unsummonable: SE removed from the game |
| Monberaux | ❌ | |
| Moogle | ❌ | |
| Mumor | ❌ | |
| Mumor II | ❌ | |
| Ygnas | ❌ | |
