# Client Mining Pass 2 - 2026-05-16

Hidden contributor staging page for the second broad client-mining sweep. This pass follows the "what else is extractable?" list and records what the current 2.1.0 Steam client can safely tell us. Public pages should use only the stable rule findings, and should keep rules separate from strategy.

## Source Scope

Primary decompile root:

- `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled\Assembly-CSharp`

Key files inspected in this pass:

- `NCJPKNGDBKM.cs`, `HBCLPLAMOJI.cs`, `AKAPMGBHNAJ.cs`, `FCOMFIGBBGF.cs`
- `CHCIGDNAAPI.cs`, `LJBBNJFKIEJ.cs`, `MNKGMIHIEBJ.cs`
- `DDEIFGPEOMI.cs`, `PPKFDLLBBOP.cs`, `UiManager.cs`, `AbilityHotbarButton.cs`
- `BCHEAEJKAJI.cs`, `DFHOJHHBAMJ.cs`, `JEKJDKMBIGN.cs`
- `AHFAPFNMNPJ.cs`

## 1. Map and System Database

The client exposes the map object shape and map classification rules, but the complete system list appears to be populated from map template data rather than a clean static table in the inspected C# files.

Client-visible map type enum:

| Enum | Meaning |
|---|---|
| `Default` | Normal map/system |
| `AshHub` | Ash hub map |
| `HumanHome` | Human home map |
| `Arena` | Arena map |

Client-visible security/contest enum:

| Enum | Meaning |
|---|---|
| `Protected` | Non-contested map display |
| `Contested` | PvP/contested map display |

Stable extracted behavior:

- Normal and Arena maps are split by `NCJPKNGDBKM.GetAllNormalMaps()` and `GetAllArenaMaps()`.
- Arena maps use the map template name as their display name.
- Non-Arena maps append `System` in the `NBMMPACPPDD` display helper.
- Map security display is `SR#` for non-contested maps and `SR# PvP` for contested maps.
- The client has a direct center-sector helper returning `GetSector(7, 7)`.
- Linked maps are exposed through the map template `PHNGJOPAMOE` array.
- Gate sectors are active sectors where the gate flag is set.
- Artifact eligibility is partly client-visible, but not enough to publish as a complete rule:
  - Map type must be `Default`.
  - A protected/home-like flag blocks artifacts.
  - One branch requires `R8+`.
  - Another branch allows maps below `R7`.

Needs data:

- Full system names, coordinates, links, sector layout, and faction control are not yet available as a clean table from these C# files.
- Need to inspect serialized resources or runtime network/template payloads if we want the complete map database.
- Artifact spawning/harvesting rules need server confirmation before public use.

## 2. Ship Blueprint Matrix

Already staged in [Client-Extracted Ships](Client-Extracted-Ships.md).

Additional confirmation from this pass:

- Arena validation reads ship size directly from `CHCIGDNAAPI.HEILBGFBJLK`.
- The daily arena event gate can reject `Huge` and `Massive` ships.
- Skirmisher ships are only valid for Skirmish Arena, and Skirmish Arena requires a Skirmisher ship.

Needs data:

- Full ship blueprint purchase/source tables are still not complete from this pass.
- Public ship pages should keep using the current extracted size, EP, slot, mod, and unique-ship data already staged.

## 3. Defense Unit Mechanics

Already staged in [Client-Extracted Structures](Client-Extracted-Structures.md).

Additional confirmation from this pass:

- Attacking an active powerful defense unit triggers a client warning: `Defense Unit Engagement`.
- The warning text says the engagement is dangerous and can kill the player.
- Repair Facility tech source depends on nearby friendly structure type:
  - Shipyard: `RepairFacility4`
  - Planet: `RepairFacility3`
  - Garrison: `RepairFacility2`
  - Outpost: `RepairFacility1`

Needs data:

- Defense unit AI, aggro, target selection, and exact engagement behavior still need deeper extraction or server confirmation.

## 4. Skill and Stat Formulas

New lock-time formula found in `DDEIFGPEOMI.GetLockTimeMS(...)`.

Formula shape:

```text
sizeDelta = attackerSizeOr1 - targetSize
baseTime = weaponOrFighterBaseLock + sizeDelta * sizeLockStep
modifiedTime = round(baseTime + baseTime * targetingSpeedPercent)
finalTime = max(modifiedTime, minimumLockTime)
```

Important details:

- Fighter-drone lock calculation uses attacker size as `1`.
- Weapon lock calculation uses attacker ship size capped at `4.5`.
- Targeting speed percent is applied as a time modifier.
- Final lock time is floored by a client config minimum.
- If the entity has the fast-lock flag, lock time returns the minimum directly.
- Weapon lock timers are staggered by weapon index and item lock modifier.
- Fighter drone lock timers are staggered separately.

Needs data:

- The actual server config values for weapon base lock, fighter base lock, size step, and minimum lock time were only exposed through config wrappers in this pass.
- Stat diminishing return formulas still live in broader stat aggregation code and should stay in the existing stat extraction pages until fully reviewed.

## 5. Technology Catalog

Already staged in [Client-Extracted Technology](Client-Extracted-Technology.md).

Additional confirmation from this pass:

- `BCHEAEJKAJI.cs` is the complete client technology enum.
- `DFHOJHHBAMJ.cs` contains display names, descriptions, `IsMajor`, `CanBeResearched`, daily-tech helpers, and dynamic daily-tech descriptions.
- The catalog includes technology families for repair facilities, evasion/hit chance, XP, targeting, harvesting, freighter, hacking/grappling/draining, hull/shield, leadership, interdictor, garrison strikes, reverse effects, deflector, technician, PvP, alien damage, drones, battle ram, scan/cloak, savior/rebirth, territory effects, daily tech, shield repair, and hack ram.

Contributor note:

- The display catalog is large enough that public pages should use topic pages by family instead of one giant unsorted dump.
- Prefer linking to a canonical technology page/family page from guides.

## 6. Item and Consumable Metadata

Already staged in [Client-Extracted Items](Client-Extracted-Items.md) and [Client-Extracted Loot Rewards](Client-Extracted-Loot-Rewards.md).

Additional confirmation from this pass:

- Arena rejects free starter items.
- Arena rejects Basic-rarity gear except Specials and Engines.
- Hardcore Arena rejects Weird Alien Artifact gear.
- The client UI can generate fake item previews with class, variant, rarity, quality, durability, EP rank, mutate seeds, and void seed.

Needs data:

- Do not publish generated preview examples as live loot tables without checking actual source/drop rules.

## 7. Crafting Systems

Already staged in [Client-Extracted Crafting](Client-Extracted-Crafting.md).

Additional confirmation from this pass:

- Achievement names expose additional craft families, including quality repair kits, nanobot charge kits, mutate kits by item slot, faction ultimate ship mods, and faction interdictor ship mods.
- Some craft achievement names are useful as a checklist of craftable categories, but not as recipes.

Needs data:

- Recipes, costs, unlock paths, and success/upgrading chances should remain in crafting extraction pages until each system is verified.

## 8. Arena Validation Rules

Source: `CHCIGDNAAPI.GetCanQueueForArena(...)`, `LJBBNJFKIEJ.cs`, `MNKGMIHIEBJ.cs`.

Client-visible Arena modes:

| Mode enum | Client behavior |
|---|---|
| `Standard` | Default Arena type |
| `Hardcore` | Hardcore-only ships |
| `Fleet` | Fleet Arena |
| `Skirmish` | Skirmisher-only ships |

Client queue validation rules:

- Skirmish Arena requires a Skirmisher ship.
- Skirmisher ships cannot queue for non-Skirmish Arena.
- The daily Arena event can block `Huge` and `Massive` ships.
- Destroyed ships cannot join.
- NPC ships cannot join.
- If player level is at least 20:
  - Accessible gear slots are checked.
  - At most one empty accessible gear slot is allowed.
  - Basic-rarity items are not allowed, excluding Specials and Engines.
- If player level is at least 40, Specials and Engines are included in the empty-slot check.
- Hardcore rounds require Hardcore ships.
- Non-Hardcore rounds reject Hardcore ships.
- Hardcore Arena rejects Weird Alien Artifacts.
- Free starter items cannot be used.
- At least one Weapon or Fighter Drone is required.
- A minimum Gear Score is required, but the number is config-driven in the inspected code.
- Corp Defenders cannot join.
- Ships listed for sale or trade cannot join.
- If the ship has a required player level, the player must meet it.

Client UI restrictions:

- The client says equipment cannot be modified while in the Arena queue.
- The client says the player cannot leave the Arena queue at some times.
- The client blocks Garrison Strike in The Arena.
- Arena combat cannot begin before the Arena state reaches `Running`.

Needs data:

- Current minimum Gear Score value should be read from live config or server data before hardcoding.
- Reward values and participation thresholds remain community/training-data unless separately confirmed.

## 9. Combat Lock and Targeting Mechanics

Source: `DDEIFGPEOMI.cs`, `PPKFDLLBBOP.cs`.

Stable extracted behavior:

- Changing sector clears grapple time.
- Moving between maps clears attack target.
- Setting attack target updates targeted-count tracking on the old and new targets.
- Clearing target resets weapon and fighter-drone lock timers unless the individual timer is marked locked.
- Arena attacks are blocked before combat begins.
- The client asks for confirmation before attacking a powerful defense unit unless the user already confirmed.
- Active ability cooldowns exist for Scan, Cloak, Repair, Drain, Grapple, Hack, Strike, and Purge.
- Purge has an 8 second base cooldown in the inspected client helper.
- Scan, Cloak, Repair, and the offensive status abilities use config-driven cooldowns.
- Repair cooldown is reduced by Repair Facility tech.
- Cloak cooldown is halved when the relevant entity flag is active.
- Hacked time can override cooldown readiness for hackable abilities.

Needs data:

- Exact base cooldown values for most abilities are config-backed and should not be hardcoded until config extraction is complete.

## 10. Achievements and Leaderboards

Source: `AHFAPFNMNPJ.cs`, `UiManager.cs`, `AbilityHotbarButton.cs`.

Extractable achievement families:

- Mission completion ladders: normal, Captain, Corp, Alliance, Universe, and tutorial missions.
- Arena ladders, including Hardcore Arena win achievements.
- Relic ladders by faction/type: Wyrd, Het, Human, Precursor.
- Alliance Point ladders.
- Deploy-ship ladders.
- Crafting achievements for kits, ship mods, mutate kits, and ship/item construction.
- Harvesting achievements by resource family and object size.
- Elite rank and Hardcore elite rank achievements.
- Named/title achievements such as `Archeologist`, `Artificer`, `No Impulse Control`, and `Oblivion`.

Needs data:

- The full achievement table is extractable, but too large to use raw in public navigation.
- Leaderboard data was not found as a clean client-side rule table in this pass.
- Public pages should add achievements only when tied to a relevant system page, or create a dedicated achievement catalog later.

## 11. Commands and UI Workflows

Source: `PPKFDLLBBOP.DoChat(...)`, `UiManager.TryChatCommandClick(...)`, `UiManager.cs`, `AbilityHotbarButton.cs`.

Stable extracted behavior:

- Chat messages are sanitized/prepared before sending.
- Client chat input is limited to 200 characters before send.
- Messages beginning with `:` are forced to Sector chat and sent as commands.
- Clickable chat command links use a `!COMD!` link marker and send the clicked command as `:<command>`.

Client-visible command/workflow examples:

- `:gift majorparty`
- `:gift minorparty`
- `:corp scrap mission`
- `:alliance scrap mission`

Needs data:

- The full command vocabulary appears server-authoritative and was not fully present client-side.
- Public command pages should distinguish "client-visible command examples" from confirmed complete command lists.

## 12. Error Messages as Rule Hints

Useful client strings found this pass:

| Area | Client string / rule hint |
|---|---|
| Arena | `Skirmish Arena requires a Skirmisher Ship!` |
| Arena | `Skirmisher Ships are only for Skirmish Arena!` |
| Arena | `Daily Arena Event: No HUGE or MASSIVE Ships!` |
| Arena | `Destroyed ships cannot join The Arena!` |
| Arena | `NPC ships cannot join The Arena!` |
| Arena | `Too many empty gear slots! (1 Max)` |
| Arena | `No BASIC RARITY items allowed!` |
| Arena | `This arena round is for Hardcore ships only!` |
| Arena | `This arena round is for Non-Hardcore ships only!` |
| Arena | `Weird Alien Artifact Not Allowed` |
| Arena | `Free starter items cannot be used in The Arena!` |
| Arena | `The Arena requires at least one Weapon or Fighter Drone!` |
| Arena | `Corp Defenders cannot join The Arena!` |
| Arena | `Cancel the ship sale first!` |
| Arena | `Cancel the ship trade first!` |
| Arena | `Arena combat has not begun!` |
| Arena | `Cannot Garrison Strike in The Arena!` |
| Arena | `You cannot modify equipment while in The Arena queue!` |
| Defense | `Defense Unit Engagement` warning before attacking powerful defense units |
| Unique ships | Unique custom ship mods cannot be removed or replaced |
| Items | New players cannot disable starting weapons |

Use these as rule-discovery leads, not polished wiki language.

## Recommended Public Follow-Up

- Update Arena rules with the stable queue validation list, but keep tactics in quick starts or strategy pages.
- Create a future `Achievements` catalog only if we want a player-facing checklist.
- Keep the full technology catalog hidden until split into family pages.
- Continue looking for serialized map/config data if a full map database is needed.
