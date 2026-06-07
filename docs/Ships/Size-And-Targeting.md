# Ship and Defense Unit Size

Every combat entity has a **size**: Small, Medium, Large, Huge, or Massive. Size affects movement speed, evasion, and **weapon targeting speed**. See the [Ships](index.md) page for fleet size and captain level requirements.

Shared combat rules such as target locks, attack readiness, and hostile ability gates live on [Combat and Targeting](../Gameplay/Combat-and-Targeting.md).

## Targeting

Before weapons can fire, a **target lock** must be acquired. **The greater the size difference**, the longer it takes for a large ship to lock onto a small one. Big ships are meant to fight other bigs and have trouble targeting shuttles and frigates.

* **Small ships** -- Can't carry as much, but are **much more evasive**. Use small ships to target other small ships and leave big guns for big targets.
* [**Defense units**](../Entities/Structures/index.md) (Planets, Garrisons, etc.) -- **No targeting limit**; they target nearly instantly. Very slow weapons on defenses get an attack speed bonus.
* [**Fighter drones**](../Items/Drones.md) -- **Ignore size disparity**, so Carriers are strong against small targets.

Targeting speed bonuses reduce lock time, but lock time cannot go below the game's minimum lock-time floor.

## Movement Warm-Up

Ship size sets **pre-move "warm up"** time (the pre-jump animation):

| Size | Warm-up |
|------|---------|
| Small | 0.7 s |
| Medium | 1.0 s |
| Large | 1.3 s |
| Huge / Massive | 1.7 s |

The **Skip Drive Engine** and **Gravity Drives** (crafted engine) reduce this to **0.5 s** for any ship.

---

## Minimum Move Times

Ships also have hard minimum move times by size:

| Size | Minimum move time |
|------|-------------------|
| Small | 3.0 s |
| Medium | 3.2 s |
| Large | 3.3 s |
| Huge / Massive | 3.5 s |

These minimums correspond to about **-65% move speed** for each size. Extra move speed above the minimum can still matter because it helps counter enemy [Interdictor](Interdictor-Carrier.md) movement penalties.

See [Carrier Leadership](Carrier-Leadership.md) for how Carrier-led fleets use move speed.

---

## See Also

* [Ships](index.md) -- Fleet size and captain levels
* [Combat and Targeting](../Gameplay/Combat-and-Targeting.md) -- Target locks and attack readiness
* [Carrier Leadership](Carrier-Leadership.md) -- Fleet movement with Carriers
* [Small Strike Team Bonus](../Gameplay/Abilities/Small-Strike-Team-Bonus.md) -- 33% small/medium = fleet bonus
* [Structures](../Entities/Structures/index.md) -- Defense unit targeting
* [Drones](../Items/Drones.md) -- Fighter drones
