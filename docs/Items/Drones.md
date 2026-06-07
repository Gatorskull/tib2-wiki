# Drones

**Drones** are equipment items that perform automatic ship actions. They come in three roles: **Fighter**, **Repair**, and **Harvester**.

Shared target-lock and attack-readiness rules live on [Combat and Targeting](../Gameplay/Combat-and-Targeting.md).

## Drone Roles

| Role | Main action | Notes |
|------|-------------|-------|
| **Fighter** | Attacks enemies. | Counts with weapons for normal attacks, does not consume battery, and ignores size disparity when targeting. |
| **Repair** | Repairs hull over time. | Can benefit from some repair technology, but does not behave exactly like the manual Repair ability. |
| **Harvester** | Harvests asteroids and debris. | Used for resource gathering and farming. |

For weapons, drones, and batteries, the first slot gives full item stats while auxiliary slots give reduced stats. A drone's main action still works at full strength in an auxiliary slot; only its normal item stats are reduced. See [Equipment Slots](Equipment-Slots.md).

## Factions and Crafting

Drone crafting categories combine [faction](../World/Factions/index.md) and role, such as **Pirate Fighter Drones**, **Het Repair Drones**, or **Precursor Harvest Drones**.

## Fighter Drones

Fighter drones behave like battery-free weapons:

- A ship needs at least one weapon or fighter drone to make normal attacks.
- Fighter drones are considered alongside weapons when the game chooses the next attack item.
- Fighter drones use target-lock timing and their own cooldown timing.
- Fighter drones ignore [size disparity](../Ships/Size-And-Targeting.md), which helps large ships hit small targets.

Fighter drone attack timing improves with rarity:

| Rarity step | Attack interval |
|-------------|-----------------|
| Common | 14.0 s |
| Each rarity above Common | 0.5 s faster |

Exact displayed fighter drone damage depends on rarity, faction, quality, and other modifiers.

## Repair Drones

Repair drones automatically repair hull:

- Repair drones still repair at full strength from auxiliary slots.
- Repair drones with [Technician](../Gameplay/Abilities/Technician.md) can remove negative effects.
- Repair drones cannot splash repair or apply repair-over-time.

Repair drone timing improves with rarity:

| Rarity step | Repair interval |
|-------------|-----------------|
| Common | 26.0 s |
| Each rarity above Common | 1.0 s faster |

Exact displayed repair amount depends on rarity, faction, quality, and other modifiers.

## Harvester Drones

Harvester drones gather resources from asteroids and debris. Harvest selection only considers Harvester drones and uses the Harvester with the lowest remaining harvest cooldown.

Base harvest timing improves with rarity:

| Rarity step | Base harvest interval before faction modifier |
|-------------|-----------------------------------------------|
| Common | 60.0 s |
| Each rarity above Common | 5.0 s faster |

Faction changes harvest timing and resource amount:

| Faction | Harvest interval modifier | Resources per harvest action |
|---------|---------------------------|------------------------------|
| Pirate | 100% | 2 |
| Het | 110% | 3 |
| Wyrd | 120% | 4 |
| Human | 130% | 2 |
| Precursor | 140% | 5 |

Higher resource amount can come with slower harvest timing. Other harvesting bonuses, such as [Freighter](../Ships/Ship-Mods.md), Prospector, or Drone Master, may change practical results.

## Equip Point Cost

Drone Equip Point cost depends on role, faction, and rarity.

Role modifier:

| Role | Modifier |
|------|----------|
| Harvester | +0 |
| Repair | +1 |
| Fighter | +2 |

Faction and rarity use the role modifier as the starting point:

| Faction | Common-Uncommon | Rare-Ultra-Rare | Elite-Legendary | Ultimate |
|---------|-------|-------|-------|----|
| Pirate | 1 + modifier | modifier | modifier - 1 | modifier - 2 |
| Het | 2 + modifier | 1 + modifier | modifier | modifier - 1 |
| Wyrd | 3 + modifier | 2 + modifier | 1 + modifier | modifier |
| Precursor | 4 + modifier | 3 + modifier | 2 + modifier | 1 + modifier |
| Human | modifier | modifier | modifier, except Legendary is modifier - 1 | modifier - 2 |

Drone EP cost cannot go below 0.

## Drone Master

[Drone Master](Specials.md) improves drone performance and can add drone-slot utility at high rarity:

| Drone Master rarity | Attack Drones tech | Repair Drones tech |
|---------------------|--------------------|--------------------|
| Common-Ultra-Rare | Rank 1 | Rank 1 |
| Elite | Rank 2 | Rank 2 |
| Legendary | Rank 3 | Rank 3 |
| Ultimate | Rank 4 | Rank 4 |

At Ultimate rarity, Drone Master can also add **+1 Drone Equipment Item Slot**.

## Needs Data

- Full displayed damage tables for Fighter drones.
- Full displayed repair tables for Repair drones.
- Exact stacking rules between Drone Master, Prospector, Freighter, and other harvesting modifiers.
- Full drone class/name list by faction and version.

## See Also

* [Items](index.md)
* [Equipment Slots](Equipment-Slots.md)
* [Weapons](Weapons.md)
* [Combat and Targeting](../Gameplay/Combat-and-Targeting.md)
* [Special Items](Specials.md)
* [Open World Farming](<../Gameplay/Activities/Player vs Environment (PVE)/Open World Farming.md>)
* [Size and Targeting](../Ships/Size-And-Targeting.md)
