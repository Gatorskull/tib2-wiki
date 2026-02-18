# Sectors

Each solar system (map) is a **15×15 grid** of **sectors**. You move from sector to sector by clicking adjacent squares; you cannot wrap around the edge — use a [**Jump Gate**](/Entities/Structures/Jump%20Gates.md) to leave the system.

* **Coordinates:** From **(0,0)** at the bottom-left to **(14,14)** at the top-right.
* **Contents:** Enemies, asteroids, other players, and [**structures**](/Entities/Structures/index.md) (e.g. corp defenses, jump gates).

## Collision (Stacking Limit)

Too many ships in one sector causes a **Collision** mechanic (damage over time) to reduce lag. Collision triggers when:

| Condition | Limit |
|-----------|--------|
| **Total ships** in the sector | More than 225 |
| **Ships per alliance** in the sector | More than 75 |
| **Enemies attacking a defense unit** | More than 75 (any alliance) |

See [PvP](/Gameplay/Activities/Player%20vs%20Player%20(PVP)/index.md) for context on alliance stacking and structure defense.

---

## See Also

* [Maps](index.md) — Solar systems and the Starmap
* [World](/World/index.md) — Navigation overview
* [Jump Gates](/Entities/Structures/Jump%20Gates.md)
