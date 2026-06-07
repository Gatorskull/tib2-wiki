# The Arena

**The Arena** is a controlled PvP environment with balanced teams, no Artifacts, and no [Corporation Skills](../../Skills.md). Arena matches award [**Skulls**](../../../Entities/Currencies/Skulls.md) and other rewards.

## How It Works

* **Schedule** -- Rounds run **every few hours at the top of the hour**. Registration opens before each round.
* **Access** -- **Captain Panel -> ARENA** when registration is announced.
* **Objective** -- The team with the **most kills** wins. Captains who lose but have high kill counts still get **bonus rewards**.
* **No durability loss** -- Your ships don't lose durability on death in The Arena. Gear loses only **1% durability**, and only **half the time**.

## Queue Rules

Arena queue validation checks the selected ship before it can enter a round.

| Requirement                | Rule                                                                                                                                                                   |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ship state**             | Destroyed ships, NPC ships, Corp Defenders, ships listed for sale, and ships listed for trade cannot join.                                                             |
| **Arena type**             | Skirmish Arena requires a Skirmisher ship. Skirmisher ships cannot join non-Skirmish rounds.                                                                           |
| **Hardcore type**          | Hardcore rounds require Hardcore ships. Non-Hardcore rounds reject Hardcore ships.                                                                                     |
| **Gear**                   | The ship must have at least one Weapon or Fighter Drone equipped and cannot use free starter items.                                                                    |
| **Rarity**                 | Basic-rarity gear is blocked, excluding Specials and Engines.                                                                                                          |
| **Empty slots**            | Ships with enough captain level for the gear check can have at most one empty accessible gear slot.                                                                    |
| **Hardcore artifact rule** | Hardcore Arena blocks Weird Alien Artifacts.                                                                                                                           |
| **Gear Score**             | At least **1,000 [Gear Score](../../../Items/index.md)** is required to queue. Full-reward thresholds may be higher and should be checked on the in-game Arena screen. |
| **Level requirement**      | If the selected ship has a required player level, the captain must meet it.                                                                                            |

Daily Arena events can add extra queue restrictions, such as blocking Huge and Massive ships.

For shared target, attack, and ability gates, see [Combat and Targeting](../../Combat-and-Targeting.md).

!!! note "Needs confirmation"
    Reward values and damage participation thresholds below remain community values unless confirmed by the in-game Arena screen.

## Modes And Modifiers

| Type | Notes |
|------|---------------------|
| **Standard** | Bring up to 3 ships; following teammates is not allowed. |
| **Fleet** | Bring up to 4 ships; following teammates is allowed. |
| **Hardcore** | Bring up to 3 Hardcore ships; following teammates is not allowed; gives extra Skulls. |
| **Chaos** | Modifier with smaller/more teams and item rewards weighted toward individual kill count. |
| **Ultimate** | Modifier where gear becomes Ultimate rarity for the duration of the Arena. |

## Observed reward notes

Community notes give these observed reward values:

| Result or bonus                                | Skulls                                       |
| ---------------------------------------------- | -------------------------------------------- |
| Losing team                                    | 7                                            |
| Winning team                                   | 15                                           |
| Hardcore Arena                                 | +2                                           |
| Chaos Arena                                    | +2                                           |
| Arena Awards Bonus Loot and Skulls daily event | +2 and an additional item reward for winning |
| Last team standing                             | +3                                           |
| Underdog team                                  | +3                                           |
| Team MVP category                              | +4, with +1 for each additional MVP category |

Players on a losing team can still earn bonus rewards for strong performance, such as high kill count, top healing, or utility.

!!! note "Needs confirmation"
    Arena reward values and thresholds can change. Check the in-game Arena screen when exact rewards matter.

## Arena Rewards Summary

Arena can award Skulls, items, and performance bonuses. Exact reward values can change, so check the in-game Arena screen when the exact payout matters.

## Player Quick Starts

* [Arena Quick Start](../../../Getting-Started/Quick-Start-Guides/Arena-Quick-Start.md) -- cattabliss' practical entry guide.
* [Lucky's Arena Notes](../../../Getting-Started/Quick-Start-Guides/Lucky-Arena-Notes.md) -- community Arena notes.

---

## See Also

* [Skulls](../../../Entities/Currencies/Skulls.md) -- What Arena Skulls are spent on
* [Player vs Player](index.md) -- Open-world PvP and structure warfare
* [Ships](../../../Ships/index.md) -- Fleet and Gear Score
* [Items](../../../Items/index.md) -- Gear Score and equipment
* [Combat and Targeting](../../Combat-and-Targeting.md) -- Target locks, attack readiness, and hostile ability gates
