# Hacking Ability

With **10+ Hack Chance**, a [ship](../../Ships/index.md) can use the **Hack** hotbar action. Hack requires a target in the same sector, is a hostile action, has a default **50 s** cooldown, and costs battery to use. Hacked targets:

* **Cannot use** any hotbar ability **except Repair**
* **Battery does not regenerate**
* **Special movement** (engines, Space Lanes) does not work

## How It Works

* **Hack Chance** increases the Hack effect.
* **Hack Resist** reduces the Hack effect.
* For player ships, **Hit Chance** can contribute to Hack power and **Evasion** can contribute to Hack resistance.
* If the final effect is too weak, the Hack can be resisted.

Exact duration and resist formulas are **Needs data** until the live behavior is confirmed.

## Technology Effects

| Technology | Effect |
|------------|--------|
| **Advanced Hacking** | Adds Hack duration. |
| **Advanced Hacking II** | Adds more Hack duration. |
| **Advanced Hacking III** | Adds the highest Hack duration bonus and makes hacked targets lose Special Item abilities. |
| **Hack Speed** | Reduces Hack cooldown by 4 s. |
| **Hack Speed II** | Reduces Hack cooldown by 6 s. |
| **Hack Speed III** | Reduces Hack cooldown by 8 s. |
| **Reverse Hacking** | Gives a high chance to deflect Hack back at attackers. |

Advanced Hacking III can disable Special Item effects such as Nova and Deflector. It also interacts with [Technician](Technician.md) repair-over-time immunity.

---

## See Also

* [Grapple](Grapple.md) | [Drain](Drain.md) | [Technician](Technician.md) | [Taunt](Taunt.md) | [Deflector](Deflector.md) | [Junker](Junker.md)
* [Stats](../../Items/Stats.md) -- Hack Chance / Resist
* [Abilities](index.md)
