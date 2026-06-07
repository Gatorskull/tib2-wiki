# Sectors

Each solar system (map) is a **15x15 grid** of **sectors**. You move from sector to sector by clicking adjacent squares; you cannot wrap around the edge -- use a [**Jump Gate**](../../Entities/Structures/Jump Gates.md) to leave the system.

* **Coordinates:** From **(0,0)** at the bottom-left to **(14,14)** at the top-right.
* **Contents:** Enemies, asteroids, other players, and [**structures**](../../Entities/Structures/index.md) (e.g. corp defenses, jump gates).

## Collision (Stacking Limit)

Too many ships in one sector causes a **Collision** mechanic (damage over time) to reduce lag. Collision triggers when:

| Condition | Limit |
|-----------|--------|
| **Total ships** in the sector | More than 225 |
| **Ships per alliance** in the sector | More than 75 |
| **Enemies attacking a defense unit** | More than 75 (any alliance) |

Turn on **Display local sector ship counts** in gameplay settings to see local ship counts. Observed count colors are friendly/allied ships in green, neutrals in yellow, PvP enemies in red, and NPCs in purple.

See [PvP](<../../Gameplay/Activities/Player vs Player (PVP)/index.md>) for context on alliance stacking and structure defense.

---

## Following Ships

Ships can follow another ship to move together. If the followed ship gets **3 or more sectors away**, the following ship immediately loses the follow and cannot refollow until it is close enough again.

---

## Movement timing

Ship size controls movement warm-up and minimum move time. See [Ship and Defense Unit Size](../../Ships/Size-And-Targeting.md) for the canonical size timing table.

Extra movement speed cannot push a ship below its size-based minimum move time, but it can still offset penalties such as enemy [Interdictor Carrier](../../Ships/Interdictor-Carrier.md) effects.

---

## See Also

* [Maps](index.md) -- Solar systems and the Starmap
* [World](../index.md) -- Navigation overview
* [Jump Gates](../../Entities/Structures/Jump Gates.md)
* [Ship and Defense Unit Size](../../Ships/Size-And-Targeting.md)
