# Ship Crafting

[**Corporations**](../Entities/Corporations/index.md) level up their [**Shipyards**](../Entities/Structures/Shipyards.md) to unlock ship blueprints. Members build ships at the corp's shipyard; each Shipyard is dedicated to **one faction** (Pirate, Het, Wyrd, or Precursor). Corp leadership chooses the faction, opening advanced **alien-class** ships with different [**technology**](../Gameplay/Technology.md) -- more powerful but more expensive.

## Requirements

Ship construction checks:

- Ship class and faction must be valid.
- Some ships/factions require a minimum number of days in a corporation.
- Some ships/factions require [Skulls](../Entities/Currencies/Skulls.md).
- Some ships/factions require [Relics](../Entities/Currencies/Relics.md).
- Pirate construction uses Human relics for the relic-bank check.
- The player's ship garage must have room.
- Resource requirements are calculated per resource type.
- The acting ship must pass the shared ship validator.
- Construction requires an eligible friendly defense unit in the current sector, or an eligible corporation-owned [Shipyard](../Entities/Structures/Shipyards.md).
- Non-human Shipyards are ignored unless owned by the player's corporation.
- Missing resources block construction.

Larger ships generally have more [Equip Points](Equip-Points.md). Exact ship values belong in [Ship Reference](Ship-Reference.md), not repeated across guide pages.

## Ship Stat Bonus Mod

When you craft a ship it gains a **random Ship Stat Bonus Mod**. Its strength is comparable to a number of [**Skill Points**](../Gameplay/Skills.md):

* **Random roll:** Between **3** and **12** Skill Points equivalent.
* **Maximum (12)** is only possible during rare **daily crafting events**.
* **Ship Stat Modification** items can drop as loot, letting you **replace** this crafted bonus.

## Corporation Ship Crafting Skill

Building a ship increases your **corporation's ship crafting skill** for that faction (e.g. building a Wyrd Reaper increases Wyrd Ship Crafting Skill). Corporations can earn up to **1,000** ship crafting skill points **per day**. Higher corp ship crafting skill **improves** the Ship Stat Bonus Mod on newly built ships.

## Equip Point Bonus

There is a **1% chance** a crafted ship gains **+1 Equip Point**; rarely **+2** or **+3**.

---

## See Also

* [Ships](index.md)
* [Shipyards](../Entities/Structures/Shipyards.md)
* [Skulls](../Entities/Currencies/Skulls.md) and [Relics](../Entities/Currencies/Relics.md)
* [Corporations](../Entities/Corporations/index.md)
* [Item Crafting](../Items/Item-Crafting.md)
