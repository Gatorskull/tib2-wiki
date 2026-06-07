# Client-Extracted Ships

Hidden contributor staging page. This captures ship class, size, EP, level, and slot data found in the current decompiled client. Treat this as source-backed extraction, not polished public wiki copy.

Primary sources:

- `Assembly-CSharp\DFHOJHHBAMJ.cs`
- `Assembly-CSharp\JEKJDKMBIGN.cs`
- `Assembly-CSharp\IKOLEGFOADL.cs`
- `Assembly-CSharp\NFLGBFKEKMC.cs`
- `Assembly-CSharp\ONCHPJDOFKP.cs`
- `Assembly-CSharp\CPBOEMLOKBM.cs`
- `TibSharp\Expansion\Library\Database\ShipDbObj.cs`

## Ship Classes

Client enum order:

| Ship class |
|---|
| Shuttle |
| Frigate |
| Assassin |
| Cruiser |
| Destroyer |
| Battleship |
| Flagship |
| Carrier |
| Hades |
| Emperor |

## Ship Sizes

Source: `DFHOJHHBAMJ.GetSize(this NFLGBFKEKMC)`.

| Size | Ship classes |
|---|---|
| Small | Shuttle, Frigate, Assassin |
| Medium | Cruiser, Destroyer |
| Large | Battleship, Flagship |
| Huge | Carrier, Hades |
| Massive | Emperor |

## Ship Mods

Sources: `Assembly-CSharp\NNGLFJGGODO.cs` and `Assembly-CSharp\DFHOJHHBAMJ.cs`.

Ship modification enum values:

| Mod | Client name | Client description |
|---|---|---|
| Medic | Medic | Add Technician & Repair Speed Technology to Ship |
| Raider | Raider | Add PvP & Defense Unit Damage Technology to Ship |
| Interdictor | Interdictor | Change Carrier Leadership to Interdictor |
| Freighter | Freighter | Add Harvesting & Resource Capacity Technology to Ship |
| Paladin | Paladin | Add Max Hull Bonus & Guardian Technology to Ship |
| Ultimate | Ultimate | Add 4 Equip Points and Extra Equipment Slots to Ship |
| DeceptionModule | Deception Module | Hides Equipped Items & Gives Enemies False Info |
| Unique | Unique | Add Random Bonus Features to Ship |
| Phoenix | Phoenix | Add Savior & Rebirth Technology to Non-Hardcore Ship |
| Gladiator | Gladiator | Add Vorpal & Savior Technology to Ship |

Retro skin enum values are `RetroShuttle`, `RetroFrigate`, `RetroScorpion`, `RetroAssassin`, `RetroCorvette`, `RetroCruiser`, `RetroTitan`, `RetroFlayer`, `RetroDevastator`, `RetroDestroyer`, `RetroBattleship`, `RetroInvader`, `RetroExecutioner`, `RetroDespoiler`, `RetroAnnihilator`, `RetroDreadnaught`, `RetroFlagship`, `RetroCarrier`, `RetroReaper`, `RetroHades`, and `RetroTerminus`.

Client helper classifications:

- `IsTechnologyMod()` is true for Medic, Raider, Interdictor, Freighter, Paladin, Ultimate, Unique, Phoenix, and Gladiator.
- `IsRetroSkin()` is true for RetroShuttle through RetroTerminus.
- Deception Module has a second description line: `Add 'Hack Ram Rank 1' Technology to Ship`.

Ship name suffixes:

| Mod | Normal suffix | Hardcore suffix |
|---|---|---|
| Medic | `-MD` | `-MDHC` |
| Raider | `-RA` | `-RAHC` |
| Interdictor | `-IN` | `-INHC` |
| Freighter | `-FR` | `-FRHC` |
| Paladin | `-PL` | `-PLHC` |
| Ultimate | `-ULT` | `-ULTHC` |
| Phoenix | `-PH` | `-PHHC` |
| Gladiator | `-GL` | `-GLHC` |

### Ship Mod Technology Bonuses

Ship mods feed into ship technology bonus slots. The client function names are obfuscated, so this table uses the observed source slot labels `Bonus E` and `Bonus F`.

| Mod | Bonus E | Bonus F |
|---|---|---|
| Medic | SpeedRepair1 for mod rank 0-1; SpeedRepair2 for rank 2-3; SpeedRepair3 for rank 4+ | Technician1 at rank 0; Technician2 at rank 1; Technician3 at rank 2-3; Technician4 at rank 4+ |
| Raider | Marauder1 for rank 0-1; Marauder2 for rank 2-3; Marauder3 for rank 4+ | PvPDamage2 at rank 0, then PvPDamage3/4/5/6 for ranks 1/2/3/4, PvPDamage7 for rank 5+ |
| Freighter | Scavenger2 at rank 0, then Scavenger3/4/5/6 for ranks 1/2/3/4, Scavenger7 for rank 5+ | Freighter1 at rank 0, then Freighter2/3/4 for ranks 1/2/3, Freighter5 for rank 4+ |
| Paladin | none for rank 0-1; Guardian1 for rank 2-3; Guardian2 for rank 4+ | HullMax3 at rank 0, then HullMax4/5/6/7 for ranks 1/2/3/4, HullMax8 for rank 5+ |
| Phoenix | Rebirth1 by default, Rebirth2 for ranks 1-2, Rebirth3 for rank 3, Rebirth4 for ranks 4-5 | Savior1 by default, Savior2 for ranks 2-3, Savior3 for rank 4, Savior4 for rank 5+ |
| Gladiator | Vorpal1 by default, Vorpal2 for ranks 1-2, Vorpal3 for rank 3, Vorpal4 for ranks 4-5 | Savior1 by default, Savior2 for ranks 2-3, Savior3 for rank 4, Savior4 for rank 5+ |
| Unique | Seed/class/faction-dependent; see notes below | Seed/class/faction-dependent; see notes below |

Interdictor is handled in the Carrier bonus path: normal Carrier bonus ranks produce Leadership1/2/3, while Interdictor Carrier replaces those with Interdictor1/2/3/4 using the same rank bands.

Unique mod bonus selection is deterministic from the ship seed and context, not a simple fixed table. `GetUniqueShipModBonusTechE(...)` chooses from drone, repair-speed, hack/grapple/drain speed, scan speed, Mechanic, Advanced Hacking/Grappling/Draining, or NovaDeath families. `GetUniqueShipModBonusTechF(...)` chooses from PvPDamage, Freighter, Technician, HullMax, Scavenger, Leadership/Interdictor or Cloak, Harvesting, Deflector, Vorpal, Rebirth, Savior, or AlienDamage families, with some outcomes depending on ship class and whether the seed is below `5,000,000`.

### Ultimate And Unique Slot/EP Bonuses

Sources: `Assembly-CSharp\CHCIGDNAAPI.cs`, `Assembly-CSharp\DDEIFGPEOMI.cs`, and `Assembly-CSharp\CPBOEMLOKBM.cs`.

`Ultimate` is exposed by the ship helper property currently named `NHMPBNHOPBA`. It gives:

- `+4` base Equip Points through `GetBonusEquipPointsFromMod()`.
- `+1` weapon slot through `GetBonusWeaponSlotsFromMod()`.
- `+1` drone slot through `GetBonusDroneSlotsFromMod()`.
- `+1` battery slot through `GetBonusBatterySlotsFromMod()`.

The final public slot counts are still capped at `6` by the shared `GetMaxWeaponSlots()`, `GetMaxDroneSlots()`, and `GetMaxBatterySlots()` helpers after base slots and item-granted slot bonuses are added.

`Unique` is exposed by the ship helper property currently named `JCFHGHACFNH`. It uses `UniqueSeed`, ship size, and modulo checks to determine bonus EP and slots:

```text
Unique bonus EP = floor(size enum value / 2) + ((UniqueSeed + 3527) % 3)
```

Size enum values are `Small = 1`, `Medium = 2`, `Large = 3`, `Huge = 4`, and `Massive = 5`, so the size term is:

| Size | Size term |
|---|---:|
| Small | 0 |
| Medium | 1 |
| Large | 1 |
| Huge | 2 |
| Massive | 2 |

Unique weapon slot bonus:

```text
if size > Medium and ((UniqueSeed + 17) % 3) != 0: +0
else if ((UniqueSeed + 23) % 7) != 0: +1
else: +2
```

Unique drone slot bonus:

```text
if size > Medium and ((UniqueSeed + 31) % 2) != 0: +0
else if ((UniqueSeed + 41) % 7) != 0: +1
else: +2
```

Unique battery slot bonus:

```text
if ((UniqueSeed + 71) % 5) != 0: +1
else: +2
```

As with Ultimate, final displayed slot counts are capped at `6`.

### Deception Module Notes

Sources:

- `Assembly-CSharp\DFHOJHHBAMJ.cs`
- `Assembly-CSharp\BAANAKJCOJA.cs`
- `Assembly-CSharp\DDEIFGPEOMI.cs`
- `Assembly-CSharp\EntityInspectPanel.cs`
- `Assembly-CSharp\InspectEntityEquipmentPanel.cs`
- `Assembly-CSharp\IKOLEGFOADL.cs`
- `Assembly-CSharp\PGJIDFCBFCC.cs`

Confirmed client-facing data:

- Name: `Deception Module`.
- Description A: `Hides Equipped Items & Gives Enemies False Info`.
- Description B: `Add 'Hack Ram Rank 1' Technology to Ship`.
- Icon path uses `icon_deception`.
- `IsTechnologyMod()` does not include `DeceptionModule`; it includes Medic, Raider, Interdictor, Freighter, Paladin, Ultimate, Unique, Phoenix, and Gladiator.

Deception is inactive when the ship does not have the module flag, when the owner has toggled deception off, or when the deception-disabled timer is active. Superusers bypass the effect. For normal players, the target's owning player/corp and friend status affect whether deception is tested.

When deception is active:

- `GetVisibleItems(...)` returns all items that are not hidden by the slot-hiding rule below.
- The inspect panel shows `Deception Hides Equipment` instead of the item count and gear score.
- The active technology label is hidden on the main inspect panel.
- The equipment inspect panel shows a false active tech label, currently `Havok Tech II`, instead of the real tech list.
- Hidden item slots are disabled in the equipment panel and replaced by a deception graphic.
- Disable Deception reveals items and stats for `30 seconds`.
- The default Disable Deception Tech Point cost is `50`, from `PGJIDFCBFCC.KLCMKEEEOJG`.

The slot-hiding helper uses the target's rank/elite value currently exposed on the entity as `OFICBLPEAGD`:

| Slot | Hidden when rank is at least |
|---|---:|
| Weapon1 | 5 |
| Weapon2 | 4 |
| Weapon3 | 3 |
| Weapon4 | 2 |
| Weapon5 | 1 |
| Weapon6 | always |
| Drone1 | 5 |
| Drone2 | 4 |
| Drone3 | 3 |
| Drone4 | 2 |
| Drone5 | 1 |
| Drone6 | always |
| Armor | 2 |
| Storage | always |
| Engine | 5 |
| Computer | 3 |
| Battery1 | 5 |
| Battery2 | 4 |
| Battery3 | 3 |
| Battery4 | 2 |
| Battery5 | 1 |
| Battery6 | always |
| Shield | 1 |
| Special | 4 |

Needs data:

- Exact source path that grants or displays the Hack Ram Rank 1 effect from Deception Module. The text is confirmed, but this pass did not find a clean matching technology-bonus branch like the other technology mods.

## Deployed Fleet Limits

Sources: `JEKJDKMBIGN.GetRequiredLevelToDeployNextShip(...)`, `JEKJDKMBIGN.GetMaxDeployedShips(...)`, `PGJIDFCBFCC.DLMMHCCOMBN`, and `IKOLEGFOADL.CanDeployShip(...)`.

The current client maximum deployed fleet size is `10` ships.

`GetRequiredLevelToDeployNextShip(currentDeployedCount)` gates the next deployment by current deployed ship count:

| Deploying ship number | Required player level |
|---:|---:|
| 1 | 0 |
| 2 | 0 |
| 3 | 10 |
| 4 | 20 |
| 5 | 30 |
| 6 | 40 |
| 7 | 50 |
| 8 | 75 |
| 9 | 100 |
| 10 | 150 |

`GetMaxDeployedShips(playerLevel)` returns the same caps by player level:

| Player level range | Max deployed ships |
|---|---:|
| 0-9 | 2 |
| 10-19 | 3 |
| 20-29 | 4 |
| 30-39 | 5 |
| 40-49 | 6 |
| 50-74 | 7 |
| 75-99 | 8 |
| 100-149 | 9 |
| 150+ | 10 |

### Fleet Size Composition Requirements

Source: `IKOLEGFOADL.IsShipSizeDeployRequirementsMet(currentDeployedCount, smallCountAfterCandidate, mediumCountAfterCandidate)`.

When deploying another ship, the client counts the candidate ship if it is Small or Medium and checks the resulting fleet:

| Deploying ship number | Requirement in resulting fleet |
|---:|---|
| 1-7 | No Small/Medium composition requirement |
| 8 | At least 1 Small or Medium ship |
| 9-10 | At least 2 total Small or Medium ships |

Important wording note: the embedded old wiki fallback says 9- and 10-ship fleets require a Small and Medium ship. The client check is broader: it tests `smallCount + mediumCount >= 2`, so two Small ships or two Medium ships satisfy the client-side requirement.

## Base Equip Points

Source: `DFHOJHHBAMJ.GetBaseEquipPoints(this NFLGBFKEKMC, ONCHPJDOFKP)`.

| Ship | Human | Wyrd | Pirate | Het | Precursor |
|---|---:|---:|---:|---:|---:|
| Shuttle | 6 | 8 | 6 | 8 | 9 |
| Frigate | 8 | 9 | 9 | 9 | 10 |
| Assassin | 10 | 11 | 11 | 11 | 12 |
| Cruiser | 11 | 12 | 12 | 12 | 13 |
| Destroyer | 13 | 14 | 14 | 14 | 15 |
| Battleship | 16 | 17 | 17 | 17 | 18 |
| Flagship | 19 | 20 | 20 | 20 | 21 |
| Carrier | 20 | 21 | 21 | 21 | 22 |
| Hades | 22 | 23 | 23 | 23 | 24 |
| Emperor | 26 | 27 | 27 | 27 | 28 |

## Required Player Level

Source: `DFHOJHHBAMJ.GetRequiredPlayerLevel(this NFLGBFKEKMC, ONCHPJDOFKP)`.

| Ship | Human | Wyrd | Pirate | Het | Precursor |
|---|---:|---:|---:|---:|---:|
| Shuttle | 0 | 0 | 0 | 0 | 0 |
| Frigate | 0 | 0 | 0 | 0 | 0 |
| Cruiser | 7 | 10 | 8 | 9 | 12 |
| Destroyer | 11 | 14 | 12 | 13 | 16 |
| Assassin | 14 | 17 | 15 | 16 | 19 |
| Battleship | 15 | 18 | 16 | 17 | 20 |
| Flagship | 20 | 20 | 20 | 20 | 25 |
| Hades | 30 | 45 | 35 | 40 | 50 |
| Carrier | 35 | 50 | 40 | 45 | 55 |
| Emperor | 45 | 60 | 50 | 55 | 65 |

## Weapon Slots

Source: `DFHOJHHBAMJ.GetMaxWeapons(this NFLGBFKEKMC, ONCHPJDOFKP)`.

Rules:

- Shuttle always follows the small rule: 2 weapons, or 3 for Precursor.
- Carrier is special: 2 weapons, or 3 for Precursor.
- Otherwise slot count is size-based.
- Precursor gets +1 weapon slot for Small, Medium, Large, and Huge ships.
- Massive ships have 6 weapon slots, except Human Emperor has 5.

| Size / special case | Non-Precursor | Precursor | Human Massive exception |
|---|---:|---:|---:|
| Shuttle | 2 | 3 | n/a |
| Small | 2 | 3 | n/a |
| Medium | 3 | 4 | n/a |
| Large | 4 | 5 | n/a |
| Huge | 5 | 6 | n/a |
| Carrier | 2 | 3 | n/a |
| Massive | 6 | 6 | 5 |

## Drone Slots

Source: `DFHOJHHBAMJ.GetMaxDroneSlots(this NFLGBFKEKMC, ONCHPJDOFKP)`.

Rules:

- Shuttle and Assassin are special: 2 drone slots, or 3 for Het.
- Carrier is special: 5 drone slots, or 6 for Het.
- Otherwise slot count is size-based.
- Het gets +1 drone slot on most ship sizes.
- Huge Human ships have 3 drone slots instead of the Huge default of 4.
- Massive ships have 6 drone slots, except Human Emperor has 5.

| Size / special case | Non-Het | Het | Human exception |
|---|---:|---:|---:|
| Shuttle | 2 | 3 | n/a |
| Assassin | 2 | 3 | n/a |
| Small | 1 | 2 | n/a |
| Medium | 2 | 3 | n/a |
| Large | 3 | 4 | n/a |
| Huge | 4 | 5 | 3 |
| Carrier | 5 | 6 | n/a |
| Massive | 6 | 6 | 5 |

## Battery Slots

Source: `DFHOJHHBAMJ.GetMaxBatterySlots(this NFLGBFKEKMC, ONCHPJDOFKP)`.

Rules:

- Shuttle, Frigate, and default Small ships have 1 battery slot, or 2 for Wyrd.
- Assassin is special: 2 battery slots, or 3 for Wyrd.
- Wyrd gets +1 battery slot for Small through Huge ships.
- Massive ships have 6 battery slots, except Human Emperor has 5.

| Size / special case | Non-Wyrd | Wyrd | Human Massive exception |
|---|---:|---:|---:|
| Shuttle | 1 | 2 | n/a |
| Frigate | 1 | 2 | n/a |
| Small/default | 1 | 2 | n/a |
| Assassin | 2 | 3 | n/a |
| Medium | 2 | 3 | n/a |
| Large | 3 | 4 | n/a |
| Huge | 4 | 5 | n/a |
| Massive | 6 | 6 | 5 |

## Movement Prep Time

Source: `JEKJDKMBIGN.GetMovePrepTime(CPBOEMLOKBM, bool, bool, bool)` and default config fields in `PGJIDFCBFCC.cs`.

The client has a separate pre-move/pre-jump animation time by ship size. If the fast-path booleans in `GetMovePrepTime(...)` are set, the method returns `500ms`. Otherwise it uses the size table below.

| Ship size | Default prep time |
|---|---:|
| Small/default | 700ms |
| Medium | 1000ms |
| Large | 1300ms |
| Huge | 1700ms |
| Massive | 1700ms |

These values are distinct from movement travel time and the hard minimum move-speed rules. The current client supports the player-confirmed rule that larger ships have longer pre-jump animation timing.

## Movement Speed Runtime Formula

Sources: `GKFECKLMHGM.GetMoveSpeedPercentMod()`, `GetModifiedMoveSpeedMS()`, `JEKJDKMBIGN.GetBaseMoveSpeedMS(...)`, `DDEIFGPEOMI.GetSpaceLaneBonus()`, `GetInterdictorPenalty()`, `OMMOANGJAIM`, `HCGPPIPPAIJ`, `CHCIGDNAAPI.GetInterdictorRank(...)`, default config fields in `PGJIDFCBFCC.cs`, and config update path `OPDJFCNPEMJ`.

The client-visible base movement formula is:

```text
base move time ms = configured base move time + size enum value * 500
modified move time ms = base move time + base move time * MoveSpeedPercent
client-visible final move time ms = max(modified move time, configured minimum move time)
```

Default backing config values:

| Field | Default |
|---|---:|
| Configured base move time | `8000ms` |
| Configured minimum move time | `3000ms` |
| MoveSpeedPercent floor | `-65%` |
| TargetingSpeedPercent floor | `-65%` |

With the default base time and ship-size enum values (`Small = 1`, `Medium = 2`, `Large = 3`, `Huge = 4`, `Massive = 5`), the client-visible base move times are:

| Size | Base move time |
|---|---:|
| Small | 8.5s |
| Medium | 9.0s |
| Large | 9.5s |
| Huge | 10.0s |
| Massive | 10.5s |

Important caveat: the client-visible final clamp is a single `3000ms` value, but current live rules confirmed by Goot are size-specific hard minimums: Small `3.0s`, Medium `3.2s`, Large `3.3s`, Huge/Massive `3.5s`. Keep the public wiki on those live values.

Config caveat: `JEKJDKMBIGN` reads these values from a static `PGJIDFCBFCC` balance/config object. The packet class currently named `OPDJFCNPEMJ` deserializes server-provided config into that same object. Treat the `PGJIDFCBFCC` field initializers as client defaults/fallbacks, not proof that live production cannot override them.

### Movement Percent Sources

`GetMoveSpeedPercentMod()` adds item movement stats and aux-scaled item movement stats, then applies technology/status effects:

| Source | Effect |
|---|---:|
| Daily movement tech condition | `-20%` |
| FriendlyTerritoryEffect | `-10%` |
| HyperDrive1/2/3 | `-10%` / `-15%` / `-20%` |
| Hardcore ship flag | `-10%` |
| NanobotCharge | `-10%` |
| SpaceLaneEffect1/2/3 | `-10%` / `-15%` / `-20%` |
| InterdictorEffect1/2/3/4 | `+15%` / `+20%` / `+25%` / `+30%` |

Movement and targeting percent modifiers both floor at `-65%` in the visible client stat container. Player-confirmed live behavior still lets ships overstack movement beyond the floor so the extra negative movement can counter enemy Interdictor penalties.

`GetSpaceLaneBonus()` returns no Space Lane bonus for NPC/structure-like entities, returns no Space Lane bonus while an Interdictor penalty is active, returns `SpaceLaneEffect3` for the relevant map/sector flag, or returns the Space Lane effect from the ship's special item.

`GetInterdictorPenalty()` returns no penalty for NPC/structure-like entities or when no sector-local map context exists. Otherwise it asks the sector/map interdictor controller for the penalty.

### Interdictor Sector State

Sources: `OMMOANGJAIM`, `HCGPPIPPAIJ`, and `OBLBONFPEOE`.

The sector-local interdictor controller stores:

- One active Interdictor source entity (`GNIBJABBHJK`) for the sector.
- One active Interdictor penalty/effect rank.
- A server-provided dictionary of nearby sector bonus rows keyed by entity id.

The network message class currently named `HCGPPIPPAIJ` sends:

| Payload field | Observed meaning |
|---|---|
| `PDDMBBHEBMI` | Map/world id byte |
| `HNCHLODMMNL`, `MJPIMIIMIEP` | Sector coordinates |
| `NNIDAJMLJJI` | Active Interdictor penalty/effect rank |
| `BKBOHHGNLIE` | Active source entity id when the rank is not `NULL` |
| `GBGCFAGGDAD[]` | Bonus rows copied into the sector controller |

Each bonus row (`OBLBONFPEOE`) contains:

| Field | Observed meaning |
|---|---|
| `HILLMMBCLFM` | Entity id |
| `COCCAHAFDLL` | Move-speed milliseconds used by the map indicator/helper |
| `GJFJLBCBJJE` | Bonus/effect rank |

This means the current client is mostly rendering and applying server-provided sector state. The visible client confirms there is one active Interdictor source for a sector at a time, but does not prove the server-side tie-break rule that chooses that source.

Penalty application rules visible in `OMMOANGJAIM.GetInterdictorPenalty(...)`:

- No active source means no penalty.
- NPC/AI state uses the opposite friendly/enemy branch from player ships.
- Protected sectors and one protected/blocked sector state return no penalty for the normal player-ship branch.
- If the entity id being checked is the active Interdictor source, it is not penalized by its own effect.
- A global debug/override flag also suppresses the penalty.
- Otherwise the active penalty rank is returned.

### Interdictor Rank Source

`CHCIGDNAAPI.GetInterdictorRank(...)` returns the ship's current Interdictor rank from either its primary carrier bonus tech or secondary/bonus tech:

| Source rank | Penalty effect |
|---|---:|
| Interdictor1 | InterdictorEffect1 / `+15%` movement and targeting time |
| Interdictor2 | InterdictorEffect2 / `+20%` movement and targeting time |
| Interdictor3 | InterdictorEffect3 / `+25%` movement and targeting time |
| Interdictor4 | InterdictorEffect4 / `+30%` movement and targeting time |

Needs data: the server-side rule for deciding which Interdictor source owns a contested sector. Training/chat currently says first-arrived or strongest-by-rank, but this pass only confirms that the client receives the already-chosen active source.

## Shipyard and Crafting Requirements

Sources: `DFHOJHHBAMJ.GetShipyardRequiredLevel(...)`, `GetCraftRequiredDaysInCorp(...)`, `GetCraftResourceRequirement(...)`, `GetCorpShipCraftSkill(...)`, and `JEKJDKMBIGN` ship-cost helpers.

### Shipyard Required Level

`GetShipyardRequiredLevel(...)` returns `0` for Human Shuttle through Human Flagship. Otherwise it returns the normal required player level table above.

### Required Days in Corp

| Ship | Human | Non-Human |
|---|---:|---:|
| Assassin | 0 | 2 |
| Destroyer | 0 | 1 |
| Battleship | 0 | 1 |
| Flagship | 0 | 2 |
| Carrier | 2 | 2 |
| Hades | 2 | 2 |
| Emperor | 2 | 2 |
| Other ships | 0 | 0 |

### Default Skull Costs

Source defaults are config-backed and can be server-sent. Human ships divide these default skull costs by `2` with integer division.

| Ship | Default non-Human skull cost | Default Human skull cost |
|---|---:|---:|
| Assassin | 150 | 75 |
| Destroyer | 20 | 10 |
| Battleship | 50 | 25 |
| Flagship | 100 | 50 |
| Carrier | 500 | 250 |
| Hades | 250 | 125 |
| Emperor | 1000 | 500 |
| Other ships | 0 | 0 |

### Default Relic Costs

The helper uses a Human/non-Human boolean for Carrier, Hades, and Emperor. Assassin has a single default relic cost.

| Ship | Human/default-Human relic cost | Non-Human relic cost |
|---|---:|---:|
| Assassin | 1 | 1 |
| Carrier | 8 | 15 |
| Hades | 2 | 3 |
| Emperor | 25 | 50 |
| Other ships | 0 | 0 |

### Resource Requirement Formula

`GetCraftResourceRequirement(...)` computes a base amount and rounds it to the nearest `5`:

```text
roundedResource = round(resourceBase / 5) * 5
resourceBase = resourceFactionMultiplier * craftingMod
```

Resource multipliers:

| Resource | Multiplier rule |
|---|---|
| Crew | Human or Het `29`; otherwise `32` |
| Organic | Het `27`; otherwise `24` |
| Gas | Wyrd `22`; otherwise `19` |
| Metal | Pirate `32`; otherwise `29` |
| Radioactive | Wyrd or Precursor `28`; otherwise `25` |
| Darkmatter | Precursor `20`; otherwise `17` |

`craftingMod` starts with base EP, adds `+2` for each non-null ship technology slot, adds `+3/+6/+9/+12` for Medium/Large/Huge/Massive size, applies ship-class reductions for Shuttle/Frigate/Cruiser/Destroyer/Battleship, then adds a faction offset. Finally, some ship classes use config-backed multipliers.

Default config-backed ship craft multipliers:

| Ship | Multiplier |
|---|---:|
| Assassin | 4.0 |
| Flagship | 3.0 |
| Carrier | 3.5 |
| Hades | 3.5 |
| Emperor | 5.0 |
| Other ships | 1.0 |

Corp ship craft skill requirement is derived from all rounded resource requirements plus relic and skull requirements:

```text
round((sum(resources) + relicRequirement * 100 + skullRequirement * 10) / 100)
```

## Stat Aggregation

Source: `Assembly-CSharp\GKFECKLMHGM.cs`, especially `CalculateStatBase(...)`, `GetMaxHull()`, `GetMaxShield()`, `GetPowerCapacity()`, `GetPowerRechargeRate()`, and `SumMaxEp()`.

This is the current working model for ship stats:

- The stat container dispatches every stat through `CalculateStatBase(...)`.
- Primary/full-slot items contribute their full stat value.
- Aux-slot items are multiplied by `MDAFDILCAGN`.
- For player ships, `MDAFDILCAGN = 0.1`, matching the 10% aux rule confirmed by Goot.
- For structures/NPC-like entities where `IMPOOFFJGKG` is true, `MDAFDILCAGN = 1`.
- `Get(...)` returns the diminishing-returns-adjusted value by default. Passing `false` returns the raw calculated value.

### Equip Points

`EquipPointMax` is:

```text
ship base EP + sum(full-slot item EquipPointMax) + sum(aux-slot item EquipPointMax)
```

Unlike ordinary aux stats, item `EquipPointMax` from aux slots is added in full in this client formula.

`EquipPointCost` is the sum of item EP costs across equipped items.

### Max Hull

For normal ships, max hull begins with:

```text
balance modifier * (1400 + entity level * 3)
```

Then the client adds full-slot item `MaxHull`, aux-slot `MaxHull * 0.1`, and applies the entity/structure multiplier. For normal ships the entity/structure multiplier is `1`.

Hull max technologies stack as a selected HullMax rank plus Advanced Alloys:

| Tech | Hull modifier |
|---|---:|
| HullMax1 | +5% |
| HullMax2 | +8% |
| HullMax3 | +11% |
| HullMax4 | +14% |
| HullMax5 | +17% |
| HullMax6 | +20% |
| HullMax7 | +23% |
| HullMax8 | +30% |
| AdvancedAlloys1 | +2% |
| AdvancedAlloys2 | +4% |

Only the highest present `HullMax#` branch is used. Advanced Alloys checks are separate and can add on top.

`JBCDDPCHFCM` is the computed level value from the XP helper (`DOFAMANMNJL` / `FOACJEKBFLG`). It is used by player level gates, ship labels, XP bars, and level sorting. For public wiki wording, call it `level`; for ships, `ship level` is reasonable when the context is clearly a ship.

### Max Shield

For normal ships, max shield is primarily equipment-driven:

```text
(sum(full-slot ShieldCapacity) + sum(aux-slot ShieldCapacity) * 0.1) * entity/structure multiplier
```

For normal ships the entity/structure multiplier is `1`.

Shield max technologies use the highest present ShieldMax rank:

| Tech | Shield modifier |
|---|---:|
| ShieldMax1 | +5% |
| ShieldMax2 | +8% |
| ShieldMax3 | +11% |
| ShieldMax4 | +14% |
| ShieldMax5 | +17% |
| ShieldMax6 | +20% |
| ShieldMax7 | +23% |

### Damage Modifiers

Source: `GKFECKLMHGM.GetOutgoingDamageMod()`, `GetIncomingDamageMod()`, `GetShieldDamageMod()`, and `GetHullDamageMod()`.

General pattern:

```text
stat = sum(full-slot item stat) + sum(aux-slot item stat) * aux multiplier + skill bonus
```

For normal player ships, aux multiplier is `0.1`.

Outgoing damage adds these technology/effect modifiers:

| Source | Outgoing damage modifier |
|---|---:|
| Overpower | +10% |
| Vanquisher | +15% |
| SmallStrikeTeamEffect | +5% |
| NanobotCharge | +10% |
| LeadershipEffect1 | +3% |
| LeadershipEffect2 | +5% |
| LeadershipEffect3 | +7% |
| Freighter1 | -50% |
| Freighter2 | -45% |
| Freighter3 | -40% |
| Freighter4 | -35% |
| Freighter5 | -30% |

Incoming damage adds:

| Source | Incoming damage modifier |
|---|---:|
| Overpower | +15% |
| EnemyTerritoryEffect | +10% |

Shield damage and hull damage use the general full-slot + aux + skill pattern. Hull damage is clamped to `0` minimum.

### Combat Action And Ability Rules

Sources:

- `Assembly-CSharp\GKFECKLMHGM.cs`
- `Assembly-CSharp\DDEIFGPEOMI.cs`
- `Assembly-CSharp\IKOLEGFOADL.cs`
- `Assembly-CSharp\JEKJDKMBIGN.cs`
- `Assembly-CSharp\PGJIDFCBFCC.cs`

Default power/action constants from `PGJIDFCBFCC.cs`:

| Mechanic | Default |
|---|---:|
| Minimum Hack/Grapple/Drain stat required to use that action | 10 |
| Base battery power capacity | 17 |
| Base battery recharge | 1.5 per second |
| Default Hack/Grapple/Drain cooldown | 50s |
| Default Scan cooldown | 40s |
| Default Cloak cooldown | 76s |
| Default Repair cooldown | 50s |
| Purge cooldown | 8s |

The client action validator blocks:

- Hack if `HackPower < 10`.
- Grapple if `GrapplePower < 10`.
- Drain if `BatteryDrainPower < 10`.
- Scan when the ship lacks scanning technology.
- Purge when the ship lacks Technician technology.
- Any ability whose cooldown is still running.
- Any ability whose battery power cost exceeds current battery power.

Ability cooldowns start from the defaults above. `SpeedHack`, `SpeedGrapple`, `SpeedDrain`, `SpeedRepair`, `SpeedScan`, and `SpeedCloak` style techs subtract `4s`, `6s`, or `8s` at ranks 1/2/3 through `GetSpeedTech1/2/3()`. Purge does not use these speed-tech reductions.

Repair cooldown is also modified by the best repair facility bonus:

| Repair facility | Cooldown multiplier |
|---|---:|
| RepairFacility1 | 90% |
| RepairFacility2 | 80% |
| RepairFacility3 | 70% |
| RepairFacility4 | 60% |

The same repair facility ranks add hull-repair stat bonuses in `GetHullRepairMod()`: `+10%`, `+15%`, `+20%`, and `+25%`.

Battery power capacity is:

```text
base power capacity + full-slot PowerCapacity + aux-slot PowerCapacity * aux multiplier + eligible battery capacity bonuses
```

Battery power recharge is:

```text
base recharge + full-slot PowerRecharge + aux-slot PowerRecharge * aux multiplier + PowerRecharge skill bonus
```

As with the other stat formulas on this page, normal player ships use `0.1` aux scaling and structures/NPC-like entities use `1.0`.

### Structure Multipliers Seen In Shared Stat Container

The same stat container is also used by structures. Keep the broader defense-unit rules in [Client Extracted Structures](Client-Extracted-Structures.md); this subsection only records the shared stat-container defaults from `PGJIDFCBFCC.cs`:

| Entity type | Hull/shield multiplier | Base hull term |
|---|---:|---:|
| Planet | 40 | 10000 |
| Garrison | 30 | 10000 |
| Outpost | 12 | 10000 |
| Shipyard | 12 | 10000 |
| Ship/default | 1 | 1400 |

For human superuser/admin-style entities (`IMPOOFFJGKG` and Human faction), max hull/shield short-circuit to very large values: `10,000,000` for planets and `1,000,000` otherwise. This should not be treated as player gameplay.

## Still Needed

- Confirm the public-facing meaning of `entity level` in the max hull formula.
- Separate normal ship stat formulas from shared structure/NPC handling before publishing public gameplay pages.
- Clean extraction of damage/stat formulas beyond max hull, max shield, power, movement, and EP.
- Public naming for any shipyard-only requirements versus player-level requirements.
- Confirmation whether current server data can override these client-side defaults.
