# Loot and Reward Reference

This page collects loot and reward data that can be documented safely. It does not list drop odds unless a specific formula is known.

## Use This For

| If you need to know... | Use |
|------------------------|-----|
| What cargo reward containers can hold | [Cargo Reward Entities](#cargo-reward-entities) |
| Standard resource, Skull, or Relic pile sizes | [Consumable Piles](#consumable-piles) |
| Scavenger or Harvesting bonus text | [Scavenger and Harvesting Bonus Text](#scavenger-and-harvesting-bonus-text) |
| Which pity counters exist | [Pity Counter Fields](#pity-counter-fields) |
| Party Box task-count caps by rarity | [Party Box Max Counts](#party-box-max-counts) |
| Possible daily or event reward descriptions | [Possible Daily/Event Reward Text](#possible-dailyevent-reward-text) |

## Cargo Reward Entities

Cargo rewards can appear in three forms:

| Reward type | Contains |
|---|---|
| `CargoMoney` | Credits, Skulls |
| `CargoItem` | Item id |
| `CargoResource` | Resource, count |

These are reward container types, not drop chances. Use them to understand what a reward object can contain.

## Consumable Piles

| Pile type | Counts |
|---|---|
| Resource piles | `100`, `500`, `1000`, `5000` |
| Skull piles | `10`, `100`, `500`, `1000` |
| Relic piles | `1`, `5`, `10`, `50`, `100` |

Resource and Skull piles are grouped as `Crafting Resources`. Relic piles are faction-specific.

## Scavenger and Harvesting Bonus Text

The highest active rank from 1 through 7 is used.

| Technology family | Rank values |
|---|---|
| Scavenger | `2%`, `4%`, `6%`, `8%`, `10%`, `12%`, `14%` Fleet Resource and Loot Bonus Chance |
| Harvesting | `5%`, `10%`, `15%`, `20%`, `25%`, `30%`, `35%` Resource Harvest Bonus Chance; also says Gain XP From Asteroids |

These are chance bonuses. The exact roll mechanics still need confirmation.

## Pity Counter Fields

Pity progress is tracked separately for item rarity tiers:

| Counter | Notes |
|---|---|
| `Pity1` through `Pity7` | One counter per item rarity tier, from Common through Ultimate |
| `PityR` | Separate pity counter, likely relic-related by naming and training context |

Exact thresholds, reset rules, Security Rating multipliers, and relic-pity behavior still need confirmation.

## Party Box Max Counts

For activity rewards, party-box rarity determines the maximum task count shown.

| Activity group | Default / Common-Rare | Ultra-Rare | Elite | Legendary | Ultimate |
|---|---:|---:|---:|---:|---:|
| Missions | 3 | 5 | 7 | 9 | 15 |
| Assassin leaders | 3 | 5 | 10 | 15 | 20 |
| Faction hunts: Pirate/Het/Wyrd/Precursor | 10 | 15 | 25 | 35 | 50 |
| Invasion/Planet/Garrison/Shipyard/Outpost/default | 1 | 1 | 1 | 1 | 1 |

Buff party counts for Critical, Repair, Grapple, Hack, and Harvest need confirmation before being published as exact counts.

## Possible Daily/Event Reward Text

Possible daily or event reward states include:

- Mission Rewards Doubled.
- Arena Awards Bonus Loot and Skulls.
- Pirate and Alien Defense Units Drop Bonus Loot.
- Double Skulls for World PvP Kills.
- Double Rewards for Alliance Defense Kills.
- Double Loot for Hardcore Ships in PvP and Homeworld Maps.
- Invasion Bosses Drop Blueprints.
- Assassin Leaders Can Drop Powerful Item Blueprints.
- Invasion Bosses Drop Powerful Holiday Gem Loot.
- Rescue Drifting Crew for Rewards.
- Alien Leaders and Invasion Bosses Always Drop Void Loot.
- Double Item Rewards for Invasion and Arena Victory.
- Bonus Loot and PvP Skulls with Low Item Durability Damage.
- Special Holiday Event.

These are descriptions of possible daily/event states, not proof that an event is active now.

## See Also

* [Pity Loot](Pity-Loot.md)
* [Items](index.md)
* [Party Boxes](../Gameplay/Events/Party-Boxes.md)
* [Daily Events](../Gameplay/Events/Daily-Events.md)
