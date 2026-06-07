# Client Extraction Notes

Source: `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled`, current Steam client decompile supplied by Goot.

This page is a staging note for facts pulled from the client. Treat these as stronger than chat/training-data guesses, but still review before moving them into public-facing wiki pages. The decompile has readable model classes under `Assembly-CSharp\TibSharp\Expansion\Library`; many display strings and formulas live in obfuscated top-level helper classes.

## High-confidence data found

### Ship classes

Source enum: `Assembly-CSharp\NFLGBFKEKMC.cs`.

Client ship classes are:

- Shuttle
- Frigate
- Assassin
- Cruiser
- Destroyer
- Battleship
- Flagship
- Carrier
- Hades
- Emperor

### Factions

Source enum: `Assembly-CSharp\ONCHPJDOFKP.cs`.

Client factions are:

- Human
- Wyrd
- Pirate
- Het
- Precursor

### Ship mods

Source enum: `Assembly-CSharp\NNGLFJGGODO.cs`.

Confirmed ship mod enum values include:

- Medic
- Raider
- Interdictor
- RetroShuttle, RetroFrigate, RetroScorpion, RetroAssassin, RetroCorvette, RetroCruiser, RetroTitan, RetroFlayer, RetroDevastator, RetroDestroyer, RetroBattleship, RetroInvader, RetroExecutioner, RetroDespoiler, RetroAnnihilator, RetroDreadnaught, RetroFlagship, RetroCarrier, RetroReaper, RetroHades, RetroTerminus
- Freighter
- Paladin
- Ultimate
- DeceptionModule
- Unique
- Phoenix
- Gladiator

Follow-up ship mod extraction is staged in `Client-Extracted-Ships.md`:

- Client names and descriptions for technology mods and retro skins.
- `IsTechnologyMod()` and `IsRetroSkin()` helper classifications.
- Ship name suffixes for Medic, Raider, Interdictor, Freighter, Paladin, Ultimate, Phoenix, and Gladiator.
- Deterministic technology bonus mappings for Medic, Raider, Freighter, Paladin, Phoenix, Gladiator, and Interdictor Carrier.
- Ultimate and Unique slot/EP bonus behavior.
- Deception UI behavior, slot-hiding thresholds, and Disable Deception default Tech Point cost.
- Unique mod behavior is seed/context-dependent and has been summarized instead of flattened into public rules.

### Structures and defense units

Sources include:

- `Assembly-CSharp\EPGIECDJPJC.cs`
- `Assembly-CSharp\DFHOJHHBAMJ.cs`
- `Assembly-CSharp\IGDDJEMDJEJ.cs`
- `Assembly-CSharp\JEKJDKMBIGN.cs`
- `Assembly-CSharp\AHFAPFNMNPJ.cs`
- `Assembly-CSharp\IKOLEGFOADL.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\DefenseEntityDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\PlanetDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\GarrisonDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\OutpostDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\ShipyardDbObj.cs`

Follow-up structure extraction is staged in `Client-Extracted-Structures.md`:

- Entity type enum values and runtime class mapping.
- Shared defense DB fields and specific Planet/Garrison fields.
- Default corp defense caps: 4 Garrisons, 8 Outposts, 4 Shipyards.
- Build-cap Tech Point cost formulas and default costs.
- Defense base EP and weapon/drone/battery slot thresholds.
- Defense `Hardcore` and `EliteRank` fields as used by EP and labels.
- Stats ignored by defense entities and the `Repair`-only targeting helper.
- Default repair facility, Intimidation, Vanquisher, vision, and affinity techs.
- Resource defense XP formula, value modifiers, and default daily XP cap.
- Quick-jump rule branches needing gameplay review before public publication.

### Item families

Source enum: `Assembly-CSharp\FDBCCHMAKHF.cs`.

Client item families are:

- Weapon
- Armor
- Storage
- Drone
- Engine
- Computer
- Special
- Shield
- Battery
- Consumable

### Equipment slots

Source enum: `Assembly-CSharp\NOCCOHODGAD.cs`; ordered set source: `Assembly-CSharp\TibSharp\Expansion\Library\GearSet.cs`.

Client slot enum:

- Weapon1 through Weapon6
- Drone1 through Drone6
- Armor
- Storage
- Engine
- Computer
- Battery1 through Battery6
- Shield
- Special

Gear set ordering is:

1. Storage
2. Special
3. Computer
4. Engine
5. Shield
6. Armor
7. Weapon1 through Weapon6
8. Drone1 through Drone6
9. Battery1 through Battery6

### Equip Point formula

Source: `Assembly-CSharp\TibSharp\Expansion\Library\GearSet.cs`.

`GetRequiredEquipPoints()` sums each equipped item's EP cost, subtracts each equipped item's EP bonus, and floors the result at 0:

```text
required EP = max(0, sum(item EP cost) - sum(item EP bonus))
```

This confirms the wiki can safely describe EP requirement as a gear-set total, not as a separate per-slot rule. Exact item EP cost and ship/defense EP max tables still need extraction or observation.

### Player inventory defaults

Source: `Assembly-CSharp\TibSharp\Expansion\Library\Database\PlayerDbObj.cs`.

Client defaults:

- `ShipCap = 4`
- `ItemCap = 16`

The same model stores player skills, craft professions, free gift flags, missions, pity counters, artifact tech unlocks, boosts, and gear sets.

### Deployed fleet limits

Sources: `Assembly-CSharp\JEKJDKMBIGN.cs`, `Assembly-CSharp\IKOLEGFOADL.cs`, `Assembly-CSharp\PGJIDFCBFCC.cs`.

Client constants and checks confirm:

- Maximum deployed fleet size is `10` ships.
- Player level gates for deployed ships are 2 ships at level 0, 3 at 10, 4 at 20, 5 at 30, 6 at 40, 7 at 50, 8 at 75, 9 at 100, and 10 at 150.
- The 8th deployed ship requires the resulting fleet to contain at least one Small or Medium ship.
- The 9th and 10th deployed ships require the resulting fleet to contain at least two total Small or Medium ships.

Note: this is separate from `ShipCap`, which is the ship storage cap on the player model, not the deployed fleet limit.

Important stale-source warning: the bundled fallback wiki string in `AJDGBIOKNKA.cs` says the 9-ship fleet requires "a SMALL and MEDIUM or less" and the 10-ship fleet requires "a SMALL, MEDIUM and LARGE or less." The current client deployment check is more specific: the 8th ship requires at least one Small or Medium ship after the candidate, and the 9th/10th require at least two total Small or Medium ships. Prefer the runtime check over the fallback wiki text.

### Item metadata fields

Source: `Assembly-CSharp\TibSharp\Expansion\Library\Items\ItemDbObj.cs`.

Base item data includes:

- `Id`
- `Rarity`
- `Durability`
- `NoDrop`
- `Free`
- `Flag`
- `Quality`
- `Void`
- `Mutate`
- `Mutate2`
- `RepairDmg`
- `CraftTag`
- `OwnerId`
- `Loc`
- `Slot`
- `Auction`
- `CorpRank`

This supports the existing wiki split between item type, rarity, rank/quality, void, mutate, repair, ownership/location, and trade state.

### Shared item runtime rules

Source: `Assembly-CSharp\JCGFOGKIBPM.cs`, `Assembly-CSharp\OMPIMDNGMHG.cs`.

The client does not expose a single obvious static item-stat table in the decompiled code path. Item stats are calculated at runtime through `JCGFOGKIBPM.Get(stat)`, which dispatches to per-family formula properties and then adds mutate bonuses.

Confirmed shared item rules:

- Quality multiplier is `(void item ? 1.1 : 1.0) + qualityValue / 1000`.
- Item gear score is `round(rarity gear-score base * quality multiplier + item EP cost * rarity)`.
- Rarity gear-score bases are R1 25, R2 50, R3 100, R4 200, R5 300, R6 450, R7 700.
- Base required player levels by rarity are R1/R2/R3 0, R4 8, R5 12, R6 16, R7 20.
- Required level family multipliers are Weapon/Armor/Shield 100%, Storage 80%, Drone 115%, Engine 150%, Computer 125%, Special 175%, Battery 90%, Consumable 0.

### Rarity and quality

Sources: `Assembly-CSharp\AHKIAECFDDB.cs`, `Assembly-CSharp\DDOLLHDOKGI.cs`.

Rarity enum:

- R1
- R2
- R3
- R4
- R5
- R6
- R7

Quality enum:

- Terrible
- VeryLow
- Low
- Poor
- Fair
- Average
- Good
- High
- Superior
- Perfect
- Masterwork

The client also has upgrade bonus types for quality, discount, repair, and rarity:

- Quality5 through Quality9
- Discount16, Discount20, Discount24, Discount28, Discount32
- Repair30, Repair40, Repair50, Repair60, Repair70
- Rarity

### Stats

Sources: `Assembly-CSharp\GONOJAJJNCE.cs`, `Assembly-CSharp\AHFAPFNMNPJ.cs`.

Client stat enum and display names:

| Enum | Display name |
|---|---|
| EquipPointCost | EquipPoint Cost |
| EquipPointMax | EquipPoint Max |
| ResourceCapacity | Resource Max |
| MoveSpeedPercent | Move Speed |
| HullRepair | Hull Repair |
| OutgoingDamage | Damage Bonus |
| ShieldDamage | Shield Damage |
| IncomingDamage | Incoming Damage |
| XpBonus | Xp Bonus |
| MaxHull | Hull Max |
| CriticalDamage | Critical Damage |
| CriticalChance | Critical Chance |
| EvasionChance | Evasion Chance |
| BatteryDrainPower | Drain Power |
| GrapplePower | Grapple Power |
| HackPower | Hack Power |
| SplashChance | Splash Chance |
| HitChance | Hit Chance |
| HackResist | Hack Resist |
| GrappleResist | Grapple Resist |
| CriticalResist | Critical Resist |
| SplashResist | Splash Resist |
| BatteryDrainResist | Drain Resist |
| PowerRecharge | Power Recharge |
| PowerCapacity | Power Max |
| ShieldCapacity | Shield Max |
| ShieldPenetration | Shield Pierce |
| TargetingSpeedPercent | Targeting Speed |
| HullDamage | Hull Damage |

### Diminishing returns

Source: `Assembly-CSharp\AHFAPFNMNPJ.cs`.

The client flags diminishing returns for positive values on:

- OutgoingDamage
- ShieldDamage
- HullDamage
- CriticalDamage
- CriticalChance
- EvasionChance
- BatteryDrainPower
- GrapplePower
- HackPower
- SplashChance
- HitChance
- HackResist
- GrappleResist
- CriticalResist
- SplashResist
- BatteryDrainResist

The client flags diminishing returns for negative values on:

- IncomingDamage

Observed DR start thresholds:

| Stat group | DR starts at |
|---|---:|
| OutgoingDamage, ShieldDamage, HullDamage, IncomingDamage | 0.05 |
| CriticalDamage | 0.14 |
| CriticalChance, EvasionChance | 10 |
| BatteryDrainPower, GrapplePower, HackPower, SplashChance | 15 |
| HitChance | 20 |
| HackResist, GrappleResist, CriticalResist, SplashResist, BatteryDrainResist | 25 |

Need confirmation before public copy: exact DR curve after the start threshold.

### Skill-upgrade stats

Source: `Assembly-CSharp\AHFAPFNMNPJ.cs`.

Stats that can be upgraded as skills:

- ResourceCapacity
- HullRepair
- OutgoingDamage
- ShieldDamage
- IncomingDamage
- XpBonus
- CriticalDamage
- CriticalChance
- EvasionChance
- BatteryDrainPower
- GrapplePower
- HackPower
- SplashChance
- HitChance
- HackResist
- GrappleResist
- CriticalResist
- SplashResist
- BatteryDrainResist
- PowerRecharge
- ShieldPenetration
- HullDamage

Basic skill mod per point:

| Stat group | Basic per point |
|---|---:|
| ResourceCapacity | 1 |
| HullRepair, OutgoingDamage, ShieldDamage, XpBonus, CriticalDamage, ShieldPenetration, HullDamage | 0.005 |
| IncomingDamage | -0.005 |
| CriticalChance, EvasionChance, BatteryDrainPower, GrapplePower, HackPower, SplashChance, HitChance | 1 |
| HackResist, GrappleResist, CriticalResist, SplashResist, BatteryDrainResist | 1.5 |
| PowerRecharge | 0.01 |

Advanced skill mod per point:

| Stat group | Advanced per point |
|---|---:|
| ResourceCapacity | 0.5 |
| HullRepair, OutgoingDamage, ShieldDamage, XpBonus, CriticalDamage, ShieldPenetration, HullDamage | 0.0025 |
| IncomingDamage | -0.0025 |
| CriticalChance, EvasionChance, BatteryDrainPower, GrapplePower, HackPower, SplashChance, HitChance, HackResist, GrappleResist, CriticalResist, SplashResist, BatteryDrainResist | 0.5 |
| PowerRecharge | 0.005 |

### Technology enum

Source enum: `Assembly-CSharp\BCHEAEJKAJI.cs`; behavior helpers in `Assembly-CSharp\DFHOJHHBAMJ.cs`, `Assembly-CSharp\DDEIFGPEOMI.cs`, and UI usage in `UiManager.cs`.

The client has a large explicit technology enum. Families visible in the enum include:

- RepairFacility
- EvasiveManeuvers
- Intimidation
- Intuition
- SkipJump
- CrewFurnace
- Analysis
- HyperDrive
- SpaceLaneEffect
- Vorpal
- Targeting
- Junker
- Mechanic
- ShieldCapacitors
- ShieldAmplifier
- ShieldPierce
- Freighter
- Scavenger
- Harvesting
- AdvancedAlloys
- AdvancedHacking
- AdvancedGrappling
- AdvancedDraining
- SpeedHack
- SpeedGrapple
- SpeedDrain
- HullMax
- ShieldMax
- Leadership
- LeadershipEffect
- Interdictor
- InterdictorEffect
- GarrisonStrikes
- Overpower
- ReverseHacking
- ReverseGrappling
- ReverseBatteryDrain
- Deflector
- Technician
- RepairOverTimeEffect
- AlienDamage
- PvPDamage
- PvPBonusXP
- NovaInversion
- NovaDeath
- Regeneration
- Marauder
- Guardian
- AttackDrones
- RepairDrones
- SpeedRepair
- BattleRam
- LongRangeVision
- PassiveScan
- Stealth
- Scan
- AdvancedScanning
- SpeedScan
- Cloak
- AdvancedCloaking
- CloakDuration
- SpeedCloak
- Vanquisher
- Savior
- Rebirth
- SmallStrikeTeamEffect
- OnFireEffect
- CollisionEffect
- EnemyTerritoryEffect
- FriendlyTerritoryEffect
- ResourceLootBonusPvP
- PvPProtection
- NanobotCharge
- SneakAttack
- DailyTech
- ShieldRepair
- HackRam

Important behavior buckets found and now staged in `Client-Extracted-Technology.md`:

- `GetStacksWithOtherRanks()` for stackable-with-other-ranks tech groups.
- `IsMajor()` for client major-tech classification.
- `CanBeResearched()` for researchable technology groups.
- `CanDefenseHave()` for defense eligibility exclusions.
- `CanPaidTechPointBoost()` for boostable techs.
- `CanBeArtifact()` for artifact tech lists.
- `IsStatusEffect()` for status-effect techs.
- `GetMaxOverrideTech()` for max-rank override families.

### Craft skills

Source enum: `Assembly-CSharp\OJELMLGPPAN.cs`.

Client craft/profession skills:

- Scientist
- Engineer
- Weaponsmith
- Armorsmith
- Dronesmith

### Item class enums

These are item class lists, not full item stat tables.

| Item family | Source enum | Values / pattern |
|---|---|---|
| Armor | `JKENBAGPGFK` | Titanium, Composite, Carbide, Exoprene, Cytoplast, Holocrine, Diamond, Thorium, Osmium, Citadel, Ajax, Aegis, Kismet |
| Battery | `EAHJHMGGHGM` | Alkaic, Chromic, Galvanic, Mercuric, Voltaic, Hydric, Lithic, Zambic, Silic, Moltic, Polyanic, Radionic |
| Computer | `CAHAIADFHCG` | SAGE/TOIL/HAVOK/CABAL/AGENT/ICE/WARRIOR MK 1-4, A1-A3 variants, plus Victor variants |
| Consumable | `PIBAEAKHECA` | Portrait, ShipModification, ItemBlueprint, Title, resource piles, skull piles, relic piles, StatModification, QualityRepairKit, NanobotChargeKit, OblivionFragment, MutateItemKit, ReMutateItemKit, PartyBox, TechComputerUpgradeKit, VoidItemKit, ReVoidItemKit |
| Drone | `HAOJHDJLJFO` | LCD/HX/WP/DCD/BAS variants V1-V12 |
| Engine | `JOPMBBDJMIO` | Gravity, Skip, Impulse, Fusion, Atomic, Crux, Stealth, Neutron |
| Shield | `MMLDADJFCJM` | A/B/C/D/E variants V01-V12 |
| Special | `EJDCMKKAGOP` | Technician, Prospector, Tank, Scout, Hacker, Stalker, NovaDevice, BattleRam, AlienHunter, BountyHunter, Deflector, WeirdAlienArtifact, GrapplingHook, Vampire, AdvConstruct, AdvShields, AdvElectronics, AdvMunitions, AdvPropulsion, AlienTechnology, DroneMaster |
| Storage | `HEPGMEMIEFG` | Human/Pirate/Het/Wyrd/Precursor Hold, Vault, Arsenal, Archive, Armory, Munitions |
| Weapon | `LMAAOEMAHAH` | Large named list including Mutilator through MatterInverter; extract into a dedicated table before public use |

## What this does not give us yet

- Full per-item stat tables.
- Full per-ship stat tables.
- Full technology descriptions and exact rank effects.
- Exact Equip Point max by ship/defense class.
- Exact item EP cost formula by rank/rarity/quality.
- Security Rating spawn/level tables.
- Exact mission reward tables.

These may still be in the client, but are likely split across obfuscated helper classes or server-provided data, not the clean database model files.

## Recommended next extraction passes

1. Mine `DFHOJHHBAMJ.cs` for technology categories: researched, stackable, artifact, defense-only, paid boost, status effect.
2. Mine item runtime classes for `GetEPCost()`, `GetEPBonus()`, item display names, and stat generation.
3. Mine ship/runtime classes for EP max, class size, move timing, base stats, and mod behavior.
4. Mine mission helpers for mission type names, descriptions, and reward formula hints.
5. Only then update public pages, keeping raw extraction notes in Contributing.

## Second-pass extraction

### Ship size mapping

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`, method `GetSize(this NFLGBFKEKMC)`.

| Size | Ship classes |
|---|---|
| Small | Shuttle, Frigate, Assassin |
| Medium | Cruiser, Destroyer |
| Large | Battleship, Flagship |
| Huge | Carrier, Hades |
| Massive | Emperor |

This matches Goot's earlier correction on movement-size bands.

### Base ship Equip Points

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`, method `GetBaseEquipPoints(this NFLGBFKEKMC, ONCHPJDOFKP)`.

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

Notes:

- Human generally has the lowest base EP.
- Precursor generally has the highest base EP.
- Pirate Shuttle is the same as Human Shuttle; Wyrd and Het Shuttle are higher.

### Ship weapon slots

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`, method `GetMaxWeapons(this NFLGBFKEKMC, ONCHPJDOFKP)`.

| Ship / size rule | Human | Wyrd | Pirate | Het | Precursor |
|---|---:|---:|---:|---:|---:|
| Shuttle | 2 | 2 | 2 | 2 | 3 |
| Other small ships | 2 | 2 | 2 | 2 | 3 |
| Medium ships | 3 | 3 | 3 | 3 | 4 |
| Large ships | 4 | 4 | 4 | 4 | 5 |
| Carrier | 2 | 2 | 2 | 2 | 3 |
| Other huge ships | 5 | 5 | 5 | 5 | 6 |
| Emperor | 5 | 6 | 6 | 6 | 6 |

### Ship drone slots

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`, method `GetMaxDroneSlots(this NFLGBFKEKMC, ONCHPJDOFKP)`.

| Ship / size rule | Human | Wyrd | Pirate | Het | Precursor |
|---|---:|---:|---:|---:|---:|
| Shuttle | 2 | 2 | 2 | 3 | 2 |
| Assassin | 2 | 2 | 2 | 3 | 2 |
| Other small ships | 1 | 1 | 1 | 2 | 1 |
| Medium ships | 2 | 2 | 2 | 3 | 2 |
| Large ships | 3 | 3 | 3 | 4 | 3 |
| Carrier | 5 | 5 | 5 | 6 | 5 |
| Other huge ships | 3 | 4 | 4 | 5 | 4 |
| Emperor | 5 | 6 | 6 | 6 | 6 |

### Ship battery slots

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`, method `GetMaxBatterySlots(this NFLGBFKEKMC, ONCHPJDOFKP)`.

| Ship / size rule | Human | Wyrd | Pirate | Het | Precursor |
|---|---:|---:|---:|---:|---:|
| Shuttle | 1 | 2 | 1 | 1 | 1 |
| Frigate | 1 | 2 | 1 | 1 | 1 |
| Assassin | 2 | 3 | 2 | 2 | 2 |
| Other small ships | 1 | 2 | 1 | 1 | 1 |
| Medium ships | 2 | 3 | 2 | 2 | 2 |
| Large ships | 3 | 4 | 3 | 3 | 3 |
| Huge ships | 4 | 5 | 4 | 4 | 4 |
| Emperor | 5 | 6 | 6 | 6 | 6 |

### Required player level by ship and faction

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`, methods `GetRequiredPlayerLevel()` and `GetRequiredPlayerLevelMod()`.

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

Need wiki wording decision: these are client crafting/use requirements, but we should verify whether UI labels them as captain level, player level, or build requirement before public copy.

Follow-up shipyard/crafting extraction is staged in `Client-Extracted-Ships.md`:

- Move prep time defaults: Small/default 700ms, Medium 1000ms, Large 1300ms, Huge 1700ms, Massive 1700ms. Fast-path movement prep returns 500ms.
- Shipyard required level helper returns 0 for Human Shuttle through Human Flagship, otherwise the normal required player level.
- Required days-in-corp, default skull costs, default relic costs, resource requirement formula, ship craft multipliers, and corp ship craft skill formula are now extracted from `DFHOJHHBAMJ.cs`, `JEKJDKMBIGN.cs`, and `PGJIDFCBFCC.cs`.

### Item EP source behavior

Sources:

- `Assembly-CSharp\JCGFOGKIBPM.cs`, methods `GetEPCost()`, `GetEPBonus()`, and `CalculateStat()`.
- Item runtime classes: `EBNNOMPAHAF.cs`, `KKKEBKMMOBA.cs`, `KJEIOMFAJOC.cs`, `BBNPEFEJEEC.cs`, `OIBAMMKGNBK.cs`, `KOBILLCNLAJ.cs`, `KKHJOEBCGAP.cs`, `BNCBECFCPHP.cs`, `ECCOKHAPHDD.cs`, `NLLPDCFPKJM.cs`.

Confirmed:

- `GetEPCost()` returns the item's calculated `EquipPointCost` stat.
- `GetEPBonus()` returns the item's calculated `EquipPointMax` stat.
- `EquipPointCost` is backed by an internal item field named `OMIBOKEONLA`.
- `EquipPointMax` is backed by an internal item field named `AKAAAIOKMOP`.
- Base EP for several item families is stored directly on the item database object as `Ep` or exposed through the runtime object's base EP field.
- Consumables return base EP `0`.

Still unresolved:

- Exact item EP tables by item class/rank are not in one clean table yet.
- Need a third pass to see whether `Ep` values are generated from blueprint/crafting code, server-provided item XML, or another client data table.

### Item craft skill mapping

Source: `Assembly-CSharp\OMPIMDNGMHG.cs`, method `GetCraftSkill(this FDBCCHMAKHF)`.

| Item family | Craft skill |
|---|---|
| Weapon | Weaponsmith |
| Armor | Armorsmith |
| Shield | Armorsmith |
| Storage | Engineer |
| Computer | Engineer |
| Battery | Engineer |
| Drone | Dronesmith |
| Engine | Scientist |
| Special | Scientist |
| Consumable | None / NULL |

### Item long-name construction

Source: `Assembly-CSharp\OMPIMDNGMHG.cs`, method `GetItemClassLongName(this FDBCCHMAKHF, byte, byte)`.

The client constructs public item class names as:

| Item family | Naming pattern |
|---|---|
| Weapon | `[weapon class display name] Weapon` |
| Armor | `[armor class display name] Armor` |
| Storage | `[storage class display name] Storage` |
| Drone | `[drone class display name] [drone variant] Drone` |
| Engine | `[engine display name]` |
| Computer | `[computer display name] Computer` |
| Special | `[special display name] Special` |
| Shield | `[shield display name]` |
| Battery | `[battery display name]` |
| Consumable | `[consumable display name]` |

### Technology behavior buckets

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`.

Confirmed helper methods:

- `GetStacksWithOtherRanks()`
- `IsMajor()`
- `CanBeResearched()`
- `CanDefenseHave()`
- `CanPaidTechPointBoost()`
- `CanBeArtifact()`
- `IsStatusEffect()`
- `GetMaxOverrideTech()`
- `IsDailyTech()`

Public-safe summary:

- Some technology ranks stack with other ranks; others are override-style rank families where the highest applicable rank wins.
- `GetMaxOverrideTech()` confirms override families including Freighter, Scavenger, Harvesting, HullMax, ShieldMax, Deflector, AlienDamage, PvPDamage, NovaDeath, Regeneration, BattleRam, Scan, Cloak, HackRam, and several leadership/interdictor-related families.
- Defense units cannot use every technology. The client has explicit defense eligibility checks, and garrison-only tech is separately flagged.
- Paid Tech Point boosting is restricted to a curated subset, mostly rank-1 techs such as Analysis1, HyperDrive1, Targeting1, ShieldPierce1, Scavenger1, Harvesting1, SpeedHack1, SpeedGrapple1, SpeedDrain1, HullMax1, ShieldMax1, AlienDamage1, PvPDamage1, PvPBonusXP1, Marauder1, Guardian1, AttackDrones1, RepairDrones1, SpeedRepair1, SpeedScan1, CloakDuration1, and SpeedCloak1.
- Artifact eligibility is also restricted by explicit client logic, not "any technology can be an artifact."
- Status-effect techs include repair facility effects, space lane effects, leadership effects, interdictor effects, repair-over-time, small strike team, on-fire, collision, territory effects, resource loot bonus PvP, PvP protection, nanobot charge, sneak attack, and daily tech.

Recommended public-page handling:

- Use this now to correct broad technology explanations.
- Public technology pages can now be drafted from the extracted source sheets, but should group techs by gameplay purpose rather than dumping every helper flag into player-facing copy.

### Movement timing

Sources:

- `Assembly-CSharp\JEKJDKMBIGN.cs`, methods `GetBaseMoveSpeedMS()` and `GetMovePrepTime()`.
- `Assembly-CSharp\GKFECKLMHGM.cs`, methods `GetMoveSpeedMS()` and `GetModifiedMoveSpeedMS()`.
- Config backing class `Assembly-CSharp\PGJIDFCBFCC.cs`.

Confirmed formula:

```text
base move time ms = configured base + (ship size enum value * 500)
modified move time ms = base move time + base move time * MoveSpeedPercent
final move time ms = max(modified move time, configured minimum move time)
```

Default config values visible in the backing class:

- Configured base move time: `8000 ms`
- Configured minimum move time: `3000 ms`

Because size enum values are `Small = 1`, `Medium = 2`, `Large = 3`, `Huge = 4`, `Massive = 5`, the visible default base move times are:

| Size | Default base move time |
|---|---:|
| Small | 8.5s |
| Medium | 9.0s |
| Large | 9.5s |
| Huge | 10.0s |
| Massive | 10.5s |

Important caveat:

- The current client has a single visible `3000 ms` minimum in `GetModifiedMoveSpeedMS()`, but Goot has confirmed live hard minimums are size-specific: Small 3.0s, Medium 3.2s, Large 3.3s, Huge/Massive 3.5s. The size-specific clamp may be server-side, config-fed, or applied elsewhere. Public wiki should keep Goot's size-specific values and note that movement is ultimately clamped after modifiers.

Move prep / pre-jump animation:

- `GetMovePrepTime()` returns `500 ms` when the relevant fast/override flags are set.
- Otherwise, it returns configured prep times by size.
- Default visible config values are Small `700 ms`, Medium `1000 ms`, Large `1300 ms`, Huge `1700 ms`, Massive `1700 ms`.

Movement / Interdictor extraction:

- `GetMoveSpeedPercentMod()` combines item movement stats, aux-scaled movement stats, daily movement tech, FriendlyTerritory, HyperDrive, Hardcore flag, NanobotCharge, SpaceLane, and Interdictor penalty.
- Visible source effects:
  - Daily movement tech condition: `-20%`.
  - FriendlyTerritoryEffect: `-10%`.
  - HyperDrive1/2/3: `-10%`, `-15%`, `-20%`.
  - Hardcore ship flag: `-10%`.
  - NanobotCharge: `-10%`.
  - SpaceLaneEffect1/2/3: `-10%`, `-15%`, `-20%`.
  - InterdictorEffect1/2/3/4: `+15%`, `+20%`, `+25%`, `+30%`.
- `GetSpaceLaneBonus()` returns no Space Lane bonus for NPC/structure-like entities or while an Interdictor penalty is active.
- `GetInterdictorPenalty()` returns no penalty for NPC/structure-like entities or without sector/map context; otherwise it delegates to the map/sector interdictor controller.
- `CHCIGDNAAPI.GetInterdictorRank(...)` accepts Interdictor1/2/3/4 from the ship's primary carrier bonus tech or secondary/bonus tech.
- `OMMOANGJAIM` stores one active Interdictor source, one active penalty rank, and a dictionary of server-provided sector bonus rows.
- `HCGPPIPPAIJ` is the network update path that copies active source id, active rank, sector coordinates, and bonus rows into the client-side sector controller.
- The client confirms one active Interdictor source per sector, but not the server-side contested-sector tie-break rule. Training/chat says first-arrived or strongest-by-rank; keep that labeled as unconfirmed until we find the server rule or current observation.

### Technology names and descriptions

Source: `Assembly-CSharp\DFHOJHHBAMJ.cs`.

The client has display-name and description methods for `BCHEAEJKAJI` technologies. This confirms the next pass can produce a real technology table rather than an inferred list.

Confirmed examples:

| Technology | Client display name | Client description |
|---|---|---|
| SkipJump | Skip Jump | Very Fast Movement Speed |
| CrewFurnace | Crew Furnace | Fast Movement Speed |
| Analysis1 | Analysis | +10% XP Bonus |
| Analysis2 | Analysis II | +15% XP Bonus |
| Analysis3 | Analysis III | +20% XP Bonus |
| HyperDrive1 | HyperDrive | 10% Ship Movement Speed Bonus |
| HyperDrive2 | HyperDrive II | 15% Ship Movement Speed Bonus |
| HyperDrive3 | HyperDrive III | 20% Ship Movement Speed Bonus |
| SpaceLaneEffect1 | Space Lane Effect | 10% Ship Movement Speed Bonus (Blue Sector Lines) |
| SpaceLaneEffect2 | Space Lane Effect II | 15% Ship Movement Speed Bonus (Blue Sector Lines) |
| SpaceLaneEffect3 | Space Lane Effect III | 20% Ship Movement Speed Bonus (Blue Sector Lines) |
| Vorpal1 | Vorpal Rank 1 | Attacks versus enemies below 5% health always critical |
| Vorpal2 | Vorpal Rank 2 | Attacks versus enemies below 10% health always critical |
| Vorpal3 | Vorpal Rank 3 | Attacks versus enemies below 15% health always critical |
| Vorpal4 | Vorpal Rank 4 | Attacks versus enemies below 20% health always critical |
| Targeting1 | Targeting | 5% Weapon & Drone Targeting Speed Bonus |
| Targeting2 | Targeting II | 10% Weapon & Drone Targeting Speed Bonus |
| Targeting3 | Targeting III | 15% Weapon & Drone Targeting Speed Bonus |

Recommended next action:

- Generate a full technology extraction table from `DFHOJHHBAMJ.cs` by pairing every `GetName(this BCHEAEJKAJI)` case with its `GetDescription(this BCHEAEJKAJI, ...)` case, then add behavior flags from the helper methods above.

## Technology extraction table

Source-backed staging page:

- `Client-Extracted-Technology.md`

What is now extracted:

- Full `BCHEAEJKAJI` enum order.
- Client display name for each technology when `GetName(this BCHEAEJKAJI)` provides one.
- Client description for each technology when `GetDescription(this BCHEAEJKAJI, ...)` provides one.
- Runtime-confirmed numerical effects for movement, targeting, XP, evasion, hit chance, hull/shield max, outgoing/incoming damage, Freighter damage penalties, Interdictor penalties, and RepairFacility hull-repair bonuses.
- Exact Regeneration rank descriptions from `JEKJDKMBIGN.GetRegenerationTechHull(...)` and `PGJIDFCBFCC` defaults:
  - Regeneration1: 25 hull every 30 seconds.
  - Regeneration2: 50 hull every 30 seconds.
  - Regeneration3: 75 hull every 30 seconds.
  - Regeneration4: 100 hull every 30 seconds.
  - Regeneration5: 150 hull every 30 seconds.
  - Regeneration6: 200 hull every 30 seconds.
  - Regeneration7: 250 hull every 30 seconds.
- Daily tech generic categories from `GetDailyTechGenericDescription(this ENIALFMHHLL)`.
- Daily tech exact variant descriptions from `GetDailyTechDescription(this ENIALFMHHLL, byte)`.
- Technology helper classifications for effect remaps, stealth/scanning/Deflector/PvP helper families, status effects, researchable techs, stackable-with-other-ranks techs, major techs, defense eligibility, paid tech-point boost candidates, artifact candidates, and max-rank override families.

Public-page handling:

- The extracted table should be treated as a source sheet, not as final wiki copy.
- Public technology pages should group techs by gameplay purpose and link to dedicated rules pages rather than repeat long descriptions everywhere.
- Daily tech entries need special care because the client describes them as dynamic random bonuses; public pages should explain the mechanic separately from the current daily roll.

Still unresolved in technology:

- A generated per-technology boolean matrix would still be useful for auditing, but the helper behavior is now staged in grouped form.

## Item class extraction table

Source-backed staging page:

- `Client-Extracted-Items.md`

What is now extracted:

- Weapon class display names, alternate variant names when the client's `GetName(this LMAAOEMAHAH, int)` argument equals `1`, and weapon faction mapping.
- Armor, battery, computer, drone, engine, shield, special, and storage class display names.
- Faction mapping for item families where the client has direct `GetFaction(...)` helper methods.
- Family DB payload fields, including which families store a direct `Ep` rank field.
- Fake-item preview path and default crafted preview start EP/rank.

Important handling notes:

- This table is raw class/display-name extraction, not a finished public item guide.
- Weapon alternate names need a targeted pass to confirm what the second `GetName(...)` argument represents in gameplay.
- Drone full item names are assembled from both a base drone class and a drone variant enum. The current table covers the base drone class names only.
- Consumable class, metadata, pile count, default rarity, craft category, EP, credit, quality repair, nanobot rarity, and CPU-upgrade decoding details are now staged in the consumable sections.

Still unresolved in items:

- Exact item EP cost tables by class/rank/rarity.
- Exact stat tables for each item class.
- Confirm whether any server-only consumable values exist beyond the named `PIBAEAKHECA` client enum.
- Whether live crafted/dropped item starting ranks always match the client preview default.

### Item stat coverage map

Source-backed staging page:

- `Client-Extracted-Item-Stat-Coverage.md`

What is now extracted:

- Runtime item-family stat override coverage for weapons, armor, storage, drones, engines, computers, specials, shields, batteries, and consumables.
- A summary matrix showing which item families have custom client logic for each stat.
- Source line references for each family/stat override.

Important handling notes:

- Coverage does not mean every item class in that family grants the stat. Many overrides contain switch statements and return `0` for most classes.
- This page is a roadmap for formula extraction, not a public stat table.
- The next useful pass is formula normalization by family, starting with simpler families before weapons/drones/computers/specials.

### Narrow item stat formula extraction

Source-backed staging page:

- `Client-Extracted-Item-Stat-Formulas-Narrow.md`

What is now extracted:

- Raw stat override bodies for shields, engines, and batteries, plus normalized helper sections for computers, specials, drones, and consumables.
- Source line references and obfuscated property names for each extracted formula.
- Context notes for common runtime fields like rarity, shared stat multiplier, class enum, and data-fed rank/base EP.

Important handling notes:

- This page is intentionally closer to source code than public wiki copy.
- Several formulas depend on helper methods such as shield `InternalGetResistMod()` or engine/battery helper methods. Many of those helpers are now translated, but public reference tables still need a careful normalization pass before publishing.
- This extraction should be used to build normalized family pages, not copied directly into gameplay pages.
- Follow-up helper pass added translated shield helper tables, engine/battery faction mappings, and battery power aggregation notes to `Client-Extracted-Item-Stat-Formulas-Narrow.md`.
- Follow-up family passes added computer technology/EP-max mappings, special technology/slot/immunity mappings, drone action/EP/credit mappings, and consumable metadata/kit mappings.

### Battery power mechanics

Sources:

- `Assembly-CSharp\GKFECKLMHGM.cs`, `GetPowerCapacity()` and `GetPowerRechargeRate()`.
- `Assembly-CSharp\PGJIDFCBFCC.cs` defaults.
- `Assembly-CSharp\IKOLEGFOADL.cs` hack/grapple/drain power requirement checks.

Confirmed client defaults:

| Mechanic | Value |
|---|---:|
| Base power capacity | 17 |
| Base power recharge | 1.5 per second |
| Minimum Hack/Grapple/Drain power to use the action | 10 |

Power capacity is base capacity plus full-slot item `PowerCapacity`, aux-slot `PowerCapacity` multiplied by the aux multiplier, and eligible battery capacity bonuses. Battery capacity bonuses apply when the ship is Pirate or when the ship faction matches the battery faction. If the result is above base capacity, the client applies another multiplier whose name/default still needs confirmation.

Power recharge is base recharge plus full-slot item `PowerRecharge`, aux-slot `PowerRecharge` multiplied by the aux multiplier, and skill bonus to `PowerRecharge`. A ship/player flag adds `+0.05` recharge before a final multiplier whose name/default still needs confirmation.

### Combat action and cooldown mechanics

Sources:

- `Assembly-CSharp\DDEIFGPEOMI.cs`
- `Assembly-CSharp\IKOLEGFOADL.cs`
- `Assembly-CSharp\JEKJDKMBIGN.cs`
- `Assembly-CSharp\PGJIDFCBFCC.cs`

Confirmed:

- Minimum Hack/Grapple/Drain stat required to use the matching action is `10`.
- Default cooldowns: Hack/Grapple/Drain `50s`, Scan `40s`, Cloak `76s`, Repair `50s`, Purge `8s`.
- Speed techs subtract `4s`, `6s`, or `8s` from matching ability cooldowns.
- RepairFacility1-4 modify Repair cooldown to `90%`, `80%`, `70%`, or `60%` of the post-speed-tech cooldown.
- Purge requires Technician technology and does not use speed-tech cooldown reductions.
- These are staged in `Client-Extracted-Ships.md` under combat action rules.

### Ship/stat aggregation findings

Source: `Assembly-CSharp\GKFECKLMHGM.cs`.

Follow-up ship stat extraction is staged in `Client-Extracted-Ships.md`.

Confirmed:

- The gear/stat container dispatches stats through `CalculateStatBase(...)`.
- Normal player ships use an aux stat multiplier of `0.1`.
- Structure/NPC-like entities where `IMPOOFFJGKG` is true use an aux multiplier of `1`.
- `Get(stat, true)` returns diminishing-returns-adjusted values where DR applies; `Get(stat, false)` returns raw calculated values.
- Normal ship `EquipPointMax` is base ship EP plus full-slot item `EquipPointMax` plus aux-slot item `EquipPointMax` in full.
- Normal ship max hull starts from `balance modifier * (1400 + level * 3)`, then adds item hull and tech modifiers. Here `level` is the computed XP-derived level value.
- Normal ship max shield is equipment-driven: full-slot shield capacity plus 10% aux shield capacity, then tech modifiers.
- Outgoing/incoming/shield/hull damage modifiers use the same full-slot + 10% aux + skill-bonus pattern for normal ships.
- Outgoing damage has source-backed modifiers for Overpower, Vanquisher, SmallStrikeTeamEffect, NanobotCharge, LeadershipEffect ranks, and Freighter ranks. These are staged in `Client-Extracted-Ships.md`.
- Shared structure defaults in this stat container: Planet multiplier 40, Garrison 30, Outpost 12, Shipyard 12, each with base hull term 10000.

Needs confirmation before public use:

- Server data can override at least many client balance constants: `JEKJDKMBIGN` exposes values from a static `PGJIDFCBFCC` object, and `OPDJFCNPEMJ` deserializes network/config payloads into that object. Use `PGJIDFCBFCC` initializers as defaults/fallbacks unless the live value is also confirmed.

### Level / XP extraction

Sources:

- `Assembly-CSharp\DOFAMANMNJL.cs`
- `Assembly-CSharp\GGLDHLJHGPO.cs`
- `Assembly-CSharp\FOACJEKBFLG.cs`
- `Assembly-CSharp\TibXpBar.cs`

Confirmed:

- `JBCDDPCHFCM` is the computed level value, derived from stored integer XP.
- Stored XP is `DJDFNOOGGMJ`; for ships/entities this comes from `CombatEntityDbObj.Xp`.
- `FOACJEKBFLG.GetLevelAsDouble(xp)` converts XP to fractional level.
- Level caps at `500.0` when XP is at least `235,261,135`.
- XP below `540` maps to integer level 1.
- The XP bar uses the fractional part of level as progress to the next level.
- A full client XP threshold table is staged in `Client-Extracted-Level-XP.md`.

### Crafting extraction

Sources:

- `Assembly-CSharp\FOACJEKBFLG.cs`
- `Assembly-CSharp\AJCLEHJNBNJ.cs`

Confirmed:

- `AJCLEHJNBNJ.GetCraftingQuality(totalCrafts, divisor, out craftingLevel, out cooldownHours)` calls `FOACJEKBFLG.GetCraftCooldownHours(totalCrafts)` and `FOACJEKBFLG.GetCraftingLevel(totalCrafts, divisor)`.
- The returned crafting level is passed to `JCGFOGKIBPM.GetQualityType(...)` to determine quality.
- If `divisor > 1`, total crafts are integer-divided by the divisor before crafting-level thresholds are checked.
- Craft cooldown returns `0` for `totalCrafts <= 333`.
- Full threshold tables are staged in `Client-Extracted-Crafting.md`.

### Item EP cost formulas

Sources:

- `Assembly-CSharp\JCGFOGKIBPM.cs`, `GetEPCost()`, `CalculateStat(...)`.
- `Assembly-CSharp\EBNNOMPAHAF.cs` weapons.
- `Assembly-CSharp\KKKEBKMMOBA.cs` armor.
- `Assembly-CSharp\KJEIOMFAJOC.cs` storage.
- `Assembly-CSharp\BNCBECFCPHP.cs` shields.
- `Assembly-CSharp\BBNPEFEJEEC.cs` drones.
- `Assembly-CSharp\OIBAMMKGNBK.cs` engines.
- `Assembly-CSharp\KOBILLCNLAJ.cs` computers.
- `Assembly-CSharp\KKHJOEBCGAP.cs` specials.
- `Assembly-CSharp\ECCOKHAPHDD.cs` batteries.
- `Assembly-CSharp\NLLPDCFPKJM.cs` consumables.

Confirmed:

- `GetEPCost()` returns the calculated `EquipPointCost` stat.
- `EquipPointCost` is backed by each item class's `OMIBOKEONLA` property.
- For weapons, armor, and storage:

```text
EP cost = max(0, item rank - item rarity + 1)
```

Here `item rank` is the runtime/db `Ep` value used in strings like `Rank X Weapon`, and `item rarity` is the rarity enum value.

- For shields:

```text
EP cost = max(0, item rank - item rarity + 1 + shield faction EP modifier)
```

Shield faction EP modifiers:

| Faction | Modifier |
|---|---:|
| Human/default | 0 |
| Pirate | 1 |
| Het | 2 |
| Wyrd | 3 |
| Precursor | 4 |

- For drones, base EP cost is computed from drone variant/category, faction, and rarity instead of the item rank field.

Drone category modifier:

| Drone category | Modifier |
|---|---:|
| Repair | 1 |
| Fighter | 2 |
| Other | 0 |

Drone special case modifier:

- `BAS_V12` Repair drones subtract 1.
- `BAS_V6` Harvest drones subtract 1.

Drone base EP cost before final clamp:

| Drone faction | Default/R1/R2 | R3/R4 | R5/R6 | R7 |
|---|---:|---:|---:|---:|
| Human/default | category mod | category mod | category mod - 1 | category mod - 2 |
| Pirate | category mod + 1 | category mod | category mod - 1 | category mod - 2 |
| Het | category mod + 2 | category mod + 1 | category mod | category mod - 1 |
| Wyrd | category mod + 3 | category mod + 2 | category mod + 1 | category mod |
| Precursor | category mod + 4 | category mod + 3 | category mod + 2 | category mod + 1 |

The runtime clamps negative drone EP values to 0 after computing this table.

- Engines, computers, specials, batteries, and consumables return `0` for base `EquipPointCost` in the runtime classes checked.

Important caveat:

- This does not yet give a full item EP table because item rank/base `Ep` values for weapons, armor, storage, and shields are still data-fed through DB objects rather than a single obvious static table in the client source.

## Loot, rewards, and cargo extraction

Public/contributor page updated: `Client-Extracted-Loot-Rewards.md`.

Confirmed from the client:

- Cargo reward entity payloads:
  - `CargoMoney`: `Credits`, `Skulls`.
  - `CargoItem`: `ItemId`.
  - `CargoResource`: `Resource`, `Count`.
- Client-visible consumable pile counts:
  - Resources: `100`, `500`, `1000`, `5000`.
  - Skulls: `10`, `100`, `500`, `1000`.
  - Relics: `1`, `5`, `10`, `50`, `100`.
- `GetScavengerRank()` and `GetHarvestingRank()` choose the highest active rank.
- Scavenger client text is `2%` through `14%` fleet Resource & Loot Bonus Chance in steps of 2.
- Harvesting client text is `5%` through `35%` Resource Harvest Bonus Chance in steps of 5 and says it grants XP from asteroids.
- Party Box activity enum values include Invasion, NPC defense busts, Missions, Assassin, faction hunts, and one-shot Overpower Advanced buffs for Critical/Repair/Grapple/Hack/Harvest.
- Party Box max-count helper:
  - Missions: default 3, R4 5, R5 7, R6 9, R7 15.
  - Assassin leaders: default 3, R4 5, R5 10, R6 15, R7 20.
  - Faction hunts: default 10, R4 15, R5 25, R6 35, R7 50.
  - Invasion and NPC defense bust activities default to 1 in the helper.
- Daily/event reward descriptions include Mission Rewards Doubled, Arena Awards Bonus Loot and Skulls, Pirate & Alien Defense Units Drop Bonus Loot, Double Rewards for Alliance Defense Kills, Hardcore/Homeworld double loot, invasion/assassin blueprint rewards, holiday gem loot, and always-drop Void Loot states.

Important caveat:

- Actual drop rolls, pity progression formulas, reward issuance, and live event state are not proven by these client helpers. Public rule pages should label those as training/server-observed unless we find server-side formulas or enough current observations.

## Faction-difference extraction

Public/contributor page updated: `Client-Extracted-Factions.md`.

Confirmed faction-specific mechanics now have a single contributor summary:

- Faction enum order: `NULL`, Human, Wyrd, Pirate, Het, Precursor.
- Ship differences:
  - Human has lower required levels and half default Skull costs for advanced ship crafting.
  - Precursor has the highest base EP trend and +1 weapon slot on Small through Huge/special cases.
  - Het has +1 drone slot on most sizes/special cases.
  - Wyrd has +1 battery slot on Small through Huge/special cases.
  - Human has the Massive/Emperor slot exceptions and Human Shuttle through Human Flagship shipyard shortcut.
- Defense affinity defaults:
  - Wyrd: Shield Capacitors and Advanced Hacking.
  - Pirate: Advanced Alloys and Attack Drones.
  - Het: Shield Pierce and Technician.
  - Precursor: Shield Amplifier and Advanced Draining.
- Item differences:
  - Shield capacity/resist/EP modifiers vary by faction.
  - Drone EP, harvest timing, harvest amount, and attack/repair formulas vary by faction.
  - Battery capacity bonuses apply for Pirate ships or matching ship/battery faction.

Public page guidance:

- Faction lore stays in World/Factions pages.
- Mechanics should link to canonical Ships/Items/Structures/Crafting pages.
- Best-faction or build-order claims belong in Strategy and should be labeled as community guidance.
