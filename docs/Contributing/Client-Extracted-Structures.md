# Client Extracted Structures

Source: `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled`, current Steam client decompile supplied by Goot.

This page stages structure and defense-unit facts pulled from the client. Keep these as contributor/source notes until reviewed for public pages.

## Entity Types

Source enum: `Assembly-CSharp\EPGIECDJPJC.cs`.

Entity type enum values:

- `NULL`
- `Artifact`
- `Planet`
- `Garrison`
- `Outpost`
- `Shipyard`
- `Ship`
- `Asteroid`
- `CargoMoney`
- `CargoItem`
- `CargoResource`

`DFHOJHHBAMJ.IsDefenseUnit()` returns true for `Planet`, `Garrison`, `Outpost`, and `Shipyard`.

Runtime class mapping from `DFHOJHHBAMJ.Create(...)`:

| Entity type | Runtime class |
|---|---|
| Artifact | `KHEBEGGPJKL` |
| Planet | `MJDGACFOCNF` |
| Garrison | `MJPCPHDMFHC` |
| Outpost | `ADLMFIMMBCD` |
| Shipyard | `IEDAMJFHMMG` |
| Ship | `CHCIGDNAAPI` |
| Asteroid | `MBGGNGIAACH` |
| CargoMoney | `BLGMBFBBDHK` |
| CargoItem | `MNGDHFFMGBM` |
| CargoResource | `NFPLLCBJOEG` |

## Defense DB Fields

Sources:

- `Assembly-CSharp\TibSharp\Expansion\Library\Database\DefenseEntityDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\PlanetDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\GarrisonDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\OutpostDbObj.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\ShipyardDbObj.cs`

Shared `DefenseEntityDbObj` fields:

| Field | Meaning inferred from population/use |
|---|---|
| `CorpId` | owning corp id |
| `SpecialAccess` | special access rank, default `Commander` |
| `GearAccess` | gear access rank, default `Commander` |
| `CreationIndex` | creation order/index |
| `Affinity` | defense affinity/faction override |
| `ImmunityMinutes` | immunity duration; nonzero means immunity is active |

Specific DB fields:

| DB class | Extra fields |
|---|---|
| `PlanetDbObj` | `Class` |
| `GarrisonDbObj` | `HadCapturedShrine` |
| `OutpostDbObj` | none found beyond shared defense fields |
| `ShipyardDbObj` | none found beyond shared defense fields |

`GarrisonDbObj.ClearLocationData()` clears location data and sets `HadCapturedShrine = false`.

## Corp Defense Caps

Sources:

- `Assembly-CSharp\GNIBJABBHJK.cs`
- `Assembly-CSharp\EAIACLBINPG.cs`
- `Assembly-CSharp\OGCPCJCNIKK.cs`
- `Assembly-CSharp\OBCIICJBFNN.cs`
- `Assembly-CSharp\PGJIDFCBFCC.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\CombatEntityDbObj.cs`

Corp defense collections:

| Corp field | Runtime collection | Defense type | Default max |
|---|---|---|---:|
| `OCNGKPHMNJK` | `EAIACLBINPG` | Garrisons | 4 |
| `LKKCABJOHPK` | `OGCPCJCNIKK` | Outposts | 8 |
| `LPFOCHEMKEL` | `OBCIICJBFNN` | Shipyards | 4 |

The collection full check is `current count >= max`.

## Build Cap Tech Point Costs

Source: `Assembly-CSharp\JEKJDKMBIGN.cs`, `GetCorpBuildDefenseCost(...)` and `GetCorpBuildDefenseCostBase(...)`.

Default base cost constants from `PGJIDFCBFCC.cs`:

| Defense type | Default base cost |
|---|---:|
| Garrison | 6000 |
| Outpost | 6000 |
| Shipyard | 6000 |

Cost by current count:

| Defense type | Current count | Cost |
|---|---:|---:|
| Garrison | 0-1 | base / 3 |
| Garrison | 2 | base / 2 |
| Garrison | 3+ | base |
| Outpost | 0-1 | base / 6 |
| Outpost | 2 | base / 5 |
| Outpost | 3 | base / 4 |
| Outpost | 4 | base / 3 |
| Outpost | 5 | base / 2 |
| Outpost | 6+ | base |
| Shipyard | 0-1 | base / 3 |
| Shipyard | 2 | base / 2 |
| Shipyard | 3+ | base |

With the default base of 6000, this gives:

| Defense type | Current count | Default cost |
|---|---:|---:|
| Garrison | 0-1 | 2000 |
| Garrison | 2 | 3000 |
| Garrison | 3+ | 6000 |
| Outpost | 0-1 | 1000 |
| Outpost | 2 | 1200 |
| Outpost | 3 | 1500 |
| Outpost | 4 | 2000 |
| Outpost | 5 | 3000 |
| Outpost | 6+ | 6000 |
| Shipyard | 0-1 | 2000 |
| Shipyard | 2 | 3000 |
| Shipyard | 3+ | 6000 |

Client-side validation in `IKOLEGFOADL.CanIncreaseCorpDefenseCap(...)`:

- Player must be in a corporation.
- Contribution must be at least 1 Tech Point.
- Corp-bank spending requires commander/leader permissions.
- Personal spending requires enough personal Tech Points.
- Only `Garrison`, `Outpost`, and `Shipyard` are valid for this cap increase helper.
- The target collection must not already be at max.

## Base Equip Points And Slots

Sources:

- `Assembly-CSharp\IGDDJEMDJEJ.cs`
- `Assembly-CSharp\TibSharp\Expansion\Library\Database\CombatEntityDbObj.cs`
- `Assembly-CSharp\EntityInspectPanel.cs`

Defense base EP:

```text
Planet   = (Hardcore ? 40 : 30) + floor(level / 10) + EliteRank * 5
Garrison = (Hardcore ? 30 : 20) + floor(level / 10) + EliteRank * 4
Outpost  = (Hardcore ? 25 : 15) + floor(level / 10) + EliteRank * 3
Shipyard = (Hardcore ? 25 : 15) + floor(level / 10) + EliteRank * 3
```

The client boolean previously called `IIBHNOLJCPL` is populated from `CombatEntityDbObj.Hardcore`. The rank value is populated from `CombatEntityDbObj.EliteRank`; `EntityInspectPanel` displays it as up to five elite-rank stars.

The defense name builder appends:

- affinity suffixes: `-WYR`, `-PIR`, `-HET`, `-PRC`
- `-HC` when `Hardcore` is true
- an elite-rank suffix when `EliteRank > 0` and the entity is not in the client-owned/default branch

Base weapon slots by level:

| Level | Weapon slots |
|---:|---:|
| `< 3` | 1 |
| `3-8` | 2 |
| `9-14` | 3 |
| `15-32` | 4 |
| `33-76` | 5 |
| `77+` | 6 |

Base drone slots by level:

| Level | Drone slots |
|---:|---:|
| `< 5` | 1 |
| `5-10` | 2 |
| `11-26` | 3 |
| `27-53` | 4 |
| `54-87` | 5 |
| `88+` | 6 |

Base battery slots by level:

| Level | Battery slots |
|---:|---:|
| `< 2` | 1 |
| `2-6` | 2 |
| `7-12` | 3 |
| `13-45` | 4 |
| `46-98` | 5 |
| `99+` | 6 |

## Stat And Action Rules

Sources:

- `Assembly-CSharp\IGDDJEMDJEJ.cs`
- `Assembly-CSharp\AHFAPFNMNPJ.cs`

Defense entities report `IMPOOFFJGKG = true`; in the shared stat container this means aux/full-slot scaling differs from player ships. The existing ship extraction notes show structure/NPC-like entities using full aux scaling rather than the player ship 10% aux rule.

Stats ignored by defense:

- `ResourceCapacity`
- `Harvest`
- `XpBonus`
- `EvasionChance`
- `HackResist`
- `GrappleResist`
- `SplashResist`
- `CriticalResist`
- `TargetingSpeedPercent`

`CanTargetDefense(...)` returns true only for the `Repair` action.

`GetInterdictorRank(...)` returns `Interdictor4` only for a deployed planet. Other defense types return `NULL`.

## Default Defense Techs

Source: `Assembly-CSharp\IGDDJEMDJEJ.cs`, `GetHasTechDefault(...)`.

Repair facility defaults:

| Tech | Default defense type |
|---|---|
| `RepairFacility1` | Outpost |
| `RepairFacility2` | Garrison |
| `RepairFacility3` | Planet |
| `RepairFacility4` | Shipyard |

Rank-based defaults:

| Tech | Default condition |
|---|---|
| `Intimidation1` | defense rank `<= 1` |
| `Intimidation2` | defense rank `2-3` |
| `Intimidation3` | defense rank `>= 4` |
| `Vanquisher` | defense rank `>= 5` |

Vision defaults:

- `LongRangeVision` and the next enum value, `PassiveScan1`, return true for Planet, Garrison, and Outpost.
- Shipyard is not included in that helper branch.

Faction affinity defaults:

| Affinity | Default techs |
|---|---|
| Wyrd | `ShieldCapacitors1` rank `<= 1`; `ShieldCapacitors2` rank `2-3`; `ShieldCapacitors3` rank `>= 4`; `AdvancedHacking1` rank `1-2`; `AdvancedHacking2` rank `>= 3` |
| Pirate | `AdvancedAlloys1` rank `1-2`; `AdvancedAlloys2` rank `>= 3`; `AttackDrones1` rank `<= 1`; `AttackDrones2` rank `2-3`; `AttackDrones3` rank `>= 4` |
| Het | `ShieldPierce1` rank `<= 1`; `ShieldPierce2` rank `2-3`; `ShieldPierce3` rank `>= 4`; `Technician1` rank `1-2`; `Technician2` rank `>= 3` |
| Precursor | `ShieldAmplifier1` rank `<= 1`; `ShieldAmplifier2` rank `2-3`; `ShieldAmplifier3` rank `>= 4`; `AdvancedDraining1` rank `1-2`; `AdvancedDraining2` rank `>= 3` |

## Resource Defense XP

Sources:

- `Assembly-CSharp\AHFAPFNMNPJ.cs`, `GetDefenseXp(...)`
- `Assembly-CSharp\EntityInspectPanel.cs`
- `Assembly-CSharp\JEKJDKMBIGN.cs`
- `Assembly-CSharp\PGJIDFCBFCC.cs`

```text
defense XP = resource value modifier * resource amount * defense XP multiplier
```

Default defense XP multiplier from `PGJIDFCBFCC.cs` is `1`. The accessor doubles it when `KMOBGNPOEEM.EHBGICPOKDA` is true; public meaning of that flag needs confirmation.

Defense units also have a daily XP absorption cap:

```text
daily defense XP cap = MFHFINEHCHK
```

Default `MFHFINEHCHK` is `15000`. The accessor doubles it when `KMOBGNPOEEM.EHBGICPOKDA` is true. The UI labels this as remaining daily XP and blocks donations once the unit has reached the cap until the next boost/reset time.

Resource value modifiers:

| Resource | Modifier |
|---|---:|
| Crew | 0.1 |
| Organic | 1 |
| Gas | 1.25 |
| Metal | 1.5 |
| Radioactive | 1.75 |
| Darkmatter | 2 |

## Quick Jump Rules

Source: `Assembly-CSharp\IGDDJEMDJEJ.cs`, `CanQuickJump(...)`.

The client rejects quick jump when:

- the ship/player or defense has no deployment/map context,
- the origin is inside the arena,
- the origin ship is destroyed,
- the defense is hostile and not Human-owned in the normal branch,
- the target defense is not a Planet or Garrison in branches that require those types,
- a Human-territory Garrison is not a jump gate,
- a non-Human map/faction condition is below R9 in the Human-territory Garrison branch,
- the player has already reached the relevant map/sector condition.

Positive branches include:

- the defense is an active Human defense in the early client check,
- the defense belongs to the player's corp,
- the defense belongs to the player's alliance,
- special map states allow Planet or Garrison,
- normal Human-territory branch allows Planet and qualifying Garrison.

This needs gameplay review before becoming public guidance because several conditions are obfuscated map/sector flags.

## Structure Multipliers

The shared stat-container extraction in `Client-Extracted-Ships.md` already stages the hull/shield multipliers:

| Entity type | Hull/shield multiplier | Base hull term |
|---|---:|---:|
| Planet | 40 | 10000 |
| Garrison | 30 | 10000 |
| Outpost | 12 | 10000 |
| Shipyard | 12 | 10000 |
| Ship/default | 1 | 1400 |

Keep structure stat formulas linked to the canonical extracted structures/ships notes instead of repeating them in strategy pages.
