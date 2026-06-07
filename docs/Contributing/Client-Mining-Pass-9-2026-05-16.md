# Client Mining Pass 9 - Crafting, Engineering, Ship Mods, Slots

Date: 2026-05-16

Scope: Current Steam client decompile under `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled\Assembly-CSharp`.

This note covers five more extraction areas after `Client-Mining-Pass-8-2026-05-16.md`:

29. Item crafting validation
30. Ship construction validation
31. Item engineering validation
32. Ship mod removal validation
33. Ship slot and Equip Point formulas

Public wiki rule: keep these as mechanics/reference material. Strategy pages may link to these rules, but the public rule pages should not include build advice or fleet advice.

## 29. Item Crafting Validation

Useful source file:

- `IKOLEGFOADL.cs`

`IKOLEGFOADL.CanCraftItem(...)` validates item crafting. The decompiler name appears as `__BB_OBFUSCATOR_30(...)`, but the body is clearly the item crafting gate.

Stable behavior:

- The item class must be valid.
- The class byte and variant byte must be valid for that item class.
- The item class determines which crafting skill is used.
- The client calculates current crafting cooldown hours for that skill.
- Resource requirements are calculated per resource type with `GetCraftResourceRequirement(...)`.
- The player must have the matching item plan/blueprint unlocked.
- If cooldown enforcement is enabled for the request, remaining cooldown blocks crafting.
- Missing crafting resources block crafting.

Public use:

- Crafting pages can describe item crafting as: valid blueprint, unlocked plan, enough resources, and no active cooldown for that craft skill.
- Avoid copying resource tables into multiple places. Link to a dedicated crafting/resources table once extracted.

Needs confirmation:

- Exact player-facing cooldown formatting. The decompiled string around the cooldown message is partially corrupted.
- Whether all crafting actions enforce cooldown, or whether some UI calls use the flag to preview requirements without blocking.

## 30. Ship Construction Validation

Useful source file:

- `IKOLEGFOADL.cs`

`IKOLEGFOADL.CanCraftShip(...)` validates ship construction.

Stable behavior:

- Ship class cannot be `NULL`.
- Ship faction cannot be `NULL`.
- Some ships/factions require a minimum number of days in a corporation.
- If corp-tenure days are required, the player's current corp membership duration must meet the requirement.
- Ship construction may require relics.
- Pirate construction uses Human relics for the relic-bank check.
- The relic requirement is calculated from the ship class and whether the construction faction is Human.
- A full ship garage blocks construction.
- Construction resource requirements are calculated per resource type with `GetCraftResourceRequirement(...)`.
- The acting ship must pass the shared ship validator.
- Some ships/factions require Skulls.
- If the player has fewer Skulls than required, construction is blocked and a skull-cost flag is set for the caller.
- Construction requires an eligible friendly defense unit in the current sector, or an eligible corporation-owned shipyard.
- Non-human shipyards are ignored unless owned by the player's corporation.
- If no eligible builder is found, the client reports either a friendly-defense-unit requirement or the required Shipyard level/faction.
- Missing construction resources block construction.

Public use:

- Ship construction should be documented as a gate stack: class/faction validity, corp tenure, relics, garage space, resources, acting ship state, skulls, and local builder/shipyard access.
- Do not repeat per-ship requirements on every ship page unless they are generated from extracted data. Prefer one construction table and link to it.

Needs confirmation:

- Exact public names for the defense-unit types that count as eligible builders.
- Whether server-side validation adds further requirements not visible in this client method.

## 31. Item Engineering Validation

Useful source file:

- `IKOLEGFOADL.cs`

`IKOLEGFOADL.CanEngineerItem(...)` validates modifying, repairing, ranking, and upgrading equipment.

Stable behavior:

- Null items are blocked.
- Items listed for sale must have the sale canceled first.
- Items currently in trade cannot be modified.
- Items with a temporary rarity upgrade cannot be modified.
- Equipped items cannot be modified while the owning entity is in the Arena queue.
- Equipped items cannot be modified while the owning entity is in Arena.
- Low-level/ownership checks restrict repair and rank actions to the player's own equipment.
- Ranking up an equipped item is blocked if the new Equip Point usage would exceed the entity's total Equip Points.
- Upgrading an equipped item is blocked if the upgraded item would require a higher entity level than the equipped entity has.
- The item then delegates to `CanApplyUpgrade(...)` for action-specific rules.

Void-item relic behavior:

- Some upgrade actions require relics.
- The relic faction comes from the item upgrade data.
- If the player lacks enough relics in the item crafting bank, the upgrade is blocked.
- The error text tells players to use relic items to add them to the item crafting bank.

Public use:

- Engineering documentation can now separate universal modification gates from action-specific item rules.
- Equip Point overflow and upgraded level requirements should be mentioned on item upgrade/rank pages because they explain why equipped gear sometimes has to be unequipped first.

Needs confirmation:

- Exact action list covered by the obfuscated enum `EICLLIOOFLD`.
- Full per-action Tech Point/resource cost formulas should come from `CanApplyUpgrade(...)` and related item classes, not this wrapper alone.

## 32. Ship Mod Removal Validation

Useful source file:

- `IKOLEGFOADL.cs`

`IKOLEGFOADL.CanRemoveShipMod(...)` validates removing several ship modification categories.

Stable behavior:

- The ship must pass the shared owned-ship validator.
- The ship must pass the shared entity-modification validator.
- The ship must be recalled before removing a mod.
- Retro-skin removal requires the current mod to be a retro skin.
- Technology-mod removal is blocked for unique ships.
- Technology-mod removal requires the current ship mod to be a technology mod.
- Bonus-stat removal requires the ship to have a bonus stat.
- Hardcore removal requires the ship to be hardcore.
- Invalid removal requests are blocked.
- Removal costs Tech Points.
- Retro-skin removal uses a different Tech Point cost constant than the other removal types.
- If the player lacks enough Tech Points, removal is blocked.

Public use:

- Ship-mod pages should document removal as a separate mechanic, not as generic engineering.
- The public page should avoid saying all ship mods are removable. Unique technology mods and invalid category combinations are explicitly blocked.

Needs confirmation:

- Exact Tech Point costs behind `JEKJDKMBIGN.HAEEHICBPFE` and `JEKJDKMBIGN.HJBBGOBKOOM`.
- Public label for the hardcore-removal branch.

## 33. Ship Slot and Equip Point Formulas

Useful source file:

- `CHCIGDNAAPI.cs`

### Equip Points

`CHCIGDNAAPI.CalculateEquipPoints()` calculates a ship's total Equip Points.

Stable behavior:

- A special internal flag forces total Equip Points to 50.
- Base Equip Points come from ship class and faction.
- Hardcore ships gain +3 Equip Points.
- Striker Gunboats use a special formula: base plus `2 + elite rank * 3`.
- A further Striker flag adds +3 more Equip Points.
- Non-Striker ships gain +1 Equip Point per elite rank.
- Bonus Equip Points from ship mods are added.
- If the ship's bonus stat is `EquipPointMax`, that bonus-stat value is added.

Public use:

- Ship pages can now avoid vague "elite rank gives EP" language. Non-Striker and Striker EP growth are different.
- Do not mix this into build advice. Strategy pages can link back to the Equip Point rule.

Needs confirmation:

- Public name for the extra Striker flag that grants +3 Equip Points.
- Which special/internal ships use the forced 50 Equip Point branch.

### Drone slots

`CHCIGDNAAPI.CalculateDroneSlots()` calculates max drone slots.

Stable behavior:

- Base drone slots come from ship class and faction.
- Bonus drone slots from ship mods are added.
- Striker Gunboats gain +1 extra drone slot at elite rank 4.
- Striker Gunboats gain +2 extra drone slots at elite rank 5.

### Battery slots

`CHCIGDNAAPI.GetBaseMaxBatterySlots()` calculates max battery slots.

Stable behavior:

- A special internal flag forces max battery slots to 1.
- Otherwise battery slots come from `CalculateBatterySlots()`.
- Battery slots are capped at 6.

Needs confirmation:

- The underlying `CalculateBatterySlots()` formula should be extracted before publishing a full battery-slot table.

## Obfuscated Junk To Avoid Promoting

Several adjacent methods contain obviously corrupt/decompiler-poisoned strings such as unrelated achievement text inside validators. Do not treat those strings as rules unless the surrounding code and call sites make sense.

Examples seen in this pass:

- `IKOLEGFOADL.__BB_OBFUSCATOR_37(...)` contains mixed strings such as Wyrd kills, screenshot text, and targeting penalties.
- Some item crafting error strings are partially overwritten by unrelated strings.

Contributor guidance:

- Trust stable boolean checks, enum comparisons, resource calculations, and method calls more than isolated decompiled string literals.
- When a string looks nonsensical, record the gate as `Needs confirmation` instead of publishing the text.
