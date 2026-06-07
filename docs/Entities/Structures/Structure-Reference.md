# Structure Reference

This page collects structure and defense-unit tables. Use it for numbers; use the other structure pages for explanations.

## Use This For

| If you need to know... | Use |
|------------------------|-----|
| How many structures a corporation can own | [Corporation Defense Caps](#corporation-defense-caps) |
| Tech Point cost to unlock another defense unit | [Build Cap Tech Point Costs](#build-cap-tech-point-costs) |
| How many Equip Points a defense unit has | [Base Equip Points](#base-equip-points) |
| Slot unlocks by defense-unit level | [Base Weapon Slots](#base-weapon-slots), [Base Drone Slots](#base-drone-slots), [Base Battery Slots](#base-battery-slots) |
| Default structure technology | [Default Defense Technology](#default-defense-technology) |
| Hull and shield scale by structure type | [Structure Multipliers](#structure-multipliers) |

## Corporation Defense Caps

| Defense type | Default max |
|---|---:|
| Garrisons | 4 |
| Outposts | 8 |
| Shipyards | 4 |

The corporation cannot add more of a defense type once the current count reaches the max.

## Build Cap Tech Point Costs

The cost to unlock the next structure depends on how many of that structure type the corporation already owns.

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

## Base Equip Points

Defense-unit Equip Points scale from structure type, Hardcore status, level, and Elite Rank.

| Structure | Normal base | Hardcore base | Level bonus | Elite Rank bonus |
|---|---:|---:|---:|---:|
| Planet | 30 | 40 | `floor(level / 10)` | `+5` per rank |
| Garrison | 20 | 30 | `floor(level / 10)` | `+4` per rank |
| Outpost | 15 | 25 | `floor(level / 10)` | `+3` per rank |
| Shipyard | 15 | 25 | `floor(level / 10)` | `+3` per rank |

Total Equip Points are the base value plus the level bonus and Elite Rank bonus.

## Base Weapon Slots

| Level | Weapon slots |
|---:|---:|
| `< 3` | 1 |
| `3-8` | 2 |
| `9-14` | 3 |
| `15-32` | 4 |
| `33-76` | 5 |
| `77+` | 6 |

## Base Drone Slots

| Level | Drone slots |
|---:|---:|
| `< 5` | 1 |
| `5-10` | 2 |
| `11-26` | 3 |
| `27-53` | 4 |
| `54-87` | 5 |
| `88+` | 6 |

## Base Battery Slots

| Level | Battery slots |
|---:|---:|
| `< 2` | 1 |
| `2-6` | 2 |
| `7-12` | 3 |
| `13-45` | 4 |
| `46-98` | 5 |
| `99+` | 6 |

## Default Defense Technology

These are default technology lines attached to defense units. Use [Technology Reference](../../Gameplay/Technology-Reference.md) for effect values where available.

### Repair facility defaults

| Tech | Default defense type |
|---|---|
| `RepairFacility1` | Outpost |
| `RepairFacility2` | Garrison |
| `RepairFacility3` | Planet |
| `RepairFacility4` | Shipyard |

### Rank-based defaults

| Tech | Default condition |
|---|---|
| `Intimidation1` | defense rank `<= 1` |
| `Intimidation2` | defense rank `2-3` |
| `Intimidation3` | defense rank `>= 4` |
| `Vanquisher` | defense rank `>= 5` |

### Faction affinity defaults

| Affinity | Default techs |
|---|---|
| Wyrd | `ShieldCapacitors1` rank `<= 1`; `ShieldCapacitors2` rank `2-3`; `ShieldCapacitors3` rank `>= 4`; `AdvancedHacking1` rank `1-2`; `AdvancedHacking2` rank `>= 3` |
| Pirate | `AdvancedAlloys1` rank `1-2`; `AdvancedAlloys2` rank `>= 3`; `AttackDrones1` rank `<= 1`; `AttackDrones2` rank `2-3`; `AttackDrones3` rank `>= 4` |
| Het | `ShieldPierce1` rank `<= 1`; `ShieldPierce2` rank `2-3`; `ShieldPierce3` rank `>= 4`; `Technician1` rank `1-2`; `Technician2` rank `>= 3` |
| Precursor | `ShieldAmplifier1` rank `<= 1`; `ShieldAmplifier2` rank `2-3`; `ShieldAmplifier3` rank `>= 4`; `AdvancedDraining1` rank `1-2`; `AdvancedDraining2` rank `>= 3` |

## Structure Multipliers

| Entity type | Hull/shield multiplier | Base hull term |
|---|---:|---:|
| Planet | 40 | 10000 |
| Garrison | 30 | 10000 |
| Outpost | 12 | 10000 |
| Shipyard | 12 | 10000 |
| Ship/default | 1 | 1400 |

## See Also

* [Structures](index.md)
* [Planets](Planets.md)
* [Garrisons](Garrisons.md)
* [Outposts](Outposts.md)
* [Shipyards](Shipyards.md)
