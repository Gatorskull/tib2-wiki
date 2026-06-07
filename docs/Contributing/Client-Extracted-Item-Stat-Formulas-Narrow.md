# Client-Extracted Narrow Item Stat Formulas

Hidden contributor staging page. This captures raw client formula bodies for the narrower item stat families: shields, engines, and batteries. This is closer to source than wiki copy; formulas still need translation before public pages.

Notes:

- `base.PPAFMKOLBBL` is the item rarity enum in runtime item classes.
- `base.EDPOPGPNMCD` is a shared item value/stat multiplier used throughout runtime item formulas.
- `DNONFFBHEEM.Class` is the item class enum; `DNONFFBHEEM.Ep` is the data-fed rank/base EP value for item families that use it.
- Obfuscated switch cases and suspicious constants should be verified before public use.
- In formulas below, `rarity` means the numeric value of `AHKIAECFDDB.R#`, `q` means the cached item quality multiplier, and `epCost` means the runtime item EquipPointCost unless noted otherwise.

## Helper dependencies to translate next

The raw formulas below call these helper methods:

| Helper | Why it matters |
|---|---|
| `GetEpCostMod()` | Shield EP cost faction modifier. Already summarized in `Client-Extraction-Notes.md`. |
| `GetFaction()` | Converts item class to faction, usually for faction-specific EP/stat behavior. |
| `GetMod()` | Converts AI/balance modifier enum to a multiplier. |
| `GetModelNumber()` | Used by shields to choose which shield models grant specific stats. |
| `InternalGetResistMod()` | Shared shield resist amount used by several shield stats. |
| `InternalGetShieldCapacity()` | Shared shield-capacity base used by shield capacity formulas. |

## Translated helpers

These helpers are stable enough to use while translating the raw formulas below. Keep them on contributor pages until the dependent stat formulas have been sanity-checked against live item displays.

### Balance modifier

Source: `Assembly-CSharp\OMPIMDNGMHG.cs`, `GetMod(this CCGPFAFAKIG)`.

The generic balance modifier enum maps to:

| Modifier | Multiplier |
|---|---:|
| Default/unknown | `1.0` |
| MIN | `1 - (NILGPMKLJEF * 0.1)` |
| LOW | `1 - (NILGPMKLJEF * 0.2)` |
| MID | `1 - (NILGPMKLJEF * 0.4)` |
| HIGH | `1 - (NILGPMKLJEF * 0.6)` |
| MAX | `1 - NILGPMKLJEF` |

Client default: `NILGPMKLJEF = 0.75`, so the default multipliers are MIN `0.925`, LOW `0.85`, MID `0.70`, HIGH `0.55`, MAX `0.25`.

### Shield helpers

Source: `Assembly-CSharp\BNCBECFCPHP.cs` and `Assembly-CSharp\OMPIMDNGMHG.cs`.

Shield class letters map to factions:

| Shield class prefix | Faction |
|---|---|
| `A_V##` | Precursor |
| `B_V##` | Wyrd |
| `C_V##` | Het |
| `D_V##` | Pirate |
| `E_V##` | Human |

Shield model number is just the numeric suffix: `*_V01` -> model `1`, through `*_V12` -> model `12`.

Base shield capacity before model/stat multipliers:

| Shield class prefix | Formula |
|---|---|
| `A_V##` / Precursor | `315 * item EP/rank value * item value multiplier` |
| `B_V##` / Wyrd | `290 * item EP/rank value * item value multiplier` |
| `C_V##` / Het | `265 * item EP/rank value * item value multiplier` |
| `D_V##` / Pirate | `240 * item EP/rank value * item value multiplier` |
| `E_V##` / Human/default | `215 * item EP/rank value * item value multiplier` |

Shared shield resist amount:

| Faction | Formula |
|---|---|
| Human/default | `rarity * 0.8 * item value multiplier` |
| Pirate | `rarity * 0.7 * item value multiplier` |
| Het | `rarity * 0.6 * item value multiplier` |
| Wyrd | `rarity * 0.5 * item value multiplier` |
| Precursor | `rarity * 0.4 * item value multiplier` |

Shield EP cost faction modifier:

| Faction | Modifier |
|---|---:|
| Human/default | `0` |
| Pirate | `1` |
| Het | `2` |
| Wyrd | `3` |
| Precursor | `4` |

### Engine and battery class factions

Source: `Assembly-CSharp\OMPIMDNGMHG.cs`.

Engine factions:

| Engine | Faction |
|---|---|
| Gravity Drive | Precursor |
| Skip Drive | Human |
| Impulse Drive | Wyrd |
| Fusion Drive | Het |
| Atomic Drive | Pirate |
| Crux Drive | Het |
| Stealth Drive | Wyrd |
| Neutron Drive | Human |

Battery factions:

| Battery | Faction |
|---|---|
| Alkaic Battery | Pirate |
| Chromic Battery | Pirate |
| Galvanic Battery | Pirate |
| Mercuric Battery | Human |
| Lithic Battery | Human |
| Voltaic Battery | Het |
| Hydric Battery | Het |
| Zambic Battery | Wyrd |
| Silic Battery | Wyrd |
| Moltic Battery | Precursor |
| Polyanic Battery | Precursor |
| Radionic Battery | Precursor |

### Battery power aggregation

Source: `Assembly-CSharp\GKFECKLMHGM.cs`, `GetPowerCapacity()` and `GetPowerRechargeRate()`.

Client defaults from `PGJIDFCBFCC.cs`:

| Constant | Default | Meaning seen in client |
|---|---:|---|
| `OEIKMFLMGEP` | `17` | Base power capacity |
| `EOJADIDEHDH` | `1.5` | Base power recharge per second |
| `EMDOMLHMHOD` | `10` | Minimum hack/grapple/drain power required to use those actions |

Power capacity aggregation:

```text
capacity = base capacity
  + full-slot item PowerCapacity
  + aux-slot item PowerCapacity * aux multiplier
  + eligible battery capacity bonuses
```

Battery capacity bonuses apply when the ship is Pirate or when the ship faction matches the battery faction. If the final value is above base capacity, the client multiplies it by `DDFFLFKNGLL`; otherwise it returns the base capacity. The meaning/default of `DDFFLFKNGLL` still needs a named-constant pass.

Power recharge aggregation:

```text
recharge = base recharge
  + full-slot item PowerRecharge
  + aux-slot item PowerRecharge * aux multiplier
  + skill bonus to PowerRecharge
```

If `OPFKNEPIMCB` is set on the ship/player object, recharge gains `+0.05`. If final recharge is above base recharge, the client multiplies it by `NOJILIOCBMF`; otherwise it returns base recharge. The meaning/default of `NOJILIOCBMF` still needs a named-constant pass.

## Armor

Source: `Assembly-CSharp\KKKEBKMMOBA.cs` and armor enum/faction helpers in `Assembly-CSharp\OMPIMDNGMHG.cs`.

### Armor classes and factions

| Armor class | Faction |
|---|---|
| Titanium | Human |
| Composite | Pirate |
| Carbide | Human |
| Exoprene | Het |
| Cytoplast | Het |
| Holocrine | Het |
| Diamond | Wyrd |
| Thorium | Pirate |
| Osmium | Wyrd |
| Citadel | Precursor |
| Ajax | Precursor |
| Aegis | Precursor |
| Kismet | Precursor |

### Shared armor formulas

Armor EP cost:

```text
epCost = max(0, item EP/rank - rarity + 1)
```

Shared armor max hull base:

```text
armorHullBase = (240 + rarity * 10) * armorHullClassFactor * q * item EP/rank
```

`armorHullClassFactor` is `0.25` for Titanium, Exoprene, Diamond, Thorium, Aegis, and Kismet; otherwise it is `1.0`.

Armor `MaxHull`:

```text
MaxHull = armorHullBase * balanceMod
```

Armor `MoveSpeedPercent` is derived from `armorHullBase` but divides quality back out:

| Rarity | Divisor |
|---|---:|
| R1/default | 15000 |
| R2 | 15500 |
| R3 | 16000 |
| R4 | 16500 |
| R5 | 17000 |
| R6 | 17500 |
| R7 | 18000 |

```text
MoveSpeedPercent = armorHullBase / (q * rarity divisor)
```

### Armor class stat formulas

Most armor class stats use one of these two shared forms:

```text
flat = (rarity + epCost) * q
percent = (rarity * 0.01 + epCost * 0.01) * q
```

| Armor class | Stat(s) | Formula |
|---|---|---|
| Titanium | EvasionChance | `flat` |
| Composite | HackResist | `flat` |
| Carbide | XpBonus | `percent` |
| Exoprene | SplashChance, HullDamage | `SplashChance = flat`; `HullDamage = percent * 0.8` |
| Cytoplast | SplashResist | `flat` |
| Holocrine | HullRepair | `percent` |
| Diamond | HitChance, HullDamage | `HitChance = flat`; `HullDamage = percent * 0.8` |
| Thorium | ShieldPenetration, HullDamage | `ShieldPenetration = percent`; `HullDamage = percent * 0.8` |
| Osmium | GrappleResist | `flat` |
| Citadel | CriticalResist | `flat` |
| Ajax | BatteryDrainResist | `flat` |
| Aegis | TargetingSpeedPercent, HullDamage | `TargetingSpeedPercent = -percent`; `HullDamage = percent * 0.8` |
| Kismet | CriticalChance, HullDamage | `CriticalChance = flat`; `HullDamage = percent * 0.8` |

Important interpretation note: `MoveSpeedPercent` and `TargetingSpeedPercent` sign/display semantics should be checked against live item panels before public wording. The formula above records the client stat value, not player-facing advice.

## Storage

Source: `Assembly-CSharp\KJEIOMFAJOC.cs`, `Assembly-CSharp\HEPGMEMIEFG.cs`, `Assembly-CSharp\EPFDDGJHAFO.cs`, and storage helpers in `Assembly-CSharp\OMPIMDNGMHG.cs`.

Storage classes are the cross-product of five factions and six categories:

| Category | Human | Pirate | Het | Wyrd | Precursor |
|---|---|---|---|---|---|
| Hold | HUMA-Hold | PIRA-Hold | HET-Hold | WYRD-Hold | PREC-Hold |
| Vault | HUMA-Vault | PIRA-Vault | HET-Vault | WYRD-Vault | PREC-Vault |
| Arsenal | HUMA-Arsenal | PIRA-Arsenal | HET-Arsenal | WYRD-Arsenal | PREC-Arsenal |
| Archive | HUMA-Archive | PIRA-Archive | HET-Archive | WYRD-Archive | PREC-Archive |
| Armory | HUMA-Armory | PIRA-Armory | HET-Armory | WYRD-Armory | PREC-Armory |
| Munitions | HUMA-Munitions | PIRA-Munitions | HET-Munitions | WYRD-Munitions | PREC-Munitions |

### Shared storage formulas

Storage EP cost:

```text
epCost = max(0, item EP/rank - rarity + 1)
```

Storage resource capacity:

```text
ResourceCapacity = (item EP/rank + (item EP/rank + rarity) * q) / 2
```

Storage EP bonus:

| Rarity | EquipPointMax |
|---|---:|
| R1-R4 | 0 |
| R5 | 1 |
| R6 | 2 |
| R7 | 3 |

Storage penalty percent helper:

| EP cost | Penalty percent |
|---:|---:|
| 0 | 1.0 |
| 1 | 0.75 |
| 2 | 0.5 |
| 3 | 0.25 |
| 4+ | 0 |

The client uses this helper in several storage category stat tradeoffs. Treat exact tradeoff stats as needs-live-panel confirmation before public tables.

### Storage slot unlock text

Source: `KJEIOMFAJOC.IMENLMBAELG`.

If `epCost >= 4`, the client returns category-based slot text:

| Storage category | Displayed slot effect |
|---|---|
| Hold, Vault | `+1 Battery Equipment Item Slot` |
| Arsenal, Munitions | `+1 Weapon Equipment Item Slot` |
| Archive, Armory | `+1 Drone Equipment Item Slot` |

This text is client display logic. Confirm server/equip behavior before moving it to public rules.

## Computer

Sources: `Assembly-CSharp\CAHAIADFHCG.cs`, `Assembly-CSharp\KOBILLCNLAJ.cs`, `Assembly-CSharp\OMPIMDNGMHG.cs`.

Computer formulas use:

- `rarity` = numeric `AHKIAECFDDB.R#`.
- `q` = cached quality multiplier.
- `techLevel` = `GetTechLevel()`, where Mark computers return 0 and Tech I/II/III return 1/2/3.
- `category` = one of Sage, Toil, Havok, Cabal, Agent, Ice, Warrior, Victor.

Computer category and faction mapping:

| Category | Faction | Classes |
|---|---|---|
| Sage | Precursor | Sage Mark I-IV, Sage Tech I-III |
| Toil | Het | Toil Mark I-IV, Toil Tech I-III |
| Havok | Pirate | Havok Mark I-IV, Havok Tech I-III |
| Cabal | Human | Cabal Mark I-IV, Cabal Tech I-III |
| Agent | Precursor | Agent Mark I-IV, Agent Tech I-III |
| Ice | Wyrd | Ice Mark I-IV, Ice Tech I-III |
| Warrior | Wyrd | Warrior Mark I-IV, Warrior Tech I-III |
| Victor | Human | Victor Mark I, Victor Tech I-III |

Computer craft categories are only emitted for non-tech, non-Victor categories. Example: `Sage Computers`. Tech computers and Victor computers return no craft category from `GetItemCraftCategory()`.

Computer EP cost:

```csharp
protected override int OMIBOKEONLA
{
	get
	{
		return 0;
	}
}
```

Computer base credit value by tech level:

| Tech level | Base credit value |
|---|---:|
| Mark / 0 | 1800 |
| Tech I | 2400 |
| Tech II | 3000 |
| Tech III | 3600 |

Runtime credit value formula:

- R1: `baseCreditValue / 2`
- R2+: `rarity^3 * baseCreditValue`

R6/R7 technology bonuses exposed by helper methods:

| Condition | Bonus |
|---|---|
| R6 Sage category | `Scan3` |
| R7 Sage category | `Scan4` |
| R7 Toil category | `ReverseGrappling` |
| R7 Havok category | `ReverseGrappling` |
| R7 Cabal category | `ReverseBatteryDrain` |
| R7 Agent category | `ReverseHacking` |
| R7 Ice category | `ReverseHacking` |
| R7 Warrior category | `ReverseBatteryDrain` |
| R7 Victor category | none from `GetR7TechBonus()` |

Computer item technology (`ENBAENEOAFE`) only appears at R7 or higher. Non-void and void map differently:

| Category | Non-void R7 item tech | Void R7 item tech |
|---|---|---|
| Sage | `AlienDamage3` | `AlienDamage4` |
| Toil | `SpeedDrain1` | `SpeedDrain2` |
| Havok | `SpeedHack1` | `SpeedHack2` |
| Cabal | `Savior1` | `Savior2` |
| Agent | `Vorpal1` | `Vorpal2` |
| Ice | `Analysis1` | `Analysis2` |
| Warrior | `Targeting1` | `Targeting2` |
| Victor | `HyperDrive1` | `HyperDrive2` |

Computer EP max bonus:

| Class group | R1-R6 EP max | R7+ EP max |
|---|---:|---:|
| Toil Mark I-IV | 1 | 2 |
| Sage Tech I, Toil Tech I | 2 | 3 |
| Havok/Cabal/Agent/Ice/Warrior Tech I | 1 | 2 |
| Sage Tech II, Toil Tech II | 3 | 4 |
| Havok/Cabal/Agent/Ice/Warrior Tech II | 2 | 3 |
| Sage Tech III, Toil Tech III | 4 | 5 |
| Havok/Cabal/Agent/Ice/Warrior Tech III | 3 | 4 |
| Victor Mark I | 1 | 2 |
| Victor Tech I | 2 | 3 |
| Victor Tech II | 3 | 4 |
| Victor Tech III | 4 | 5 |
| Other Mark computers | 0 | 0 |

The per-stat computer formulas are present in `KOBILLCNLAJ.cs`, but several decompiled switch blocks include impossible/raw cast cases that need translation against enum order or live item-panel checks before publishing as rules. Confirm before public use.

## Special

Sources: `Assembly-CSharp\EJDCMKKAGOP.cs`, `Assembly-CSharp\KKHJOEBCGAP.cs`, `Assembly-CSharp\OMPIMDNGMHG.cs`.

Special item craft category:

- All non-null specials except Weird Alien Artifact return `Specialist Items`.
- `NULL` and Weird Alien Artifact return no craft category.

Special item EP cost:

```csharp
protected override int OMIBOKEONLA
{
	get
	{
		return 0;
	}
}
```

Special credit value:

- R1: `2175`
- R2+: `rarity^3 * 4350`

Special technology slot A (`IDHKHPPPENO` / `GetTechBonusA`):

| Special | Rarity mapping |
|---|---|
| Technician | R1-R4 `Technician1`, R5 `Technician2`, R6 `Technician3`, R7 `Technician4` |
| Prospector | `Harvesting1` through `Harvesting7` by rarity |
| Tank | `HullMax1` through `HullMax7` by rarity |
| Scout | R1-R2 `Scan1`, R3 `Scan2`, R4 `Scan3`, R5 `Scan4`, R6 `Scan5`, R7 `Scan6` |
| Hacker | R4-R5 `AdvancedHacking1`, R6 `AdvancedHacking2`, R7 `AdvancedHacking3` |
| Stalker | R1-R2 `Cloak1`, R3 `Cloak2`, R4 `Cloak3`, R5 `Cloak4`, R6 `Cloak5`, R7 `Cloak6` |
| Nova Device | `NovaDeath1` through `NovaDeath7` by rarity |
| Battle Ram | `BattleRam1` through `BattleRam7` by rarity |
| Alien Hunter | `Scavenger1` through `Scavenger7` by rarity |
| Bounty Hunter | `PvPDamage1` through `PvPDamage7` by rarity |
| Deflector | `Deflector1` through `Deflector7` by rarity |
| Weird Alien Artifact | none |
| Grappling Hook | R4-R5 `AdvancedGrappling1`, R6 `AdvancedGrappling2`, R7 `AdvancedGrappling3` |
| Vampire | R4-R5 `AdvancedDraining1`, R6 `AdvancedDraining2`, R7 `AdvancedDraining3` |
| Advanced Construct | R6 `Mechanic1`, R7 `Mechanic2` |
| Advanced Shields | `ShieldMax1` through `ShieldMax7` by rarity |
| Advanced Electronics | R5 `Scan1`, R6 `Scan2`, R7 `Scan3` |
| Advanced Munitions | R6 `Mechanic1`, R7 `Mechanic2` |
| Advanced Propulsion | R6 `Mechanic1`, R7 `Mechanic2` |
| Alien Technology | none |
| Drone Master | R1-R4 `AttackDrones1`, R5 `AttackDrones2`, R6 `AttackDrones3`, R7 `AttackDrones4` |

Special technology slot B (`ENBAENEOAFE` / `GetTechBonusB`):

| Special | Rarity mapping |
|---|---|
| Technician | R1-R5 `SpeedRepair1`, R6 `SpeedRepair2`, R7 `SpeedRepair3` |
| Tank | R7 `AdvancedAlloys1` |
| Scout | R1-R5 `SpeedScan1`, R6 `SpeedScan2`, R7 `SpeedScan3` |
| Hacker | R1-R5 `SpeedHack1`, R6 `SpeedHack2`, R7 `SpeedHack3` |
| Stalker | R1-R5 `CloakDuration1`, R6 `CloakDuration2`, R7 `CloakDuration3` |
| Nova Device | R6-R7 `NovaInversion` |
| Alien Hunter | `AlienDamage1` through `AlienDamage7` by rarity |
| Bounty Hunter | R1-R4 `PvPBonusXP1`, R5-R6 `PvPBonusXP2`, R7 `PvPBonusXP3` |
| Deflector | R7 `ShieldCapacitors1` |
| Grappling Hook | R1-R5 `SpeedGrapple1`, R6 `SpeedGrapple2`, R7 `SpeedGrapple3` |
| Vampire | R1-R5 `SpeedDrain1`, R6 `SpeedDrain2`, R7 `SpeedDrain3` |
| Advanced Shields | R7 `ShieldAmplifier1` |
| Drone Master | R1-R4 `RepairDrones1`, R5 `RepairDrones2`, R6 `RepairDrones3`, R7 `RepairDrones4` |
| Other specials | none |

Special EP max bonus:

| Special | Rarity mapping |
|---|---|
| Tank | R7 `+1` |
| Battle Ram | R1-R4 `+0`, R5 `+1`, R6 `+2`, R7 `+3` |
| Alien Hunter, Bounty Hunter, Deflector, Vampire | R1-R5 `+0`, R6 `+1`, R7 `+2` |
| Advanced Construct | R1-R5 `+2`, R6 `+3`, R7 `+4` |
| Advanced Shields, Advanced Propulsion | R1-R3 `+0`, R4-R6 `+1`, R7 `+2` |
| Advanced Electronics, Advanced Munitions | R1-R4 `+0`, R5-R6 `+1`, R7 `+2` |
| Alien Technology | R1-R6 `+1`, R7 `+2` |
| Other specials | `+0` |

Special display slot text:

| Special | Condition | Displayed slot effect |
|---|---|---|
| Alien Hunter, Bounty Hunter | R7+ | `+1 Weapon Equipment Item Slot` |
| Weird Alien Artifact | any rarity | `+1 Drone Equipment Item Slot` |
| Vampire, Alien Technology | R7+ | `+1 Battery Equipment Item Slot` |
| Drone Master | R7+ | `+1 Drone Equipment Item Slot` |

Special immunity display text:

| Special | Rarity | Displayed text |
|---|---|---|
| Hacker | R2-R7 | `Immune to Hack Ram Rank 1-6` |
| Advanced Construct | R2-R7 | `Immune to Battle Ram and Hack Ram Rank 1-6` |

The remaining direct stat formulas in `KKHJOEBCGAP.cs` are a mix of readable overrides and obfuscation-noise methods. Use this section as the stable technology/EP/slot extraction until the per-stat pass is completed.

## Drone

Sources: `Assembly-CSharp\HAOJHDJLJFO.cs`, `Assembly-CSharp\HHIKNHLFHOI.cs`, `Assembly-CSharp\BBNPEFEJEEC.cs`, `Assembly-CSharp\BFADKAEGMNI.cs`, `Assembly-CSharp\OMPIMDNGMHG.cs`, `Assembly-CSharp\PGJIDFCBFCC.cs`.

Drone categories:

| Enum | Category |
|---|---|
| `Harvest` | Harvest drone |
| `Repair` | Repair drone |
| `Fighter` | Fighter drone |

Drone class family and faction mapping:

| Prefix | Faction | Versions |
|---|---|---|
| `LCD` | Pirate | V1-V12 |
| `HX` | Het | V1-V12 |
| `WP` | Wyrd | V1-V12 |
| `DCD` | Precursor | V1-V12 |
| `BAS` | Human | V1-V12 |

Drone craft categories are faction plus category, for example `Pirate Fighter Drones`, `Het Repair Drones`, or `Precursor Harvest Drones`.

Drone EP cost:

- Category modifier: Harvest `+0`, Repair `+1`, Fighter `+2`.
- Special case: BAS-V12 Repair reduces the category-modified EP cost by 1 before faction/rarity logic.
- Special case: BAS-V6 Harvest reduces the category-modified EP cost by 1 before faction/rarity logic.
- Final `OMIBOKEONLA` clamps negative results to `0`.

Faction/rarity EP cost before final clamp:

| Faction | R1-R2 | R3-R4 | R5-R6 | R7 |
|---|---:|---:|---:|---:|
| Pirate | `1 + categoryMod` | `categoryMod` | `categoryMod - 1` | `categoryMod - 2` |
| Het | `2 + categoryMod` | `1 + categoryMod` | `categoryMod` | `categoryMod - 1` |
| Wyrd | `3 + categoryMod` | `2 + categoryMod` | `1 + categoryMod` | `categoryMod` |
| Precursor | `4 + categoryMod` | `3 + categoryMod` | `2 + categoryMod` | `1 + categoryMod` |
| Human | `categoryMod` | `categoryMod` | `categoryMod` except R6 `categoryMod - 1` | `categoryMod - 2` |

Drone base credit value:

| Faction | R1 credit value | R2+ formula |
|---|---:|---|
| Human | 900 | `rarity^3 * 1800` |
| Pirate | 1000 | `rarity^3 * 1900` |
| Het | 1100 | `rarity^3 * 2000` |
| Wyrd | 1200 | `rarity^3 * 2100` |
| Precursor | 1300 | `rarity^3 * 2200` |

Drone action timers use config defaults from `PGJIDFCBFCC`:

| Category | Base formula |
|---|---|
| Fighter | `14000ms - (rarity - R1) * 500ms` |
| Repair | `26000ms - (rarity - R1) * 1000ms` |
| Harvest | `(60000ms - (rarity - R1) * 5000ms) * factionMultiplier` |

Harvest timer faction multipliers:

| Faction | Multiplier |
|---|---:|
| Pirate | 100% |
| Het | 110% |
| Wyrd | 120% |
| Human | 130% |
| Precursor | 140% |

Harvest resource amount by faction:

| Faction | Resources per harvest action |
|---|---:|
| Human | 2 |
| Pirate | 2 |
| Het | 3 |
| Wyrd | 4 |
| Precursor | 5 |

Fighter drone damage display:

- Minimum damage uses `BFADKAEGMNI.GetDroneMinDmg(rarity, factionAttackBonusDps, 14000, q, aiBalanceMod)`.
- `GetDroneMinDmg` computes `((2 + rarity + factionAttackBonusDps) * 14000 * q)`, reduces it by one third, divides by `1000`, then applies `aiBalanceMod.GetWeaponDamageMod()`.
- Maximum displayed damage is `minDamage * 2`.
- The displayed attack interval still uses the rarity-adjusted Fighter timer above.

Fighter faction attack bonus values:

| Faction | Attack bonus DPS input |
|---|---:|
| Human | 0 |
| Pirate | 1 |
| Het | 2 |
| Wyrd | 3 |
| Precursor | 4 |

Repair drone display:

- Minimum repair uses `BFADKAEGMNI.GetDroneMinRepair(rarity, factionAttackBonusDps, 26000, q)`.
- `GetDroneMinRepair` computes `((rarity + factionAttackBonusDps) * 26000 * q)`, reduces it by one half, then divides by `1000`.
- Maximum displayed repair is `minRepair * 2`.
- The displayed repair interval still uses the rarity-adjusted Repair timer above.

Category scaling for regular stat bonuses:

- Several normal stat bonuses use a `CBNFHGOHOJH` multiplier: Fighter category `1.0`, non-Fighter categories `0.5`.
- Several resistance-style bonuses use an `NMNJHLNBOHM` multiplier: Fighter category `0.5`, non-Fighter categories `1.0`.
- Some percent bonuses use `NALIIKPGKPC`: Repair category `1.0`, non-Repair categories `0.5`.

The main drone actions above are category behavior, not ordinary item stat bonuses. This is the current-client backing for the wiki rule that an aux drone still keeps its main action at full value while its normal item stats are subject to aux scaling.

## Consumable

Sources: `Assembly-CSharp\PIBAEAKHECA.cs`, `Assembly-CSharp\NLLPDCFPKJM.cs`, `Assembly-CSharp\OMPIMDNGMHG.cs`.

Consumable runtime items are metadata-driven. `PIBAEAKHECA` is the class enum, `NLLPDCFPKJM.FLCMIIEJMPG` is the metadata field, and helpers in `OMPIMDNGMHG.cs` provide display names, descriptions, craft categories, default rarities, resource/currency types, pile counts, and tech-computer-upgrade decoding.

Consumable EP cost:

```csharp
public override int GetBaseEP()
{
	return 0;
}
```

Consumable required player level is `0` through the shared item-family required-level rule.

Consumable base credit value:

| Condition | Credit value |
|---|---:|
| Resource pile | `pileCount * resourceType.GetScrapCreditValue()` |
| Skull pile | `pileCount * 25` |
| Other consumable with `ANPJBFOPCPB == false` | `0` |
| Other consumable with `ANPJBFOPCPB == true` | `rarity * 100` |

For all named `PIBAEAKHECA` values in the current enum, `ANPJBFOPCPB` evaluates false. The `rarity * 100` branch appears to be a fallback for unknown/future consumable values beyond the current enum range. Current named non-resource, non-skull consumables therefore have base credit value `0` unless another branch handles them.

Client craft categories:

| Craft category | Consumable classes |
|---|---|
| `Crafting Resources` | Resource piles and Skull piles |
| `Consumable Kits` | QualityRepairKit, NanobotChargeKit, MutateItemKit, VoidItemKit |
| none | Portrait, ShipModification, ItemBlueprint, Title, Relic piles, StatModification, OblivionFragment variants, ReMutateItemKit, PartyBox, TechComputerUpgradeKit, ReVoidItemKit, NULL/default |

Default rarity:

| Class | Default rarity |
|---|---|
| Portrait | R3 |
| ShipModification | R7 |
| Title | R6 |
| SkullPile10 | R4 |
| SkullPile100 | R5 |
| SkullPile500 | R6 |
| SkullPile1000 | R7 |
| RelicPile1/5/10/50/100 | R7 |
| StatModification, QualityRepairKit, NanobotChargeKit, MutateItemKit, PartyBox, TechComputerUpgradeKit | R5 |
| OblivionFragment, OblivionFragment5, OblivionFragment10 | R7 |
| ReMutateItemKit, ReVoidItemKit | R6 |
| VoidItemKit | R7 |
| Any class reaching the pile-count fallback with pile count 100 | R3 |
| Any class reaching the pile-count fallback with pile count 500 | R4 |
| Any class reaching the pile-count fallback with pile count 1000 | R5 |
| Any class reaching the pile-count fallback with pile count 5000 | R7 |
| Fallback | R2 |

Pile counts:

| Family | Counts |
|---|---|
| Resource piles | `100`, `500`, `1000`, `5000` |
| Skull piles | `10`, `100`, `500`, `1000` |
| Relic piles | `1`, `5`, `10`, `50`, `100` |

Metadata encodings:

| Consumable | Metadata encoding |
|---|---|
| Portrait | `portraitFamilyByte | portraitIndexA << 8 | portraitIndexB << 16` |
| ItemBlueprint | `itemFamilyByte | class/category byte << 8 | class/category byte << 16 | buildCount << 24` |
| StatModification | `statByte | absoluteValueTimes1000 low/mid/high bytes << 8/16/24`; sign is reconstructed from whether the stat treats the value as a penalty |
| TechComputerUpgradeKit | `computerCategory + techLevel * 1000`; techLevel is 1 below 2000, 2 below 3000, and 3 at 3000+ |

Tech computer upgrade display rules:

| Decoded tech level | Client name/description meaning |
|---:|---|
| 1 | `Category Mk CPU Upgrade`; upgrades a Mark computer to Tech 1 |
| 2 | `Category Tech 1 CPU Upgrade`; upgrades Tech 1 to Tech 2 |
| 3 | `Category Tech 2 CPU Upgrade`; upgrades Tech 2 to Tech 3 |

Nanobot charge kit rarity helper:

| Duration hours | Rarity |
|---:|---|
| 1-5 | R2 |
| 6-10 | R3 |
| 11-20 | R4 |
| 21-30 | R5 |
| 31-40 | R6 |
| 41+ | R7 |

Quality repair kit public effect text from the client:

| Kit rarity/metadata | Client description |
|---|---|
| Not R6/R7 | Upgrade any non-special item's quality to `150` |
| R6 | Upgrade any non-special item's quality to `175` |
| R7 | Upgrade any non-special item's quality to `200` |

## Shield

Source: `Assembly-CSharp\BNCBECFCPHP.cs`

### EquipPointCost

Source line: `618`, obfuscated property: `OMIBOKEONLA`.

```csharp
protected override int OMIBOKEONLA
	{
		get
		{
			int num = this.DNONFFBHEEM.Ep - (int)base.PPAFMKOLBBL + 1 + BNCBECFCPHP.GetEpCostMod(this.DNONFFBHEEM.Class.GetFaction());
			if (num > 0)
			{
				return num;
			}
			return 0;
		}
	}
```

### IncomingDamage

Source line: `754`, obfuscated property: `PLHGOLKMLJJ`.

```csharp
protected override float PLHGOLKMLJJ
	{
		get
		{
			int modelNumber = this.CECBGCDJJAH.GetModelNumber();
			if (modelNumber != 4 && modelNumber - 9 > 1)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * -0.015f * base.EDPOPGPNMCD;
		}
	}
```

### HackResist

Source line: `244`, obfuscated property: `IJICKEGDCCE`.

```csharp
protected override float IJICKEGDCCE
	{
		get
		{
			int modelNumber = this.CECBGCDJJAH.GetModelNumber();
			if (modelNumber - 3 > 1 && modelNumber != 12)
			{
				return 0f;
			}
			return this.InternalGetResistMod();
		}
	}
```

### GrappleResist

Source line: `9`, obfuscated property: `AFNCJMNENCA`.

```csharp
protected override float AFNCJMNENCA
	{
		get
		{
			int modelNumber = this.CECBGCDJJAH.GetModelNumber();
			if (modelNumber <= 3)
			{
				if (modelNumber == 1 || modelNumber == 3)
				{
					goto IL_29;
				}
			}
			else if (modelNumber == 7 || modelNumber == 11)
			{
				goto IL_29;
			}
			return 0f;
			IL_29:
			return this.InternalGetResistMod();
		}
	}
```

### CriticalResist

Source line: `303`, obfuscated property: `CDLEBDHOLGB`.

```csharp
protected override float CDLEBDHOLGB
	{
		get
		{
			int modelNumber = this.CECBGCDJJAH.GetModelNumber();
			if (modelNumber != 2 && modelNumber != 10 && modelNumber != 12)
			{
				return 0f;
			}
			return this.InternalGetResistMod();
		}
	}
```

### SplashResist

Source line: `804`, obfuscated property: `BFILEEDOAPJ`.

```csharp
protected override float BFILEEDOAPJ
	{
		get
		{
			int modelNumber = this.CECBGCDJJAH.GetModelNumber();
			if (modelNumber != 2 && modelNumber != 5 && modelNumber != 11)
			{
				return 0f;
			}
			return this.InternalGetResistMod();
		}
	}
```

### BatteryDrainResist

Source line: `171`, obfuscated property: `LDOFEGMICPK`.

```csharp
protected override float LDOFEGMICPK
	{
		get
		{
			int modelNumber = this.CECBGCDJJAH.GetModelNumber();
			if (modelNumber != 1 && modelNumber != 6 && modelNumber != 9)
			{
				return 0f;
			}
			return this.InternalGetResistMod() * 1.5f;
		}
	}
```

### ShieldCapacity

Source line: `718`, obfuscated property: `KHAGACJJONM`.

```csharp
protected override float KHAGACJJONM
	{
		get
		{
			int modelNumber = this.CECBGCDJJAH.GetModelNumber();
			if (modelNumber - 5 <= 2)
			{
				return 1.25f * this.InternalGetShieldCapacity() * this.NDOJHMKGBFK.GetMod() * 1.15f;
			}
			if (modelNumber != 8)
			{
				return this.InternalGetShieldCapacity() * this.NDOJHMKGBFK.GetMod() * 1.15f;
			}
			return 1.5f * this.InternalGetShieldCapacity() * this.NDOJHMKGBFK.GetMod() * 1.15f;
		}
	}
```

## Engine

Source: `Assembly-CSharp\OIBAMMKGNBK.cs`

### EquipPointCost

Source line: `647`, obfuscated property: `OMIBOKEONLA`.

```csharp
protected override int OMIBOKEONLA
	{
		get
		{
			return 0;
		}
	}
```

### EquipPointMax

Source line: `355`, obfuscated property: `AKAAAIOKMOP`.

```csharp
protected override int AKAAAIOKMOP
	{
		get
		{
			if (this.CECBGCDJJAH != JOPMBBDJMIO.Gravity)
			{
				if (base.PPAFMKOLBBL < AHKIAECFDDB.R6)
				{
					return 0;
				}
				return 1;
			}
			else
			{
				if (base.PPAFMKOLBBL < AHKIAECFDDB.R7)
				{
					return 0;
				}
				return 1;
			}
		}
	}
```

### MoveSpeedPercent

Source line: `108`, obfuscated property: `JCKNDPELNLG`.

```csharp
protected override float JCKNDPELNLG
	{
		get
		{
			JOPMBBDJMIO @class = this.CECBGCDJJAH;
			if (@class - JOPMBBDJMIO.Impulse > 2)
			{
				return 0f;
			}
			return -0.0125f * (float)base.PPAFMKOLBBL * base.EDPOPGPNMCD;
		}
	}
```

### CriticalDamage

Source line: `1003`, obfuscated property: `EPIANIDJPJF`.

```csharp
protected override float EPIANIDJPJF
	{
		get
		{
			if (this.CECBGCDJJAH != JOPMBBDJMIO.Neutron)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 0.01f * base.EDPOPGPNMCD;
		}
	}
```

### EvasionChance

Source line: `295`, obfuscated property: `CICMMLJMJKP`.

```csharp
protected override float CICMMLJMJKP
	{
		get
		{
			JOPMBBDJMIO @class = this.CECBGCDJJAH;
			if (@class == JOPMBBDJMIO.Fusion)
			{
				return (float)base.PPAFMKOLBBL * 1.5f * base.EDPOPGPNMCD;
			}
			if (@class != JOPMBBDJMIO.Neutron)
			{
				return (float)base.PPAFMKOLBBL * 0.5f * base.EDPOPGPNMCD;
			}
			return 0f;
		}
	}
```

### GrappleResist

Source line: `792`, obfuscated property: `AFNCJMNENCA`.

```csharp
protected override float AFNCJMNENCA
	{
		get
		{
			if (this.CECBGCDJJAH != JOPMBBDJMIO.Impulse)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 2f * base.EDPOPGPNMCD;
		}
	}
```

### CriticalResist

Source line: `778`, obfuscated property: `CDLEBDHOLGB`.

```csharp
protected override float CDLEBDHOLGB
	{
		get
		{
			if (this.CECBGCDJJAH != JOPMBBDJMIO.Neutron)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * base.EDPOPGPNMCD;
		}
	}
```

### PowerCapacity

Source line: `864`, obfuscated property: `JEFDOBNBCJO`.

```csharp
protected override float JEFDOBNBCJO
	{
		get
		{
			if (this.CECBGCDJJAH != JOPMBBDJMIO.Atomic)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * base.EDPOPGPNMCD;
		}
	}
```

## Battery

Source: `Assembly-CSharp\ECCOKHAPHDD.cs`

### EquipPointCost

Source line: `460`, obfuscated property: `OMIBOKEONLA`.

```csharp
protected override int OMIBOKEONLA
	{
		get
		{
			return 0;
		}
	}
```

### EquipPointMax

Source line: `436`, obfuscated property: `AKAAAIOKMOP`.

```csharp
protected override int AKAAAIOKMOP
	{
		get
		{
			if (base.PPAFMKOLBBL < AHKIAECFDDB.R7)
			{
				return 0;
			}
			return 1;
		}
	}
```

### MoveSpeedPercent

Source line: `814`, obfuscated property: `JCKNDPELNLG`.

```csharp
protected override float JCKNDPELNLG
	{
		get
		{
			EAHJHMGGHGM @class = this.DNONFFBHEEM.Class;
			if (@class - EAHJHMGGHGM.Alkaic <= 1)
			{
				return -0.01f * (float)base.PPAFMKOLBBL * base.EDPOPGPNMCD;
			}
			if (@class != EAHJHMGGHGM.Voltaic)
			{
				return 0f;
			}
			return -0.015f * (float)base.PPAFMKOLBBL * base.EDPOPGPNMCD;
		}
	}
```

### HullRepair

Source line: `196`, obfuscated property: `LDCKLGHOKDN`.

```csharp
protected override float LDCKLGHOKDN
	{
		get
		{
			if (this.DNONFFBHEEM.Class != EAHJHMGGHGM.Alkaic)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 0.003f * base.EDPOPGPNMCD;
		}
	}
```

### ShieldDamage

Source line: `364`, obfuscated property: `AEDGBNCKKPF`.

```csharp
protected override float AEDGBNCKKPF
	{
		get
		{
			EAHJHMGGHGM @class = this.DNONFFBHEEM.Class;
			if (@class - EAHJHMGGHGM.Zambic > 1)
			{
				return 0f;
			}
			return (0.01f + (float)base.PPAFMKOLBBL * 0.01f) * base.EDPOPGPNMCD;
		}
	}
```

### XpBonus

Source line: `154`, obfuscated property: `LMJGMPDOOHH`.

```csharp
protected override float LMJGMPDOOHH
	{
		get
		{
			EAHJHMGGHGM @class = this.DNONFFBHEEM.Class;
			if (@class != EAHJHMGGHGM.Galvanic && @class != EAHJHMGGHGM.Silic)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 0.015f * base.EDPOPGPNMCD;
		}
	}
```

### CriticalChance

Source line: `686`, obfuscated property: `MOLDAGLDGFJ`.

```csharp
protected override float MOLDAGLDGFJ
	{
		get
		{
			if (this.DNONFFBHEEM.Class != EAHJHMGGHGM.Galvanic)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 0.5f * base.EDPOPGPNMCD;
		}
	}
```

### EvasionChance

Source line: `763`, obfuscated property: `CICMMLJMJKP`.

```csharp
protected override float CICMMLJMJKP
	{
		get
		{
			if (this.DNONFFBHEEM.Class != EAHJHMGGHGM.Hydric)
			{
				return 0f;
			}
			return (1f + (float)base.PPAFMKOLBBL * 1f) * base.EDPOPGPNMCD;
		}
	}
```

### BatteryDrainPower

Source line: `51`, obfuscated property: `AKHIEAMMMAD`.

```csharp
protected override float AKHIEAMMMAD
	{
		get
		{
			if (this.DNONFFBHEEM.Class != EAHJHMGGHGM.Chromic)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 1.5f * base.EDPOPGPNMCD;
		}
	}
```

### GrapplePower

Source line: `422`, obfuscated property: `AAALLHAEEIB`.

```csharp
protected override float AAALLHAEEIB
	{
		get
		{
			if (this.DNONFFBHEEM.Class != EAHJHMGGHGM.Hydric)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 1.5f * base.EDPOPGPNMCD;
		}
	}
```

### HitChance

Source line: `580`, obfuscated property: `AMFJDLDNMHO`.

```csharp
protected override float AMFJDLDNMHO
	{
		get
		{
			if (this.DNONFFBHEEM.Class != EAHJHMGGHGM.Silic)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 1.5f * base.EDPOPGPNMCD;
		}
	}
```

### HackResist

Source line: `295`, obfuscated property: `IJICKEGDCCE`.

```csharp
protected override float IJICKEGDCCE
	{
		get
		{
			switch (this.DNONFFBHEEM.Class)
			{
			case EAHJHMGGHGM.Alkaic:
			case EAHJHMGGHGM.Galvanic:
			case EAHJHMGGHGM.Voltaic:
			case EAHJHMGGHGM.Silic:
			case EAHJHMGGHGM.Polyanic:
				return (1f + (float)base.PPAFMKOLBBL) * base.EDPOPGPNMCD;
			default:
				return 0f;
			case EAHJHMGGHGM.Lithic:
				if (base.PPAFMKOLBBL < AHKIAECFDDB.R3)
				{
					return 0f;
				}
				return (1f + (float)base.PPAFMKOLBBL - 1f) * base.EDPOPGPNMCD;
			}
		}
	}
```

### GrappleResist

Source line: `865`, obfuscated property: `AFNCJMNENCA`.

```csharp
protected override float AFNCJMNENCA
	{
		get
		{
			EAHJHMGGHGM @class = this.DNONFFBHEEM.Class;
			if (@class != EAHJHMGGHGM.Mercuric && @class != EAHJHMGGHGM.Zambic && @class != EAHJHMGGHGM.Radionic)
			{
				return 0f;
			}
			return (1f + (float)base.PPAFMKOLBBL) * base.EDPOPGPNMCD;
		}
	}
```

### CriticalResist

Source line: `717`, obfuscated property: `CDLEBDHOLGB`.

```csharp
protected override float CDLEBDHOLGB
	{
		get
		{
			switch (this.DNONFFBHEEM.Class)
			{
			case EAHJHMGGHGM.Lithic:
				if (base.PPAFMKOLBBL < AHKIAECFDDB.R3)
				{
					return 0f;
				}
				return (1f + (float)base.PPAFMKOLBBL - 1f) * base.EDPOPGPNMCD;
			case EAHJHMGGHGM.Zambic:
			case EAHJHMGGHGM.Moltic:
			case EAHJHMGGHGM.Polyanic:
			case EAHJHMGGHGM.Radionic:
				return (1f + (float)base.PPAFMKOLBBL) * base.EDPOPGPNMCD;
			default:
				return 0f;
			}
		}
	}
```

### SplashResist

Source line: `470`, obfuscated property: `BFILEEDOAPJ`.

```csharp
protected override float BFILEEDOAPJ
	{
		get
		{
			EAHJHMGGHGM @class = this.DNONFFBHEEM.Class;
			if (@class - EAHJHMGGHGM.Alkaic > 1 && @class - EAHJHMGGHGM.Mercuric > 1)
			{
				return 0f;
			}
			return (1f + (float)base.PPAFMKOLBBL) * base.EDPOPGPNMCD;
		}
	}
```

### BatteryDrainResist

Source line: `513`, obfuscated property: `LDOFEGMICPK`.

```csharp
protected override float LDOFEGMICPK
	{
		get
		{
			EAHJHMGGHGM @class = this.DNONFFBHEEM.Class;
			if (@class - EAHJHMGGHGM.Moltic > 1)
			{
				return 0f;
			}
			return (1f + (float)base.PPAFMKOLBBL * 1.5f) * base.EDPOPGPNMCD;
		}
	}
```

### PowerRecharge

Source line: `118`, obfuscated property: `ENGLBKJJOGE`.

```csharp
protected override float ENGLBKJJOGE
	{
		get
		{
			switch (base.PPAFMKOLBBL)
			{
			case AHKIAECFDDB.R2:
				return 0.69f * base.EDPOPGPNMCD;
			case AHKIAECFDDB.R3:
				return 0.78000003f * base.EDPOPGPNMCD;
			case AHKIAECFDDB.R4:
				return 0.87000006f * base.EDPOPGPNMCD;
			case AHKIAECFDDB.R5:
				return 0.96000004f * base.EDPOPGPNMCD;
			case AHKIAECFDDB.R6:
				return 1.0500001f * base.EDPOPGPNMCD;
			case AHKIAECFDDB.R7:
				return 1.14f * base.EDPOPGPNMCD;
			default:
				return 0.6f * base.EDPOPGPNMCD;
			}
		}
	}
```

### PowerCapacity

Source line: `400`, obfuscated property: `JEFDOBNBCJO`.

```csharp
protected override float JEFDOBNBCJO
	{
		get
		{
			return (3f + (float)base.PPAFMKOLBBL * 3f) * base.EDPOPGPNMCD;
		}
	}
```

### ShieldCapacity

Source line: `550`, obfuscated property: `KHAGACJJONM`.

```csharp
protected override float KHAGACJJONM
	{
		get
		{
			EAHJHMGGHGM @class = this.DNONFFBHEEM.Class;
			if (@class == EAHJHMGGHGM.Mercuric || @class == EAHJHMGGHGM.Lithic)
			{
				return (float)base.PPAFMKOLBBL * 50f * base.EDPOPGPNMCD * 1.15f;
			}
			if (@class != EAHJHMGGHGM.Radionic)
			{
				return 0f;
			}
			return (float)base.PPAFMKOLBBL * 25f * base.EDPOPGPNMCD * 1.15f;
		}
	}
```

### ShieldPenetration

Source line: `91`, obfuscated property: `BIDNACKAGFL`.

```csharp
protected override float BIDNACKAGFL
	{
		get
		{
			EAHJHMGGHGM @class = this.DNONFFBHEEM.Class;
			if (@class - EAHJHMGGHGM.Chromic > 1)
			{
				return 0f;
			}
			return (0.01f + (float)base.PPAFMKOLBBL * 0.01f) * base.EDPOPGPNMCD;
		}
	}
```

### TargetingSpeedPercent

Source line: `604`, obfuscated property: `KHLBGHAAHOE`.

```csharp
protected override float KHLBGHAAHOE
	{
		get
		{
			if (this.DNONFFBHEEM.Class != EAHJHMGGHGM.Moltic)
			{
				return 0f;
			}
			return -0.025f * (float)base.PPAFMKOLBBL * base.EDPOPGPNMCD;
		}
	}
```
