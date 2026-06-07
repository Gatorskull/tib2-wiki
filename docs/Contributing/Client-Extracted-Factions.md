# Client-Extracted Faction Differences

This page summarizes faction-specific mechanics found during client extraction. It points back to the more detailed extraction pages instead of duplicating every item/ship table.

## Faction Enum

Source: `ONCHPJDOFKP.cs`.

| Enum order | Faction |
|---:|---|
| 0 | `NULL` |
| 1 | `Human` |
| 2 | `Wyrd` |
| 3 | `Pirate` |
| 4 | `Het` |
| 5 | `Precursor` |

## Ship Faction Differences

Source: `Client-Extracted-Ships.md`.

| Area | Human | Wyrd | Pirate | Het | Precursor |
|---|---|---|---|---|---|
| Base EP trend | Lowest baseline | +1 over Human on most ships | +1 over Human on most ships | +1 over Human on most ships | Highest baseline, usually +2 over Human |
| Required levels | Lowest | Higher than Pirate/Het on many ships | Low alien requirements | Between Pirate and Wyrd | Highest requirements |
| Weapon slots | Human Emperor has 5 instead of 6 | normal | normal | normal | +1 weapon slot on Small through Huge, including Shuttle and Carrier special cases |
| Drone slots | Huge Human ships have 3; Human Emperor has 5 | normal | normal | +1 drone slot on most sizes and special cases | normal |
| Battery slots | Human Emperor has 5 | +1 battery slot on Small through Huge and special cases | normal | normal | normal |
| Skull craft costs | Half of non-Human default for advanced ships | non-Human default | non-Human default | non-Human default | non-Human default |
| Shipyard level shortcut | Human Shuttle through Human Flagship return required Shipyard level 0 | normal | normal | normal | normal |

## Ship Craft Resource Biases

Source: `Client-Extracted-Ships.md`, `GetCraftResourceRequirement(...)`.

| Resource | Faction-specific multiplier rule |
|---|---|
| Crew | Human or Het `29`; otherwise `32` |
| Organic | Het `27`; otherwise `24` |
| Gas | Wyrd `22`; otherwise `19` |
| Metal | Pirate `32`; otherwise `29` |
| Radioactive | Wyrd or Precursor `28`; otherwise `25` |
| Darkmatter | Precursor `20`; otherwise `17` |

These are crafting resource formulas, not strategy recommendations.

## Defense Affinity Default Techs

Source: `Client-Extracted-Structures.md`.

| Affinity | Default tech identity |
|---|---|
| Wyrd | Shield Capacitors by rank; Advanced Hacking by rank |
| Pirate | Advanced Alloys by rank; Attack Drones by rank |
| Het | Shield Pierce by rank; Technician by rank |
| Precursor | Shield Amplifier by rank; Advanced Draining by rank |

The extracted helper did not list a Human affinity branch in the same default-tech table.

## Item Faction Differences

Sources: `Client-Extracted-Items.md`, `Client-Extracted-Item-Stat-Formulas-Narrow.md`.

| Item area | Faction-specific rule |
|---|---|
| Shields | Class prefix maps to faction: `A` Precursor, `B` Wyrd, `C` Het, `D` Pirate, `E` Human. |
| Shield capacity | Precursor has the highest base shield-capacity coefficient; Human/default the lowest. |
| Shield resist | Human/default has the highest shared resist coefficient; Precursor the lowest. |
| Shield EP modifier | Human/default `0`, Pirate `1`, Het `2`, Wyrd `3`, Precursor `4`. |
| Drones | Prefix maps to faction: `BAS` Human, `LCD` Pirate, `HX` Het, `WP` Wyrd, `DCD` Precursor. |
| Drone EP | Faction/category/rarity table; higher alien factions generally carry higher EP before rarity reductions. |
| Harvest drones | Pirate has fastest harvest timer multiplier; Precursor slowest, but Precursor harvest drones return the most resource per harvest. |
| Fighter/repair drones | Attack/repair formulas use a faction attack-bonus value: Human `0`, Pirate `1`, Het `2`, Wyrd `3`, Precursor `4`. |
| Batteries | Capacity bonuses apply when the ship is Pirate or when the battery faction matches the ship faction. |
| Engines, computers, specials, storage, armor | Client maps classes/categories to factions; see the item extraction pages for full tables. |

## Public Page Guidance

- Keep faction **lore** on the faction lore pages.
- Keep faction **mechanics** on Ships, Items, Structures, Crafting, and this contributor reference.
- Keep faction **build advice** and “best faction” claims in Strategy pages, dated or labeled as community guidance.
- Avoid presenting extracted faction coefficients as recommendations; they are rules data, not a meta tier list.
