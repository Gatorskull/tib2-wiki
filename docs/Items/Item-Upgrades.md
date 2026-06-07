# Item Upgrades

The item inspect panel's **UPGRADE** menu is the canonical place for item rank, rarity, and repair actions. For action restrictions such as item lock, trade, sale listings, deconstruction, auctions, and corporation bank storage, see [Item Management](Item-Management.md).

---

## Engineering requirements

Item engineering checks:

- The item must exist.
- Items listed for sale must have the sale canceled first.
- Items currently in trade cannot be modified.
- Items with a temporary rarity upgrade cannot be modified.
- Equipped items cannot be modified while the owning entity is in the Arena queue.
- Equipped items cannot be modified while the owning entity is in Arena.
- Repair and rank actions are restricted to the player's own equipment.
- Ranking up an equipped item is blocked if the new Equip Point usage would exceed the entity's total [Equip Points](../Ships/Equip-Points.md).
- Upgrading an equipped item is blocked if the upgraded item would require a higher entity level than the equipped entity has.
- Some Void item upgrades require relics in the item crafting bank.

The exact action list and full per-action cost formulas still need extraction from the item-specific upgrade logic.

---

## Rarity Augmenting

Increasing an item's rarity is often called **augmenting**. Higher rarity can add power, unlock stronger item effects, improve some special-item technologies, and sometimes reduce [Equip Point](../Ships/Equip-Points.md) pressure.

Known source examples from community guide data:

| Upgrade | Example cost |
|---------|--------------|
| Uncommon Special -> Rare | 18 [Tech Points](../Entities/Currencies/Tech Points.md) |
| Rare -> Ultra-Rare | 36 Tech Points |
| Ultra-Rare -> Elite | 240 Tech Points |

!!! note "Needs confirmation"
    The examples above are guide values, not a complete rarity-cost table. Add more costs only after checking them in game.

!!! warning "Needs data"
    The wiki does not yet have a complete rarity augment cost table by item type, rarity, or server ruleset.

---

## Rank Up and Rank Down

Some item types can be increased or decreased in **rank**, including:

- Weapons
- Shields
- Storage
- Armor

Increasing an item's rank generally increases both its positive and negative stats. Rank changes can also change the item's [Equip Point](../Ships/Equip-Points.md) cost.

!!! warning "Needs data"
    The wiki does not yet have the exact rank scaling formula or full Equip Point cost table for ranked item types.

---

## Quality

Item quality affects item stats. See [Item Crafting](Item-Crafting.md) for crafting quality and [Void Items](Void-Items.md) for Void quality scaling.

Quality thresholds for deciding whether an item is worth upgrading are strategy, not rules. Put that guidance in [Build Philosophy](../Strategy/Build-Philosophy.md) or a dedicated item strategy page.

---

## Repairs

Equipment can take damage when ships die. At **0% Durability**, an item cannot be equipped until repaired.

Known repair paths:

| Repair path | Notes |
|-------------|-------|
| Item inspect -> **Upgrade** -> **Repair** | Repairs the item but can reduce item quality. |
| `:corp repair mytp confirm` | Repairs 5 random equipped items by 10% for every online corporation member, at an approximate cost of 1.5 Tech Points per item. |
| `:alliance repair mytp confirm` | Repairs 2 random equipped items by 10% for every online alliance member, at an approximate cost of 1.5 Tech Points per item. |

---

## See Also

* [Items](index.md)
* [Item Management](Item-Management.md)
* [Equipment Slots](Equipment-Slots.md)
* [Equip Points](../Ships/Equip-Points.md)
* [Tech Points](../Entities/Currencies/Tech Points.md)
* [Void Items](Void-Items.md)
