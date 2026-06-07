# Client-Extracted Items

Hidden contributor staging page. This is raw client-extracted item class/display-name data from the current 2.1.0 Steam client decompile. Use it as a source sheet for public item pages, not as final copy.

Source files:

- `Assembly-CSharp\JCGFOGKIBPM.cs` shared item runtime rules
- `Assembly-CSharp\OMPIMDNGMHG.cs` item family `GetName(...)`, `GetFaction(...)`, and related helper methods
- Item class enum files such as `LMAAOEMAHAH.cs`, `JKENBAGPGFK.cs`, `HAOJHDJLJFO.cs`, and related files

Notes:

- These tables identify client-visible item class names and faction mappings where the client exposes a direct mapping.
- Weapon names have a second variant column because the client `GetName(this LMAAOEMAHAH, int)` swaps names when the second argument equals `1`. The exact gameplay meaning of that argument still needs a targeted pass.
- Drone full names also include a drone variant from a separate enum in `GetItemClassLongName(...)`; this page currently stages the base drone class names only.
- Consumables often depend on metadata, rarity, or item blueprint contents; use the consumable class and metadata notes below before turning them into public copy.

## Shared item runtime rules

Source: `JCGFOGKIBPM.cs`.

### Stat calculation

Runtime item stats are calculated properties, not a flat static item-stat table in the decompiled code. `JCGFOGKIBPM.Get(stat)` fills a cached stat array by dispatching each `GONOJAJJNCE` stat to an item-family property such as `EquipPointCost`, `ResourceCapacity`, `MoveSpeedPercent`, `ShieldCapacity`, and so on.

After the family formula runs, mutate stat bonuses are added if the item has mutate fields set. Source-backed public stat tables therefore need to account for item family, item class/category/faction, rarity, EP/rank field where present, quality multiplier, void state, mutate bonuses, and family-specific balance mod fields.

### Quality multiplier

Source: `JCGFOGKIBPM.SetQualityValueCache(...)`.

The cached item quality multiplier is:

```text
quality multiplier = (void item ? 1.1 : 1.0) + qualityValue / 1000
```

`qualityValue` is the stored signed quality byte. The client maps the same value to public quality names:

| Quality value range | Quality name |
|---|---|
| less than -120 | Terrible |
| -120 to -101 | VeryLow |
| -100 to -71 | Low |
| -70 to -41 | Poor |
| -40 to -11 | Fair |
| -10 to 9 | Average |
| 10 to 39 | Good |
| 40 to 69 | High |
| 70 to 99 | Superior |
| 100 to 119 | Perfect |
| 120+ | Masterwork |

### Gear score

Source: `JCGFOGKIBPM.AFOHFGPEFDH` and `OMPIMDNGMHG.GetGearScoreBase(...)`.

Item gear score is:

```text
round(rarity gear-score base * quality multiplier + item EP cost * rarity)
```

Rarity gear-score bases:

| Rarity | Gear-score base |
|---|---:|
| R1 | 25 |
| R2 | 50 |
| R3 | 100 |
| R4 | 200 |
| R5 | 300 |
| R6 | 450 |
| R7 | 700 |

### Required player level

Source: `JCGFOGKIBPM.GetRequiredLevel(rarity, itemFamily)`.

Base required levels by rarity:

| Rarity | Base required level |
|---|---:|
| R1 | 0 |
| R2 | 0 |
| R3 | 0 |
| R4 | 8 |
| R5 | 12 |
| R6 | 16 |
| R7 | 20 |

Item-family multipliers:

| Item family | Required level rule |
|---|---:|
| Weapon | base |
| Armor | base |
| Shield | base |
| Storage | base * 80% |
| Drone | base * 115% |
| Engine | base * 150% |
| Computer | base * 125% |
| Special | base * 175% |
| Battery | base * 90% |
| Consumable | 0 |

Integer math is used for the family multipliers.

## EP cost notes

Source-backed formula notes are in `Client-Extraction-Notes.md`.

Short version:

- Weapons, armor, and storage use `max(0, item rank - item rarity + 1)`.
- Shields use the same pattern plus a shield-faction modifier: Human/default 0, Pirate 1, Het 2, Wyrd 3, Precursor 4.
- Drones use a separate faction/category/rarity table and then clamp negative values to 0.
- Engines, computers, specials, batteries, and consumables return 0 base EP cost in the checked runtime classes.
- Exact rank/base `Ep` values for weapons, armor, storage, and shields are still data-fed and need a deeper data-table pass.

## Item DB Payload And Rank Fields

Sources:

- `Assembly-CSharp\TibSharp\Expansion\Library\Items\WeaponDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\ArmorDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\StorageDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\ShieldDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\DroneDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\EngineDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\ComputerDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\SpecialDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\BatteryDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Items\ConsumableItemDbObj.cs`
- `Assembly-CSharp\OMPIMDNGMHG.cs`
- `Assembly-CSharp\UiManager.cs`
- `Assembly-CSharp\PGJIDFCBFCC.cs`

The concrete item DB subclasses show which item families store a direct `Ep` rank field:

| Item family | DB class | Family-specific DB fields found | Direct `Ep` rank field? |
|---|---|---|---|
| Weapon | `WeaponDbObj` | `Class`, `Ep`, `Variant`, `BalanceMod` | yes |
| Armor | `ArmorDbObj` | `Class`, `Ep`, `BalanceMod` | yes |
| Storage | `StorageDbObj` | `Class`, `Ep` | yes |
| Shield | `ShieldDbObj` | `Class`, `Ep`, `BalanceMod` | yes |
| Drone | `DroneDbObj` | `Class`, `Category`, `BalanceMod` | no |
| Engine | `EngineDbObj` | `Class` | no |
| Computer | `ComputerDbObj` | `Class` | no |
| Special | `SpecialDbObj` | `Class` | no |
| Battery | `BatteryDbObj` | `Class` | no |
| Consumable | `ConsumableItemDbObj` | `Class`, `Metadata` | no |

`OMPIMDNGMHG.AssignClassByte(...)` confirms that the fake-item/previews path passes the `epRank` argument into only Weapon, Armor, Storage, and Shield runtime objects. Drone uses the second byte as `Category`; Consumable uses the second byte as metadata for selected consumable classes.

The item-version inspection helper uses `JEKJDKMBIGN.IJDFDKAKHOG` as the starting EP/rank for generated previews. The visible default in `PGJIDFCBFCC.cs` is:

```text
crafted item start EP/rank = 6
```

Important distinction: this is a preview/default generation value. It is not proof that all crafted or dropped items start at rank 6 in live gameplay.

## Weapon classes

| Enum | Client name | Variant name when argument is `1` | Faction |
|---|---|---|---|
| NULL |  |  |  |
| Mutilator | Mutilator | Piercer | Precursor |
| Starshatter | Starshatter | Pervader | Precursor |
| Striker | Striker | Negspace Rifle | Precursor |
| Exterminator | Exterminator | Neutralizer | Precursor |
| Voidblaster | Voidblaster | Opposer | Precursor |
| Ravager | Ravager | Invalidator | Precursor |
| Brutalizer | Brutalizer | Nullifier | Precursor |
| Vaporizer | Vaporizer | Subduer | Precursor |
| Desolator | Desolator | Permeator | Precursor |
| Atomizer | Atomizer | Breacher | Precursor |
| Corruptor | Corruptor | Transverser | Precursor |
| Mindslayer | Mindslayer | Defier | Precursor |
| Riftbreaker | Riftbreaker | Anullifier | Precursor |
| Soultaker | Soultaker | Attestor | Precursor |
| Nullcannon | Nullcannon | Foiler | Precursor |
| Demolisher | Demolisher | Deposer | Precursor |
| Incinerator | Incinerator | Negator | Precursor |
| Eradicator | Eradicator | QuanTunneler | Precursor |
| Rapture | Rapture | Ecstasy | Het |
| Glory | Glory | Elation | Het |
| Oblivion | Oblivion | Euphoria | Het |
| Horror | Horror | Exaltation | Het |
| Ruin | Ruin | Bliss | Het |
| Cataclysm | Cataclysm | Nirvana | Het |
| Torment | Torment | Serenity | Het |
| Smolder | Smolder | Exhilaration | Het |
| Destruction | Destruction | Mirth | Het |
| Frenzy | Frenzy | Fervor | Het |
| Silence | Silence | Ardor | Het |
| Exodus | Exodus | Muse | Het |
| Darkness | Darkness | Zeal | Het |
| Agony | Agony | Solemnity | Het |
| Prophecy | Prophecy | Dream | Het |
| Radiance | Radiance | Trance | Het |
| Animus | Animus | Delight | Het |
| Pain | Pain | Paradise | Het |
| Screamer | Screamer | Siren | Wyrd |
| Succubus | Succubus | Incubus | Wyrd |
| Banshee | Banshee | Revenant | Wyrd |
| Basilisk | Basilisk | Cockatrice | Wyrd |
| Harpy | Harpy | Sphinx | Wyrd |
| Wyvern | Wyvern | Drake | Wyrd |
| Viper | Viper | Asp | Wyrd |
| Ripper | Ripper | Shredder | Wyrd |
| Penetrator | Penetrator | Impacter | Wyrd |
| Serpent | Serpent | Adder | Wyrd |
| Hydra | Hydra | Typhoon | Wyrd |
| Firecat | Firecat | Skiver | Wyrd |
| Hellcannon | Hellcannon | Inferno Rifle | Wyrd |
| Ophidian | Ophidian | Tarasque | Wyrd |
| Behemoth | Behemoth | Bahamut | Wyrd |
| Gargoyle | Gargoyle | Golem | Wyrd |
| Kraken | Kraken | Jormungand | Wyrd |
| Dragon | Dragon | Tiamat | Wyrd |
| BurstCannon | Burst Cannon | Flak Cannon | Pirate |
| ProtonLauncher | Proton Launcher | Neutron Ejector | Pirate |
| AutoCannon | Auto Cannon | Transmech Rifle | Pirate |
| FusionBeam | Fusion Beam | Abs-Z Emitter | Pirate |
| Phaser | Phaser | Particle Cannon | Pirate |
| MassDriver | Mass Driver | Helix Driver | Pirate |
| GaussCannon | Gauss Cannon | Coilgun | Pirate |
| MeasonBlaster | Meson Blaster | Boson Blaster | Pirate |
| OmegaRifle | Omega Rifle | Alpha Rifle | Pirate |
| Leviathan | Leviathan | Griffon | Pirate |
| Accelerator | Accelerator | Synchrotron | Pirate |
| RailGun | Rail Gun | Helical Railgun | Pirate |
| Disruptor | Disruptor | Violator | Pirate |
| GravitySmasher | Gravity Smasher | Graviton Gun | Pirate |
| Pulverizer | Pulverizer | Decimater | Pirate |
| IonCannon | Ion Cannon | Cation Cannon | Pirate |
| PlasmaLance | Plasma Lance | Phasic Lance | Pirate |
| MatterInverter | Matter Inverter | Matter Reverter | Pirate |

## Armor classes

| Enum | Client name | Faction |
|---|---|---|
| NULL |  |  |
| Titanium | Titanium | Human |
| Composite | Composite | Pirate |
| Carbide | Carbide | Human |
| Exoprene | Exoprene | Het |
| Cytoplast | Cytoplast | Het |
| Holocrine | Holocrine | Het |
| Diamond | Diamond | Wyrd |
| Thorium | Thorium | Pirate |
| Osmium | Osmium | Wyrd |
| Citadel | Citadel | Precursor |
| Ajax | Ajax | Precursor |
| Aegis | Aegis | Precursor |
| Kismet | Kismet | Precursor |

## Battery classes

| Enum | Client name | Faction |
|---|---|---|
| NULL |  |  |
| Alkaic | Alkaic Battery | Pirate |
| Chromic | Chromic Battery | Pirate |
| Galvanic | Galvanic Battery | Pirate |
| Mercuric | Mercuric Battery | Human |
| Voltaic | Voltaic Battery | Het |
| Hydric | Hydric Battery | Het |
| Lithic | Lithic Battery | Human |
| Zambic | Zambic Battery | Wyrd |
| Silic | Silic Battery | Wyrd |
| Moltic | Moltic Battery | Precursor |
| Polyanic | Polyanic Battery | Precursor |
| Radionic | Radionic Battery | Precursor |

## Computer classes

| Enum | Client name | Faction |
|---|---|---|
| NULL |  |  |
| SAGE_MK_1 | Sage Mark I | Precursor |
| SAGE_MK_2 | Sage Mark II | Precursor |
| SAGE_MK_3 | Sage Mark III | Precursor |
| SAGE_MK_4 | Sage Mark IV | Precursor |
| TOIL_MK_1 | Toil Mark I | Het |
| TOIL_MK_2 | Toil Mark II | Het |
| TOIL_MK_3 | Toil Mark III | Het |
| TOIL_MK_4 | Toil Mark IV | Het |
| HAVOK_MK_1 | Havok Mark I | Pirate |
| HAVOK_MK_2 | Havok Mark II | Pirate |
| HAVOK_MK_3 | Havok Mark III | Pirate |
| HAVOK_MK_4 | Havok Mark IV | Pirate |
| CABAL_MK_1 | Cabal Mark I | Human |
| CABAL_MK_2 | Cabal Mark II | Human |
| CABAL_MK_3 | Cabal Mark III | Human |
| CABAL_MK_4 | Cabal Mark IV | Human |
| AGENT_MK_1 | Agent Mark I | Precursor |
| AGENT_MK_2 | Agent Mark II | Precursor |
| AGENT_MK_3 | Agent Mark III | Precursor |
| AGENT_MK_4 | Agent Mark IV | Precursor |
| ICE_MK_1 | Ice Mark I | Wyrd |
| ICE_MK_2 | Ice Mark II | Wyrd |
| ICE_MK_3 | Ice Mark III | Wyrd |
| ICE_MK_4 | Ice Mark IV | Wyrd |
| WARRIOR_MK_1 | Warrior Mark I | Wyrd |
| WARRIOR_MK_2 | Warrior Mark II | Wyrd |
| WARRIOR_MK_3 | Warrior Mark III | Wyrd |
| WARRIOR_MK_4 | Warrior Mark IV | Wyrd |
| A1_SAGE | Sage Tech I | Precursor |
| A1_TOIL | Toil Tech I | Het |
| A1_HAVOK | Havok Tech I | Pirate |
| A1_CABAL | Cabal Tech I | Human |
| A1_AGENT | Agent Tech I | Precursor |
| A1_ICE | Ice Tech I | Wyrd |
| A1_WARRIOR | Warrior Tech I | Wyrd |
| A2_SAGE | Sage Tech II | Precursor |
| A2_TOIL | Toil Tech II | Het |
| A2_HAVOK | Havok Tech II | Pirate |
| A2_CABAL | Cabal Tech II | Human |
| A2_AGENT | Agent Tech II | Precursor |
| A2_ICE | Ice Tech II | Wyrd |
| A2_WARRIOR | Warrior Tech II | Wyrd |
| A3_SAGE | Sage Tech III | Precursor |
| A3_TOIL | Toil Tech III | Het |
| A3_HAVOK | Havok Tech III | Pirate |
| A3_CABAL | Cabal Tech III | Human |
| A3_AGENT | Agent Tech III | Precursor |
| A3_ICE | Ice Tech III | Wyrd |
| A3_WARRIOR | Warrior Tech III | Wyrd |
| VICTOR_MK_1 | Victor Mark I | Human |
| A1_VICTOR | Victor Tech I | Human |
| A2_VICTOR | Victor Tech II | Human |
| A3_VICTOR | Victor Tech III | Human |

Client category families for computers are Sage, Toil, Havok, Cabal, Agent, Ice, Warrior, and Victor. Tech I/II/III variants report `GetTechLevel()` 1/2/3; Mark variants report 0. Client craft categories are emitted only for non-tech, non-Victor families, such as `Sage Computers`.

## Drone classes

| Enum | Client name | Faction |
|---|---|---|
| NULL |  |  |
| LCD_V1 | LCD-V1 | Pirate |
| LCD_V2 | LCD-V2 | Pirate |
| LCD_V3 | LCD-V3 | Pirate |
| LCD_V4 | LCD-V4 | Pirate |
| LCD_V5 | LCD-V5 | Pirate |
| LCD_V6 | LCD-V6 | Pirate |
| LCD_V7 | LCD-V7 | Pirate |
| LCD_V8 | LCD-V8 | Pirate |
| LCD_V9 | LCD-V9 | Pirate |
| LCD_V10 | LCD-V10 | Pirate |
| LCD_V11 | LCD-V11 | Pirate |
| LCD_V12 | LCD-V12 | Pirate |
| HX_V1 | HX-V1 | Het |
| HX_V2 | HX-V2 | Het |
| HX_V3 | HX-V3 | Het |
| HX_V4 | HX-V4 | Het |
| HX_V5 | HX-V5 | Het |
| HX_V6 | HX-V6 | Het |
| HX_V7 | HX-V7 | Het |
| HX_V8 | HX-V8 | Het |
| HX_V9 | HX-V9 | Het |
| HX_V10 | HX-V10 | Het |
| HX_V11 | HX-V11 | Het |
| HX_V12 | HX-V12 | Het |
| WP_V1 | WP-V1 | Wyrd |
| WP_V2 | WP-V2 | Wyrd |
| WP_V3 | WP-V3 | Wyrd |
| WP_V4 | WP-V4 | Wyrd |
| WP_V5 | WP-V5 | Wyrd |
| WP_V6 | WP-V6 | Wyrd |
| WP_V7 | WP-V7 | Wyrd |
| WP_V8 | WP-V8 | Wyrd |
| WP_V9 | WP-V9 | Wyrd |
| WP_V10 | WP-V10 | Wyrd |
| WP_V11 | WP-V11 | Wyrd |
| WP_V12 | WP-V12 | Wyrd |
| DCD_V1 | DCD-V1 | Precursor |
| DCD_V2 | DCD-V2 | Precursor |
| DCD_V3 | DCD-V3 | Precursor |
| DCD_V4 | DCD-V4 | Precursor |
| DCD_V5 | DCD-V5 | Precursor |
| DCD_V6 | DCD-V6 | Precursor |
| DCD_V7 | DCD-V7 | Precursor |
| DCD_V8 | DCD-V8 | Precursor |
| DCD_V9 | DCD-V9 | Precursor |
| DCD_V10 | DCD-V10 | Precursor |
| DCD_V11 | DCD-V11 | Precursor |
| DCD_V12 | DCD-V12 | Precursor |
| BAS_V1 | BAS-V1 | Human |
| BAS_V2 | BAS-V2 | Human |
| BAS_V3 | BAS-V3 | Human |
| BAS_V4 | BAS-V4 | Human |
| BAS_V5 | BAS-V5 | Human |
| BAS_V6 | BAS-V6 | Human |
| BAS_V7 | BAS-V7 | Human |
| BAS_V8 | BAS-V8 | Human |
| BAS_V9 | BAS-V9 | Human |
| BAS_V10 | BAS-V10 | Human |
| BAS_V11 | BAS-V11 | Human |
| BAS_V12 | BAS-V12 | Human |

Drone categories are `Harvest`, `Repair`, and `Fighter`. Client craft categories combine faction and category, such as `Pirate Fighter Drones`.

## Engine classes

| Enum | Client name | Faction |
|---|---|---|
| NULL |  |  |
| Gravity | Gravity Drive | Precursor |
| Skip | Skip Drive | Human |
| Impulse | Impulse Drive | Wyrd |
| Fusion | Fusion Drive | Het |
| Atomic | Atomic Drive | Pirate |
| Crux | Crux Drive | Het |
| Stealth | Stealth Drive | Wyrd |
| Neutron | Neutron Drive | Human |

## Shield classes

| Enum | Client name | Faction |
|---|---|---|
| NULL |  |  |
| A_V01 | Shield-PCSR01 | Precursor |
| A_V02 | Shield-PCSR02 | Precursor |
| A_V03 | Shield-PCSR03 | Precursor |
| A_V04 | Shield-PCSR04 | Precursor |
| A_V05 | Shield-PCSR05 | Precursor |
| A_V06 | Shield-PCSR06 | Precursor |
| A_V07 | Shield-PCSR07 | Precursor |
| A_V08 | Shield-PCSR08 | Precursor |
| A_V09 | Shield-PCSR09 | Precursor |
| A_V10 | Shield-PCSR10 | Precursor |
| A_V11 | Shield-PCSR11 | Precursor |
| A_V12 | Shield-PCSR12 | Precursor |
| B_V01 | Shield-WYR01 | Wyrd |
| B_V02 | Shield-WYR02 | Wyrd |
| B_V03 | Shield-WYR03 | Wyrd |
| B_V04 | Shield-WYR04 | Wyrd |
| B_V05 | Shield-WYR05 | Wyrd |
| B_V06 | Shield-WYR06 | Wyrd |
| B_V07 | Shield-WYR07 | Wyrd |
| B_V08 | Shield-WYR08 | Wyrd |
| B_V09 | Shield-WYR09 | Wyrd |
| B_V10 | Shield-WYR10 | Wyrd |
| B_V11 | Shield-WYR11 | Wyrd |
| B_V12 | Shield-WYR12 | Wyrd |
| C_V01 | Shield-HET01 | Het |
| C_V02 | Shield-HET02 | Het |
| C_V03 | Shield-HET03 | Het |
| C_V04 | Shield-HET04 | Het |
| C_V05 | Shield-HET05 | Het |
| C_V06 | Shield-HET06 | Het |
| C_V07 | Shield-HET07 | Het |
| C_V08 | Shield-HET08 | Het |
| C_V09 | Shield-HET09 | Het |
| C_V10 | Shield-HET10 | Het |
| C_V11 | Shield-HET11 | Het |
| C_V12 | Shield-HET12 | Het |
| D_V01 | Shield-PRT01 | Pirate |
| D_V02 | Shield-PRT02 | Pirate |
| D_V03 | Shield-PRT03 | Pirate |
| D_V04 | Shield-PRT04 | Pirate |
| D_V05 | Shield-PRT05 | Pirate |
| D_V06 | Shield-PRT06 | Pirate |
| D_V07 | Shield-PRT07 | Pirate |
| D_V08 | Shield-PRT08 | Pirate |
| D_V09 | Shield-PRT09 | Pirate |
| D_V10 | Shield-PRT10 | Pirate |
| D_V11 | Shield-PRT11 | Pirate |
| D_V12 | Shield-PRT12 | Pirate |
| E_V01 | Shield-HUM01 | Human |
| E_V02 | Shield-HUM02 | Human |
| E_V03 | Shield-HUM03 | Human |
| E_V04 | Shield-HUM04 | Human |
| E_V05 | Shield-HUM05 | Human |
| E_V06 | Shield-HUM06 | Human |
| E_V07 | Shield-HUM07 | Human |
| E_V08 | Shield-HUM08 | Human |
| E_V09 | Shield-HUM09 | Human |
| E_V10 | Shield-HUM10 | Human |
| E_V11 | Shield-HUM11 | Human |
| E_V12 | Shield-HUM12 | Human |

## Special classes

| Enum | Client name | Faction |
|---|---|---|
| NULL |  |  |
| Technician | Technician | Het |
| Prospector | Prospector | Human |
| Tank | Tank | Het |
| Scout | Scout | Human |
| Hacker | Hacker | Human |
| Stalker | Stalker | Precursor |
| NovaDevice | Nova Device | Precursor |
| BattleRam | Battle Ram | Pirate |
| AlienHunter | Alien Hunter | Human |
| BountyHunter | Bounty Hunter | Pirate |
| Deflector | Deflector | Het |
| WeirdAlienArtifact | Weird Alien Artifact | Precursor |
| GrapplingHook | Grappling Hook | Pirate |
| Vampire | Vampire | Het |
| AdvConstruct | Advanced Construct | Wyrd |
| AdvShields | Advanced Shields | Wyrd |
| AdvElectronics | Advanced Electronics | Wyrd |
| AdvMunitions | Advanced Munitions | Wyrd |
| AdvPropulsion | Advanced Propulsion | Wyrd |
| AlienTechnology | Alien Technology | Precursor |
| DroneMaster | Drone Master | Pirate |

Client craft category for specials is `Specialist Items` for every non-null special except Weird Alien Artifact. Weird Alien Artifact has no craft category in the client helper.

## Consumable classes

Sources: `Assembly-CSharp\PIBAEAKHECA.cs`, `Assembly-CSharp\NLLPDCFPKJM.cs`, `Assembly-CSharp\OMPIMDNGMHG.cs`.

Consumables are metadata-driven. The enum class identifies the broad item type, while `Metadata` and sometimes rarity identify the exact portrait, ship mod, blueprint, title, faction relic, stat modification, kit target, party box, or CPU upgrade.

| Enum | Client display group | Craft category | Notes |
|---|---|---|---|
| Portrait | Portrait | none | Metadata stores portrait identity. |
| ShipModification | Ship Mod or Ship Skin | none | Retro skins display as Ship Skin. |
| ItemBlueprint | Blueprint | none | Metadata packs item family, class/category bytes, and build count. |
| Title | Title | none | Metadata stores title identity. |
| CrewPile100/500/1000/5000 | Resource | Crafting Resources | Resource pile. |
| OrganicPile100/500/1000/5000 | Resource | Crafting Resources | Resource pile. |
| GasPile100/500/1000/5000 | Resource | Crafting Resources | Resource pile. |
| MetalPile100/500/1000/5000 | Resource | Crafting Resources | Resource pile. |
| RadioactivePile100/500/1000/5000 | Resource | Crafting Resources | Resource pile. |
| DarkmatterPile100/500/1000/5000 | Resource | Crafting Resources | Resource pile. |
| SkullPile10/100/500/1000 | Skull | Crafting Resources | Currency pile; client currency type is Skulls. |
| RelicPile1/5/10/50/100 | Relic | none | Metadata selects Human, Wyrd, Het, or Precursor relic. |
| StatModification | Stat Mod | none | Metadata packs target stat and value. |
| QualityRepairKit | Kit | Consumable Kits | Minor/Major/Ultimate names are rarity/metadata based. |
| NanobotChargeKit | Kit | Consumable Kits | Metadata is the duration in hours. |
| OblivionFragment | Fragment | none | Metadata selects fragment faction/type. |
| OblivionFragment5 | Fragment | none | Five fragments; metadata selects faction/type. |
| OblivionFragment10 | Fragment | none | Ten fragments; metadata selects faction/type. |
| MutateItemKit | Kit | Consumable Kits | Metadata 0 is any item; otherwise metadata names an item family. |
| ReMutateItemKit | Kit | none | Re-rolls mutated item bonus. |
| PartyBox | Party | none | Metadata selects party box contents/description helper. |
| TechComputerUpgradeKit | Kit | none | Metadata encodes computer category and target tech level. |
| VoidItemKit | Kit | Consumable Kits | Applies a void bonus to a non-special item. |
| ReVoidItemKit | Kit | none | Re-rolls void bonus. |

Pile counts exposed by the client are resources `100`, `500`, `1000`, `5000`; skulls `10`, `100`, `500`, `1000`; and relics `1`, `5`, `10`, `50`, `100`.

## Storage classes

| Enum | Client name | Faction |
|---|---|---|
| NULL |  |  |
| HumanHold | HUMA-Hold | Human |
| HumanVault | HUMA-Vault | Human |
| HumanArsenal | HUMA-Arsenal | Human |
| HumanArchive | HUMA-Archive | Human |
| HumanArmory | HUMA-Armory | Human |
| HumanMunitions | HUMA-Munitions | Human |
| PirateHold | PIRA-Hold | Pirate |
| PirateVault | PIRA-Vault | Pirate |
| PirateArsenal | PIRA-Arsenal | Pirate |
| PirateArchive | PIRA-Archive | Pirate |
| PirateArmory | PIRA-Armory | Pirate |
| PirateMunitions | PIRA-Munitions | Pirate |
| HetHold | HET-Hold | Het |
| HetVault | HET-Vault | Het |
| HetArsenal | HET-Arsenal | Het |
| HetArchive | HET-Archive | Het |
| HetArmory | HET-Armory | Het |
| HetMunitions | HET-Munitions | Het |
| WyrdHold | WYRD-Hold | Wyrd |
| WyrdVault | WYRD-Vault | Wyrd |
| WyrdArsenal | WYRD-Arsenal | Wyrd |
| WyrdArchive | WYRD-Archive | Wyrd |
| WyrdArmory | WYRD-Armory | Wyrd |
| WyrdMunitions | WYRD-Munitions | Wyrd |
| PrecursorHold | PREC-Hold | Precursor |
| PrecursorVault | PREC-Vault | Precursor |
| PrecursorArsenal | PREC-Arsenal | Precursor |
| PrecursorArchive | PREC-Archive | Precursor |
| PrecursorArmory | PREC-Armory | Precursor |
| PrecursorMunitions | PREC-Munitions | Precursor |
