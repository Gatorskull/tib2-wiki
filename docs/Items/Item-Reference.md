# Item Reference

This page collects item formulas and lookup tables. Use it for stable numbers; use the other item pages for explanations.

## Quality Multiplier

The quality multiplier is:

```text
quality multiplier = (void item ? 1.1 : 1.0) + qualityValue / 1000
```

`qualityValue` is the item's internal quality value.

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

## Gear Score

Item gear score is:

```text
round(rarity gear-score base * quality multiplier + item EP cost * rarity)
```

| Rarity | Gear-score base |
|---|---:|
| Common | 25 |
| Uncommon | 50 |
| Rare | 100 |
| Ultra-Rare | 200 |
| Elite | 300 |
| Legendary | 450 |
| Ultimate | 700 |

## Required Player Level

Base required levels by rarity:

| Rarity | Base required level |
|---|---:|
| Common | 0 |
| Uncommon | 0 |
| Rare | 0 |
| Ultra-Rare | 8 |
| Elite | 12 |
| Legendary | 16 |
| Ultimate | 20 |

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

## Equip Point Cost Notes

Equip Point formula notes:

- Weapons, armor, and storage use `max(0, item rank - item rarity + 1)`.
- Shields use the same pattern plus a shield-faction modifier: Human/default `0`, Pirate `1`, Het `2`, Wyrd `3`, Precursor `4`.
- Drones use a separate faction/category/rarity table and then clamp negative values to `0`.
- Engines, computers, specials, batteries, and consumables have `0` base Equip Point cost in the checked formulas.

Needs data:

- Exact rank/base `Ep` values for weapons, armor, storage, and shields still need a deeper data-table pass before publishing a complete item EP table.

## See Also

* [Items](index.md)
* [Item Upgrades](Item-Upgrades.md)
* [Void Items](Void-Items.md)
* [Equipment Slots](Equipment-Slots.md)
* [Equip Points](../Ships/Equip-Points.md)
