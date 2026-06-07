# Client Mining Pass 4 - UI Hints, Achievements, Missions, Combat

Date: 2026-05-16

Scope: Current Steam client decompile under `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled\Assembly-CSharp`.

This note covers the next four mining targets after `Client-Mining-Pass-3-2026-05-16.md`:

5. UI and error strings as rule hints
6. Achievements and leaderboards
7. Missions, gifts, daily/event surfaces
8. Combat, abilities, status/targeting

Public wiki rule: treat UI/error strings as hints unless the surrounding code path also confirms the rule. Strings are excellent for finding game constraints, but some are old, fallback-only, or server-driven.

## 5. UI and Error Strings as Rule Hints

Useful source files:

- `AbilityHotbarButton.cs`
- `CHDFPJKNCOH.cs`
- `CHCIGDNAAPI.cs`
- `CorpInspectPanel.cs`
- `CorpButton.cs`
- `CELOHADEBLD.cs`

### Arena validation hints

The client has a dedicated arena validator in `CHCIGDNAAPI.cs`. Strings and code paths indicate these arena restrictions:

- Skirmish arena requires a Skirmisher ship.
- Destroyed ships cannot join the arena.
- NPC ships cannot join the arena.
- Corp Defenders cannot join the arena.
- Arena entry can require a minimum player level.
- Arena entry can require a minimum Gear Score.
- Arena entry requires at least one Weapon or Fighter Drone.
- Arena gear requirement says `UNCOMMON+ gear`; the string notes Specials and Engines are not included.
- Free starter items cannot be used in the arena.
- Some alien artifact / hardcore combinations are rejected by the validator.
- Equipment cannot be modified while in the arena queue.
- Garrison Strike cannot be used in the arena.
- Defense units cannot deploy in the arena.
- The Strike ability is blocked by the ability helper's `CanUseInArena` check.

Public page use: put these on an arena rules/reference page, not in an arena strategy page.

### Deployment and structure constraints

UI strings identify several deployment rules:

- Defense units cannot deploy in a Homeworld system. The string says Security Rating 8 and below only.
- Defense units cannot deploy on a jump gate.
- Deployment can be blocked by nearby enemy ships.
- Deployment can be blocked in enemy territory.
- Ship construction requires a friendly defense unit.
- Capturing artifacts requires a deployed friendly Planet or Garrison.
- Some ship/unit types cannot capture artifacts.
- There is a max garrison limit.

Public page use: structure/deployment reference page; strategy pages can link back to it.

### Free starter, no-drop, and bound item restrictions

Strings and UI code identify these restrictions:

- Free starter ships cannot be bought, traded, or sold.
- Account-bound ships cannot be bought, traded, or sold.
- `NO DROP` items cannot go to the vault.
- Free starter items cannot be equipped to defense units.
- Free starter items cannot be equipped to Hardcore units.
- New players cannot scrap or remove free starting items until Player Level 3.
- Some items cannot be ranked down.
- Some items cannot be modified right now, depending on context.

Public page use: account/item rules page or FAQ entries that link to item rules.

### Corp and one-way action hints

Useful strings:

- Players cannot leave a corporation while in combat.
- AI players cannot be promoted in a corporation.
- Corporate bank can be full.
- Tech Point donations assist with corporate expenses and are one-way.
- Corp Tech Points stay with the corporation.
- Corp unit resource donations are one-way.
- Corp Defenders have a "ready to deploy" state and an "under attack" state in UI.

Public page use: corp rules/reference page. Avoid putting corp strategy in the same file.

### Repair and Oblivion rule hint

`CHDFPJKNCOH.cs` and `CELOHADEBLD.cs` include the string:

- `Oblivion Rule: Items cannot be repaired!`

This needs public wording after we confirm what "Oblivion" maps to in current live terms.

## 6. Achievements and Leaderboards

Useful source files:

- `OGHCKGOOEPK.cs`
- `AHJEJEBENMA.cs`
- `AHFAPFNMNPJ.cs`
- `LMMFNJLGHED.cs`

### Leaderboard enum families

The client has leaderboard/stat categories for:

- Achievements, major achievements, critical achievements, and titles
- Ship XP and Defense XP
- Resources harvested and credits earned
- Spaceball credits and Tech Points
- Party Boxes opened and completed
- Arena wins, Hardcore arena wins, arena kills, Hardcore arena kills, Arena Phoenix, Arena Gladiator
- Solo, corp, alliance, and universe missions
- Mission Tech Points
- Crafting: ultimate ships, Interdictor, CPU kits, items, blueprints, ships, Assassin, Hades, Carrier, Emperor
- Loot: items, legendary loot, ultimate loot, relics, fragments harvested
- PvE kills: NPCs, planets, garrisons, outposts, shipyards, Pirates, Precursors, Wyrds, Hets, major leaders, minor leaders, Assassin leaders
- Invasions: wins, items looted, leaders, bosses
- PvP: players killed, Hardcore players killed, skulls earned, PvP planets/garrisons/outposts/shipyards killed

`AHJEJEBENMA.GetCategory` groups those into Player, Arena, Missions, Crafting, Loot, PvE, Invasions, and PvP leaderboard categories.

The client also supports corp leaderboard handling for many of these categories. Do not assume every leaderboard has a corp version until the specific enum is checked.

### Achievement ladder groups

The achievement table is large. It is best used as a checklist for a future achievement index rather than copied into core gameplay pages.

Confirmed groups include:

- Arena wins and Hardcore arena wins.
- Party Box opened and Party Box completed.
- Rift Daily Challenge completion.
- Mission completion, plus alliance/corp/universe mission completion.
- Corp XP contribution and Corp Tech Point contribution.
- Leader kills, including Assassin Leader kills.
- Deploy, scrap, and build ship families by faction and ship class.
- Scrap, loot, repair, and upgrade item achievements across item categories.

Arena win ladders include dense early thresholds from 1 to 20 wins, then larger milestones through 5,000.

Corp XP contribution ladder includes:

- 10, 50, 100, 250, 500, 750
- 1,000 through 10,000 in 500-step milestones
- 20,000, 30,000, 40,000, 50,000
- 100,000 through 500,000 in 100,000-step milestones
- 1,000,000

Leader kill ladders include early milestones 1, 5, 10, 25, 50, 100, then larger long-tail milestones.

### Item achievement axes

Item achievement generation references these item categories:

- Weapon
- Armor
- Storage
- Drone
- Engine
- Computer
- Special
- Shield
- Battery

Rarity axes include Basic through Ultimate. Repair and upgrade achievements appear to start at Uncommon rather than Basic.

Public page use: create an achievement/leaderboard reference page later. Keep it separate from build or progression strategy.

## 7. Missions, Gifts, Daily/Event Surfaces

Useful source files:

- `MLGDJJKFBBH.cs`
- `OEFFLDGGABF.cs`
- `LMMFNJLGHED.cs`
- `AHJEJEBENMA.cs`
- `AHFAPFNMNPJ.cs`
- `UiManager.cs`

### Mission type enum

`MLGDJJKFBBH` defines mission types:

- KillPlayers
- KillNpcDefenses
- HuntNpcLeaders
- HarvestResources
- HuntNPCs
- HuntEliteNPCs
- Explore
- Deposit
- CraftItem
- UpgradeItem
- EquipItem
- ScrapItem
- Mine
- Rescue
- Distress
- OutpostDeposit
- HuntNamedNPC

### Tutorial/simple mission seed list

`OEFFLDGGABF.FGLJOOGNOHM` defines a small seed list:

- Rescue
- Mine
- Deposit
- CraftItem
- EquipItem
- UpgradeItem
- ScrapItem

The constructor arguments need naming before we expose exact values publicly.

### Chain/outpost mission data

`OEFFLDGGABF.JHMJFCGOLHN` defines multiple mission chains with system/id-like values and allowed faction/class pools.

Repeated chain mission components include:

- Distress
- HuntNPCs
- OutpostDeposit
- HuntNamedNPC

Observed chain tiers include values such as:

- Distress 100/1, HuntNPCs 300/5, OutpostDeposit 300/5
- Distress 150/2, HuntNPCs 350/6, OutpostDeposit 350/6, HuntNamedNPC 500/5
- Distress 200/3, HuntNPCs 400/7, OutpostDeposit 400/7, HuntNamedNPC 600/10
- Distress 250/4, HuntNPCs 450/8, OutpostDeposit 450/8, HuntNamedNPC 700/15

These look like amount/level/count fields, but the field names need confirmation before public documentation.

Allowed chain ship pools include Pirate, Precursor, Het, and Wyrd ships at different tiers.

### Mission stat buckets

`LMMFNJLGHED.cs` stores mission count buckets:

- `SolMis`
- `CrpMis`
- `AliMis`
- `UnvMis`

Leaderboard enums also include `MissionTechPoints`.

### Gifts and event surfaces

Client strings and achievement labels confirm UI surfaces for:

- Daily Login Bonus
- Party Box open/completion
- Rift Daily Challenge
- Daily/event descriptions

Party Box achievement ladders include:

- Open 1, 5, 10, 25, 50, 100 Party Boxes.
- Finish 1, then 5, 10, 20...100, then longer milestones through 1,000 Party Boxes.

Rift Daily Challenge achievements include early consecutive-style multipliers and long-tail milestones through 5,000.

Old fallback/training text mentions:

- A FREE button at defense units for free crafting resources.
- A Gift Box that can upgrade ships, elite ranks, equipped item rarity/quality, durability repairs, and other outcomes.
- A 00:00 UTC reset.
- Anti-gaming behavior if players try to force Gift Box outcomes.

Keep those as historical/training hints until confirmed against current live behavior or server data.

## 8. Combat, Abilities, Status, and Targeting

Useful source files:

- `IFOIKKPPAON.cs`
- `AHFAPFNMNPJ.cs`
- `DDEIFGPEOMI.cs`
- `DFHOJHHBAMJ.cs`

### Ability enum

`IFOIKKPPAON` defines:

- Scan
- Cloak
- Repair
- Drain
- Grapple
- Hack
- Strike
- Purge

### Ability helper rules

`AHFAPFNMNPJ.cs` confirms:

- Repair and Purge cannot be hacked.
- Strike is not usable in the arena.
- Repair can target defense units.
- Repair, Drain, Grapple, Hack, and Purge require a target.
- Drain, Grapple, Hack, and Strike are hostile actions.
- Scan, Cloak, Grapple, and Hack can have battery costs; Repair, Drain, Strike, and Purge return 0 from the battery cost helper.

Battery costs are pulled from runtime config values and can be multiplied by a caller-provided multiplier. Some caller flags make the cost 0.

### Ability speed technology mapping

The speed helper maps abilities to tech families:

- Scan -> SpeedScan1/2/3
- Cloak -> SpeedCloak1/2/3
- Repair -> SpeedRepair1/2/3
- Drain -> SpeedDrain1/2/3
- Grapple -> SpeedGrapple1/2/3
- Hack -> SpeedHack1/2/3

Technology descriptions confirm:

- Advanced Hacking adds hack duration; rank 3 also makes targets lose special abilities.
- Advanced Grappling adds grapple duration; rank 3 also drags targets on move.
- Advanced Draining adds shield and battery stolen by Drain; rank 3 can critical.
- Speed Hack/Grapple/Drain ranks reduce those cooldowns by 4/6/8 seconds.

### Target locking and attack timers

`DDEIFGPEOMI.GetLockTimeMS` confirms lock-time inputs:

- Corp defense uses the minimum lock value directly.
- Fighter/drone lock calculation can use a different base than weapon lock calculation.
- Attacker size is capped at 4.5 for non-fighter lock calculations.
- Target size modifies lock time through the size lock step.
- TargetingSpeedPercent is applied to the calculated base.
- Final lock time cannot go below the configured minimum lock time.

`SetAttackTarget` updates targeted counts on old/new targets and calls `SetWeaponLockTimes`.

`SetWeaponLockTimes` confirms:

- Clearing a target resets non-locked weapon/drone timers.
- Fighters are staggered after the fighter lock time.
- Weapons are staggered after the weapon lock time.
- Corp defense uses shorter stagger divisors.
- Weapon-specific lock multipliers can scale final lock timing.

Public page use: this belongs on a combat/targeting rules page. Do not mix with fleet target-calling strategy.

### Interdictor and Space Lane interactions

`DDEIFGPEOMI.GetInterdictorPenalty` returns no penalty for corp defense or missing sector. Otherwise it asks the current sector for the ship/faction penalty.

`DDEIFGPEOMI.GetSpaceLaneBonus` returns no bonus when:

- The entity is corp defense.
- The current sector has an interdictor penalty.
- The ship has no special.

If the sector has the Space Lane flag, it returns the highest Space Lane effect. Otherwise it uses the ship special's Space Lane rank.

`DFHOJHHBAMJ.GetInterdictorEffect` maps Interdictor1/2/3/4 to InterdictorEffect1/2/3/4.

Public page use: movement/reference page can link to Interdictor and Space Lane mechanics. Strategy belongs in a separate fleet movement page.

### Other combat helpers worth mining later

`DDEIFGPEOMI` also exposes helpers for:

- Next attack item selection.
- Next harvest drone timer.
- Technician rank, with default technician rank fallback.
- Regeneration tech selection.
- Reset behavior that clears target, weapon/drone timers, cooldowns, and restores hull/shield/battery.

## Public Page Candidates

Do after a review pass, not automatically:

- `Reference/Arena-Rules.md`
- `Reference/Deployment-Rules.md`
- `Reference/Account-And-Item-Restrictions.md`
- `Reference/Achievements-And-Leaderboards.md`
- `Reference/Mission-Types.md`
- `Reference/Combat-Targeting.md`
- `Reference/Abilities.md`
- `Reference/Interdictors-And-Space-Lanes.md`

Rules pages should link to strategy pages, but strategy should stay out of the rules files.

## Needs Confirmation

- Exact field names for `ChainMissionData` constructor arguments.
- Which old FREE/Gift Box strings are still live behavior.
- Exact daily reset time in current live server behavior.
- Exact arena validation outcomes for alien artifact/hardcore edge cases.
- Exact definition of "Oblivion Rule" in current public player language.
- Exact interdictor penalty values by rank/effect.
- Server-authoritative durations/effects for Hack, Grapple, Drain, Purge, Strike, Scan, Cloak, and Repair.
