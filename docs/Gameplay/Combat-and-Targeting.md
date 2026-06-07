# Combat and Targeting

Combat actions are built around target rules, target locks, item readiness, ability gates, and protection checks. This page covers the shared rules; item-specific details stay on [Weapons](../Items/Weapons.md), [Drones](../Items/Drones.md), and [Abilities](Abilities/index.md).

## Target Locks

Before weapons or Fighter drones can fire, the ship must acquire a **target lock**.

| Factor | Effect |
|--------|--------|
| Size difference | Large ships take longer to lock small targets. |
| Targeting Speed | Reduces lock time for weapons and drones. |
| Interdictor penalties | Can increase movement and targeting time in affected sectors. |
| Minimum lock time | Lock time cannot go below the game's minimum lock-time floor. |

[Defense units](../Entities/Structures/index.md) ignore most size-based targeting limits and target nearly instantly.

## Size and Targeting

Every combat entity has a size: **Small**, **Medium**, **Large**, **Huge**, or **Massive**. Size affects movement, evasion, and targeting.

Small ships are harder for large ships to lock. [Fighter drones](../Items/Drones.md) ignore size disparity, which makes them useful for large ships that need to hit small targets.

For size tables, movement warm-up, and minimum move times, see [Size and Targeting](../Ships/Size-And-Targeting.md).

## Attack Requirements

A ship needs at least one **Weapon** or **Fighter Drone** to make normal attacks.

Targets with a non-enemy relation cannot be attacked. Protected targets cannot be attacked unless the attacker has a valid protection bypass state.

## Attack Readiness

Weapons and Fighter drones both use target-lock timing and cooldown timing.

When choosing the next attack item, the game compares each ready weapon or Fighter drone and uses the candidate with the lowest remaining effective wait. Disabled weapon slots are ignored. Clearing a target resets weapon and drone lock timers that have not already locked.

For drone-specific timing, see [Drones](../Items/Drones.md). For weapon-slot and item behavior, see [Weapons](../Items/Weapons.md).

## Hostile Abilities

Some abilities are hostile actions and require a target in the same sector.

| Ability | Target required | Hostile | Battery |
|---------|-----------------|---------|---------|
| Grapple | Yes | Yes | Costs battery |
| Hack | Yes | Yes | Costs battery |
| Drain | Yes | Yes | No battery cost |
| Strike | Varies by source | Yes | No battery cost |
| Purge | Yes | No | No battery cost |
| Repair | Yes | No | No battery cost |

Grapple, Hack, and Drain require **10+** of the matching stat to use and have a default **50 s** cooldown. See [Abilities](Abilities/index.md) for ability-specific effects and technology lines.

## Ability Gates

Common ability checks include:

- The ship must be allowed to use the ability in its current context.
- The ability must not be on cooldown.
- The ship must have enough battery for abilities with a battery cost.
- Target-required abilities require a target in the same sector.
- Target-required abilities cannot target destroyed entities.
- Hostile abilities require a hostile target and respect protection rules.
- Repair requires the target to be below maximum hull.
- Purge requires the target to have a removable negative status.

If a ship is hacked, hackable abilities may show the hacked timer instead of the normal cooldown timer.

## Defense Unit Attacks

Defense units can only be attacked by players in an alliance. Defense-unit attacks also require the attacking ship to meet the required Gear Score and respect any attack-protection timer.

For structure warfare rewards and PvP context, see [Structure Warfare Rules](<Activities/Player vs Player (PVP)/Structure Busts.md>) and [Skulls](../Entities/Currencies/Skulls.md).

## Arena Restrictions

Arena rules can block certain actions or gear states:

- The ship must have at least one Weapon or Fighter Drone.
- Free starter items cannot be used.
- Strike is not usable in Arena.
- Some Arena modes or daily modifiers add extra restrictions.

See [Arena](<Activities/Player vs Player (PVP)/Arena.md>) for the full Arena rule page.

## See Also

* [Weapons](../Items/Weapons.md)
* [Drones](../Items/Drones.md)
* [Abilities](Abilities/index.md)
* [Size and Targeting](../Ships/Size-And-Targeting.md)
* [Interdictor Carrier](../Ships/Interdictor-Carrier.md)
* [Player vs Player](<Activities/Player vs Player (PVP)/index.md>)
