# Item Crafting

**Captain Panel -> ITEM CRAFTING** -- Blueprints and resources live here. To craft an [item](index.md), collect the resources for a blueprint and click the blueprint. You **discover new blueprints** when you **Research** an item instead of scrapping it.

Crafting is connected to [corporations](../Entities/Corporations/index.md), resources, blueprints, and crafting skills.

---

## Crafting requirements

Item crafting checks:

- The item class must be valid.
- The blueprint's class and variant bytes must be valid for that item class.
- The player must have the matching item plan/blueprint unlocked.
- The craft skill for that item class is used.
- Resource requirements are calculated per resource type.
- If the crafting action is enforcing cooldown, any remaining cooldown for that craft skill blocks crafting.
- Missing resources block crafting.

Some menus may preview requirements without enforcing the cooldown. The exact cooldown display text is **Needs confirmation**.

## Quality

Each craft gives **crafting skill**. Skill improves the **quality** of crafted items:

* **Quality range:** 1 to 255.
* **Each point:** +0.1% to the item's [stats](Stats.md) -> **25.4%** difference between worst and best of the same rarity.
* Outside [The Arena](<../Gameplay/Activities/Player vs Player (PVP)/Arena.md>), loot with quality above 100 is rare.

## Skill Categories

There are **6** item crafting skill categories:

| Category | Builds |
|----------|--------|
| **Scientist** | Engines and Special-type items. |
| **Engineer** | Computers, Batteries, Storage. |
| **Weapons** | Weapons. |
| **Armor** | Armor. |
| **Shields** | Shields. |
| **Drones** | Drones. |

Most **Engine** and **Special-type** items enter the game only through crafting or unique events.

## Crafted item ownership

Crafted items are tagged with the creator's name.

## Commands

* **Queue** -- Click a blueprint multiple times to queue several crafts.
* **:CRAFT** in chat -- Management commands (e.g. clear queue, set lower skill rank for next craft).
* **:CRAFTVOID** -- Used by crafters for [Void](Void-Items.md) crafting.

---

## See Also

* [Items](index.md)
* [Void Items](Void-Items.md)
* [Special Items](Specials.md)
* [Tech Computers](Tech-Computers.md)
* [Ship Crafting](../Ships/Ship-Crafting.md)
* [Diminishing Returns](Diminishing-Returns.md)
* [Corporations](../Entities/Corporations/index.md)
* [Computer Deconstruction Strategy](../Strategy/Computer-Deconstruction.md)
* [Computer Deconstruction Quick Start](../Getting-Started/Quick-Start-Guides/Computer-Deconstruction-Quick-Start.md) -- cattabliss guide material on CPU/Tech Computer planning
