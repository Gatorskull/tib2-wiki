# Weapons

**Weapons** are one of the nine [**item types**](index.md) in *The Infinite Black 2*. They are the primary source of damage for ships and [defense units](../Entities/Structures/index.md). Weapons, along with Armor, Shields, and Storage, have a **Rank** that modifies their power and [**Equip Point**](../Ships/Equip-Points.md) cost; you can change rank (and other stats) via the **UPGRADE** button on the item inspect panel.

Shared targeting, attack-readiness, and hostile-action rules live on [Combat and Targeting](../Gameplay/Combat-and-Targeting.md).

---

## How Weapons Work

- **Damage** -- Weapon damage is modified by [**stats**](Stats.md) such as **Outgoing Damage Bonus**, which affects all damage (weapons, drones, battle ram, etc.). See [Stats](Stats.md) for the full list.
- **Targeting** -- Before a weapon can fire, the ship must **acquire a target lock**. [**Ship size**](../Ships/Size-And-Targeting.md) affects targeting speed: large ships target small ships more slowly. [**Targeting Speed**](Stats.md) stat modifies lock-on speed.
- **Battery** -- Most weapons consume **battery** to fire; Battery and Engine items affect capacity and recharge.
- **Defense units** -- Weapons and [fighter drones](Drones.md) on [structures](../Entities/Structures/index.md) attack **faster** than their listed speed; **slower weapons get a bigger bonus**. Defenses also ignore size-based targeting limits and target nearly instantly.
- **Attack requirement** -- A ship needs at least one weapon or fighter drone to make normal attacks.

## Attack Readiness

Weapons and fighter drones both use target-lock timing and their own cooldown timing. When choosing the next attack item, the game compares each ready weapon or fighter drone and uses the candidate with the lowest remaining effective wait.

Disabled weapon slots are ignored. Clearing a target resets weapon and drone lock timers that have not already locked.

---

## Weapon Slots and Fleet

Ships have multiple **weapon slots**. [**Elite Ranks**](../Ships/Elite-Ranks.md) on the Striker Gunboat add more slots (e.g. Elite Rank 3 adds +1 Weapon Slot, Elite Rank 4 adds another). Equip Points limit how many high-rank weapons you can fit; see [Equip Points](../Ships/Equip-Points.md) and [Stats](Stats.md).

---

## Related Item Types

- **Fighter Drones** -- Behave like weapons that don't consume battery; they **ignore** [size disparity](../Ships/Size-And-Targeting.md), so large ships can use them effectively against small targets. See [Drones](Drones.md).
- **Armor / Shield** -- Defensive items; see [Stats](Stats.md) for Hull, Shield, and resist stats.
- **Item Crafting** -- One of the six crafting categories is **Weapons**; see [Item Crafting](Item-Crafting.md).

---

## See Also

* [Items](index.md) -- All 9 item types and Gear Score
* [Drones](Drones.md) -- Fighter, Repair, and Harvester drones
* [Combat and Targeting](../Gameplay/Combat-and-Targeting.md) -- Target locks and attack readiness
* [Stats](Stats.md) -- Outgoing Damage, Targeting Speed, and all other stats
* [Size and Targeting](../Ships/Size-And-Targeting.md) -- How size affects weapon targeting
* [Structures](../Entities/Structures/index.md) -- How weapons behave on defense units
* [Elite Ranks](../Ships/Elite-Ranks.md) -- Extra weapon slots on Striker Gunboat
