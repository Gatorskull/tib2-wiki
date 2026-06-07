# Client-Extracted Loot And Rewards

This page records loot and reward behavior found in the decompiled 2.1.0 Steam client. Treat this as **client-visible rules and display data**, not a full server drop table. Actual drop rolls, pity progression math, and reward issuance are likely server-controlled unless a specific client formula is listed here.

## Cargo Reward Entities

Sources: `TibSharp\Expansion\Library\Database\CargoMoneyDbObj.cs`, `CargoItemDbObj.cs`, `CargoResourceDbObj.cs`.

The client has three cargo/reward entity payloads:

| Entity type | Runtime class | DB object | Payload |
|---|---|---|---|
| `CargoMoney` | `BLGMBFBBDHK` | `CargoMoneyDbObj` | `Credits`, `Skulls` |
| `CargoItem` | `MNGDHFFMGBM` | `CargoItemDbObj` | `ItemId` |
| `CargoResource` | `NFPLLCBJOEG` | `CargoResourceDbObj` | `Resource`, `Count` |

These confirm the reward containers the client can display/sync, but not how the server decides to spawn them.

## Consumable Piles

Source: `Client-Extracted-Items.md` extraction from `PIBAEAKHECA.cs`, `NLLPDCFPKJM.cs`, `OMPIMDNGMHG.cs`.

Client-visible pile sizes:

| Pile type | Counts |
|---|---|
| Resource piles | `100`, `500`, `1000`, `5000` |
| Skull piles | `10`, `100`, `500`, `1000` |
| Relic piles | `1`, `5`, `10`, `50`, `100` |

Resource and Skull piles are grouped as `Crafting Resources` by the client. Relic piles use metadata to select faction.

## Scavenger And Harvesting Bonus Text

Sources: `DFHOJHHBAMJ.cs`, `DDEIFGPEOMI.cs`.

`DDEIFGPEOMI.GetScavengerRank()` and `GetHarvestingRank()` use the highest active rank from 1 through 7.

| Technology family | Rank values shown by client |
|---|---|
| Scavenger | `2%`, `4%`, `6%`, `8%`, `10%`, `12%`, `14%` Fleet Resource & Loot Bonus Chance |
| Harvesting | `5%`, `10%`, `15%`, `20%`, `25%`, `30%`, `35%` Resource Harvest Bonus Chance; also says Gain XP From Asteroids |

The client text names these as chance bonuses. The exact server roll mechanics are not confirmed by these methods.

## Pity Counter Fields

Sources: `TibSharp\Expansion\Library\Database\PlayerDbObj.cs`.

The player database object stores pity-related integer fields:

| Field | Notes |
|---|---|
| `Pity1` through `Pity7` | One stored counter per item rarity tier, inferred from naming and field family |
| `PityR` | Separate stored pity counter, likely relic-related by naming and old wiki/training context |

`PlayerDbObj.Populate(...)` copies these fields into the runtime player object. This confirms that pity progress exists as persisted player state, but this pass did not find the actual drop-roll or pity-increment formula in the client. Treat exact thresholds, reset rules, Security Rating multipliers, and relic-pity behavior as server/training data until confirmed elsewhere.

## Loot Achievement And Leaderboard Ladders

Sources: `PCPMMMCCILL.cs`, `AHFAPFNMNPJ.cs`, `DbStats.cs`, `DIANDBKMEHE.cs`, `OGHCKGOOEPK.cs`.

The client tracks total loot and per-rarity loot achievement milestones. For each rarity `R1` through `R7`, `GetLootRarity(rarity, count)` maps counts to achievement ids at these thresholds:

| Threshold count | Achievement tier suffix |
|---:|---|
| 5 | `_5` |
| 10 | `_10` |
| 25 | `_25` |
| 50 | `_50` |
| 100 | `_100` |
| 200 | `_200` |
| 300 | `_300` |
| 400 | `_400` |
| 500 | `_500` |
| 1000 | `_1000` |
| 2000 | `_2000` |
| 3000 | `_3000` |
| 4000 | `_4000` |
| 5000 | `_5000` |
| 10000 | `_10000` |

The non-rarity total-loot ladder starts at 5 and includes 5, 10, 25, 50, 75, 100, 150, 200, then 100-step thresholds through 1000 and larger thresholds after that.

Leaderboard/stat fields:

| Leaderboard/stat | Source field |
|---|---|
| ItemsLooted | `LootR1 + LootR2 + LootR3 + LootR4 + LootR5 + LootR6 + LootR7` |
| LegendaryLoot | `LootR6` |
| UltimateLoot | `LootR7` |
| RelicsLooted | faction relic totals |
| InvasionItemsLooted | `InvasionLoot` |

These are tracking/display systems. They do not reveal drop odds.

## Party Box Activity Types

Sources: `OMDIMDNOAJG.cs`, `DFHOJHHBAMJ.cs`.

Client party activity enum:

| Enum | Client task text pattern |
|---|---|
| `Invasion` | Loot bonus for next Invasion Victory/Victories |
| `Planet` | Loot bonus for next NPC Planet Kill/Kills |
| `Garrison` | Loot bonus for next NPC Garrison Kill/Kills |
| `Shipyard` | Loot bonus for next NPC Shipyard Kill/Kills |
| `Outpost` | Loot bonus for next NPC Outpost Kill/Kills |
| `Missions` | Complete Mission/Missions for a loot bonus |
| `Assassin` | Kill Assassin Leader/Leaders for a loot bonus |
| `Pirate` | Kill Elite-ADV Pirate/Pirates for a loot bonus |
| `Het` | Kill Elite-ADV Het/Hets for a loot bonus |
| `Wyrd` | Kill Elite-ADV Wyrd/Wyrds for a loot bonus |
| `Precursor` | Kill Elite-ADV Precursor/Precursors for a loot bonus |
| `Critical` | Next Critical Attack(s) are Overpower Advanced |
| `Repair` | Next Hull Repair(s) are Overpower Advanced |
| `Grapple` | Next Grapple Attack(s) are Overpower Advanced |
| `Hack` | Next Hack Attack(s) are Overpower Advanced |
| `Harvest` | Next Harvest(s) are Overpower Advanced |

Client helpers:

- `GetIsActivityType()` is true for `Invasion` through `Precursor`.
- `GetIsFactionHuntType()` is true for `Pirate`, `Het`, `Wyrd`, and `Precursor`.
- `GetIsDefenseBust(type, entityType)` maps `Planet`, `Garrison`, `Shipyard`, and `Outpost` activity types to matching defense-unit entity types.
- `GetIsNpcFaction(type, faction)` maps `Pirate`, `Het`, `Wyrd`, and `Precursor` hunt types to matching NPC factions.

## Party Box Max Counts

Source: `DFHOJHHBAMJ.GetMaxCount(this OMDIMDNOAJG, AHKIAECFDDB)`.

For activity rewards, the client uses the party-box rarity to determine the maximum task count shown.

| Activity group | Default / R1-R3 | R4 | R5 | R6 | R7 |
|---|---:|---:|---:|---:|---:|
| Missions | 3 | 5 | 7 | 9 | 15 |
| Assassin leaders | 3 | 5 | 10 | 15 | 20 |
| Faction hunts: Pirate/Het/Wyrd/Precursor | 10 | 15 | 25 | 35 | 50 |
| Buffs: Critical/Repair/Grapple/Hack/Harvest | `rarity * R3` | `rarity * R3` | `rarity * R3` | `rarity * R3` | `rarity * R3` |
| Invasion/Planet/Garrison/Shipyard/Outpost/default | 1 | 1 | 1 | 1 | 1 |

The buff formula depends on enum numeric values for `AHKIAECFDDB`; keep the public page descriptive unless the rarity enum values are documented beside it.

## Daily/Event Reward Text

Source: `DFHOJHHBAMJ.GetDailyTechDescription(this ENIALFMHHLL, byte)`.

The client includes daily/event descriptions related to rewards:

- Mission Rewards Doubled.
- Arena Awards Bonus Loot and Skulls.
- Pirate & Alien Defense Units Drop Bonus Loot.
- Double Skulls for World PvP Kills.
- Double Rewards for Alliance Defense Kills.
- Double Loot for Hardcore Ships in PvP & Homeworld Maps.
- Invasion Bosses Drop Blueprints.
- Assassin Leaders Can Drop Powerful Item Blueprints.
- Invasion Bosses Drop Powerful Holiday Gem Loot.
- Rescue Drifting Crew for Rewards.
- Alien Leaders & Invasion Bosses Always Drop Void Loot.
- Double Item Rewards for Invasion & Arena Victory.
- Bonus Loot and PvP Skulls with Low Item Durability Damage.
- Special Holiday Event.

These are descriptions of possible daily/event states, not proof that the event is active at any specific time.

## Needs Server Or Training Confirmation

- Exact pity loot thresholds and progress multipliers.
- Exact meaning of `PityR`.
- Exact drop chances for Scavenger, Harvesting, security rating, invasions, defense units, and daily/event bonuses.
- Whether Party Box reward issuance has additional server-side eligibility checks beyond the client-visible activity/faction/defense type helpers.
- Whether cargo rewards have despawn timers, ownership windows, or pickup restrictions not visible in the DB payload classes.
