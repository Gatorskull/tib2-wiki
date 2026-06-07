# Client Mining Pass 6 - Validation Gates, Item Actions, Helper Mechanics

Date: 2026-05-16

Scope: Current Steam client decompile under `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled\Assembly-CSharp`.

This note covers five more extraction areas after `Client-Mining-Pass-5-2026-05-16.md`:

14. Defense deployment and attack validation
15. Ability validation gates
16. Item engineering and item modification
17. Helper mechanics for repairs, specials, and next actions
18. Entity, deception, retro skin, and relic display helpers

Public wiki rule: gameplay/rules pages should contain only observed logic and may link to separate strategy pages. Do not place strategy advice inside canonical gameplay reference pages.

## 14. Defense Deployment and Attack Validation

Useful source file:

- `IKOLEGFOADL.cs`

### Attacking defense units

`CanAttack(...)` first calls the general targeted-action validator, then applies combat-specific gates.

Stable behavior:

- If the attacking ship is taunted and its taunt target is still in the same sector, attacking is blocked with a taunt timer message.
- A target with a non-enemy relation cannot be attacked.
- A ship with no weapons or fighter drones cannot attack.
- Defense units can only be attacked by players in an alliance.
- Defense unit attacks require the attacking ship to meet a configured gear score minimum.
- Defense unit attack protection blocks attacks while the protection timer is active.
- Non-defense protected targets block attacks unless the relevant protection bypass state applies.

Public use:

- The Structures or PvP reference can state that defense attacks are alliance-gated and gear-score-gated.
- The exact gear score threshold is config-driven and should be filled from extracted configuration before publishing as a fixed value.

### Deploying defense units

`CanDeployDefense(...)` validates ownership, alliance context, map context, cost, sector rules, and duplicate structure rules.

Stable behavior:

- The defense unit must not already be deployed.
- The defense unit must belong to a corporation.
- The corporation must belong to an alliance.
- The defense unit must belong to the player's corporation.
- Invasion maps block deployment.
- Arena maps block deployment.
- Deployment requires a configured corporation Tech Point cost.
- Homeworld/security-restricted systems block deployment.
- Some non-default/special map states block deployment.
- If another alliance controls the system, only Outposts can be deployed in captured maps; the client message points players toward destroying the local shrine Garrison.
- Deployment cannot happen in enemy territory.
- Planet deployment requires a valid planet class.
- A sector cannot already contain the same defense unit type being deployed: Planet, Garrison, Outpost, or Shipyard.

### Deployment proximity checks

`TestDeploySector(...)` is run against the current sector and linked/nearby sectors.

Stable behavior:

- Current-sector deployment is blocked if too close to a Space Lane.
- Deployment is blocked if too close to a Jump Gate.
- Deployment is blocked if too close to a Jump Gate destination.
- Deployment is blocked if an enemy defense unit is nearby.
- Deployment is blocked if an enemy ship is nearby, unless that ship has the relevant ignore/protection bypass state.

Needs confirmation:

- The exact shape of "linked/nearby sectors" should be mapped from the caller loop before the public page describes a radius.
- The client messages mention Space Lanes, Jump Gates, and Jump Gate destinations, but the underlying sector flags need clearer public names.

## 15. Ability Validation Gates

Useful source file:

- `IKOLEGFOADL.cs`

`CanUseAbility(...)` centralizes several active ability checks.

Stable behavior:

- The player ship must pass the general "my ship" validation.
- Abilities that cannot be used in Arena are blocked by the shared validator when the ship is in Arena context.
- Cloak requires the ship not already be cloaked and requires cloaking power above zero.
- Strike delegates to a separate Garrison Strike validator.
- Scan requires scanning power above zero.
- Purge requires an available Technician rank.
- Hack requires Hack Power at or above a configured minimum.
- Grapple requires Grapple Power at or above a configured minimum.
- Drain requires Battery Drain Power at or above a configured minimum.
- Ability cooldowns block use and show a wait timer.
- If a hackable ability is blocked while the ship is hacked, the message uses the hacked timer instead of the generic wait timer.
- Battery power must meet the ability's computed battery cost.
- Target-required abilities require a target in the same sector.
- Target-required abilities cannot target destroyed entities.
- Hostile target abilities require a hostile target and respect protection unless the ship can ignore protection.
- Abilities that cannot target defense units are blocked from doing so.
- Purge requires the target to have a removable status; the client checks hacked, taunted, or grappled style flags.
- Repair requires the target to be below maximum hull.

Public use:

- The Abilities reference can document validation as rules without recommending when to use each ability.
- Strategy pages can link back to the ability reference for exact gates.

Needs confirmation:

- The shared minimum used by Hack, Grapple, and Drain should be named from configuration extraction before publishing the numeric threshold.
- Purge status names should be confirmed against public terms; the client logic clearly checks three removable status flags, but one message string says the target is "already repaired."

## 16. Item Engineering and Item Modification

Useful source files:

- `JCGFOGKIBPM.cs`
- `IKOLEGFOADL.cs`

### Engineering actions

`CanApplyUpgrade(...)` validates item engineering operations before changes are applied.

Stable behavior:

- Repair is blocked for items that cannot be repaired.
- The Oblivion rule can globally block repairs with a specific message.
- Repair is blocked if the item is already at 100% durability.
- Rank Up and Rank Down are limited to Weapon, Armor, Storage, and Shield items.
- Rank Up is blocked if the item's base Equip Point cost is already 30 or higher.
- Rank Down is blocked if the item's base Equip Point cost is already 1 or lower.
- Rarity upgrade is blocked for R1 items.
- Rarity upgrade is blocked for R7 items.
- The Oblivion rule can block upgrading R6+ items to Ultimate.

### Engineering effects

`InternalApplyUpgrade(...)` applies the validated engineering change.

Observed behavior:

- Repair restores durability to 100%.
- Normal repair tracks repaired durability; every 15 accumulated repair points can reduce item quality by 1, down to signed byte minimum.
- Rank Up increases base Equip Point cost by 1, bounded to 1-30.
- Rank Down decreases base Equip Point cost by 1, bounded to 1-30.
- Rarity upgrade increases rarity by 1.
- Some rarity kit types can increase rarity by an additional step while still below R7.
- Non-free rarity upgrades can add kit quality bonus, clear starter/newbie style flags, and add kit durability bonus up to 250 durability.
- Rarity upgrade also increases base Equip Point cost by 1 for Weapon, Armor, Storage, and Shield items.

Public use:

- The item engineering reference should separate validation rules from effects.
- The repair-quality degradation should be documented carefully because it is easy to miss and likely important.

Needs confirmation:

- Name the engineering kit types from extracted enum/member names before making a polished public table.
- Confirm whether "normal repair can reduce quality" is server-authoritative or only client-predicted display behavior.

### Scrap, deconstruct, corp bank, and auction gates

`CanScrapItem(...)`, `CanMoveItemToCorp(...)`, `CanItemBeAuctioned(...)`, and `CanBuyoutItem(...)` expose common item restrictions.

Stable behavior:

- Missing/deleted items cannot be modified.
- Temporarily rarity-upgraded items cannot be scrapped/deconstructed.
- Item Lock blocks scrap, deconstruct, auction, and moving to corporation bank.
- Items in trade cannot be modified.
- Crafted items cannot be deconstructed.
- Free starter items cannot be deconstructed.
- Items with no deconstruction value/chance cannot be deconstructed.
- Some consumables cannot be scrapped.
- Items not owned by the player cannot be scrapped or deconstructed.
- Equipped items on player-owned ships/entities cannot be scrapped while in combat, in Arena queue, or in Arena.
- Listed items must have their sale cancelled before scrap/deconstruct.
- Free starter items cannot be scrapped until player level 3.
- Moving an item to corporation bank requires the player to be in a corporation and requires available corporation bank space.
- Auctionable items must be in a player's inventory, cannot be free starter items, cannot be no-drop items, cannot be locked, and cannot be in trade.
- Items for sale must be in the player's bank.
- No Repair items cannot be sold at 0% durability.
- Buyout requires the auction to be active, have a buyout price, and not belong to the buyer.
- If the current buyer is already the high bidder, buyout cost is buyout minus current bid; otherwise it is the full buyout.

Public use:

- These restrictions belong on an Item Management or Economy reference page.
- Market price guidance should stay out unless it is clearly dated and observed.

## 17. Helper Mechanics for Repairs, Specials, and Next Actions

Useful source files:

- `DDEIFGPEOMI.cs`
- `JCGFOGKIBPM.cs`

### Repair facility bonus selection

`GetBestRepairFacilityBonus()` selects the best nearby repair facility bonus.

Observed behavior:

- Defense units map directly to their own repair facility bonus:
  - Planet: `RepairFacility3`
  - Garrison: `RepairFacility2`
  - Outpost: `RepairFacility1`
  - Shipyard: `RepairFacility4`
- Ships require a current sector.
- For ships, friendly/non-enemy nearby structures are checked.
- Best observed priority is Shipyard, then Planet, then Garrison, then Outpost.
- One config path also requires the facility structure not be destroyed.

Public use:

- Document repair facility rank by structure type once structure public names are confirmed.

### Technician rank

`GetTechnicianRank()` combines equipped Technician and default Technician rank.

Stable behavior:

- If no Technician special is equipped, the entity returns its default Technician rank.
- If a Technician special is equipped and there is no default rank, the special rank is used.
- If both exist, the higher rank is used.

Public use:

- Technician pages should note that default Technician rank and equipped Technician rank do not stack additively; the higher rank wins.

### Highest-rank technology selectors

Several helpers scan from rank 7 down to rank 1 and return the highest available rank.

Observed examples:

- `GetRegeneration()` checks `Regeneration7` down to `Regeneration1`.
- `GetHackRamRarity()` checks `HackRam7` down to `HackRam1`.
- `GetNovaDeathRarity()` checks `NovaDeath7` down to `NovaDeath1`, but first blocks normal Small and Medium entities; Large+ or unique ships can qualify.

Needs confirmation:

- Public ability/technology names should be cross-checked against extracted technology display text before publishing.
- Nova Death size gating should be verified against real client UI or server behavior because the unique-ship exception is a little surprising.

### Deflector and Battle Ram

Observed behavior:

- `GetDeflectorRarity()` returns the highest `Deflector7` to `Deflector1` technology rank.
- `GetDeflectorPercentChance()` maps rarity to chance:
  - R1: 3%
  - R2: 5%
  - R3: 7%
  - R4: 9%
  - R5: 11%
  - R6: 13%
  - R7: 15%
- `GetBattleRamRarity()` only returns a rank when the equipped special item is Battle Ram.
- Battle Ram special items map `BattleRam1` through `BattleRam7` to R1 through R7.

Public use:

- Deflector can be documented as technology-derived.
- Battle Ram can be documented as special-item-derived.

### Next attack and next harvest selection

`GetNextAttackItem()` and `GetNextHarvestSeconds(...)` select the next item to use by readiness.

Stable behavior:

- Fighter drones and weapons are both considered for the next attack item.
- The client compares the greater of lock timer and cooldown timer for each candidate.
- The next attack item is the candidate with the lowest remaining effective wait.
- Disabled weapon slots are ignored.
- Harvest drone selection only considers harvest drones.
- Harvest selection picks the drone with the lowest remaining harvest cooldown, with an immediate-ready shortcut when the cooldown timer is in its ready state.

Public use:

- These mechanics belong on item/ability reference pages only if players need to understand automation or UI readiness order.

## 18. Entity, Deception, Retro Skin, and Relic Display Helpers

Useful source file:

- `DFHOJHHBAMJ.cs`

### Deception hidden slot thresholds

`GetIsDeceptionHidden(slot, deceptionRank)` exposes which item slots are hidden at each Deception rank.

Observed thresholds:

- Weapon 1: rank 5+
- Weapon 2: rank 4+
- Weapon 3: rank 3+
- Weapon 4: rank 2+
- Weapon 5: rank 1+
- Weapon 6: always hidden
- Drone 1: rank 5+
- Drone 2: rank 4+
- Drone 3: rank 3+
- Drone 4: rank 2+
- Drone 5: rank 1+
- Drone 6: always hidden
- Armor: rank 2+
- Storage: always hidden
- Engine: rank 5+
- Computer: rank 3+
- Battery 1: rank 5+
- Battery 2: rank 4+
- Battery 3: rank 3+
- Battery 4: rank 2+
- Battery 5: rank 1+
- Battery 6: always hidden
- Shield: rank 1+
- Special: rank 4+

Public use:

- This can become a Deception reference table after terminology is checked against the UI.

### Relic and entity helpers

Observed behavior:

- `IsRelicShrine(...)` returns true for Human, Wyrd, Het, and Precursor relic entities.
- `GetRelicFaction(...)` maps those relics to Human, Wyrd, Het, and Precursor.
- Relic shrine display names vary by size:
  - Small: Minor [Faction] Shrine
  - Large: Major [Faction] Shrine
  - Huge: Revered [Faction] Shrine
  - Massive: Sacred [Faction] Shrine
  - Default/fallback: Elaborate [Faction] Shrine
- `IsDefenseUnit(...)` returns true for Planet, Garrison, Outpost, and Shipyard.
- Entity creation maps entity type to runtime class for Artifact, Planet, Garrison, Outpost, Shipyard, Ship, Asteroid, Cargo Money, Cargo Item, and Cargo Resource.

Public use:

- Relic/shrine naming belongs in a clean world-objects or structures reference.
- Runtime class names should stay in contributor notes, not public pages.

### Retro skin matching

`IsRetroSkin(...)` treats retro skins as a contiguous enum range from Retro Shuttle through Retro Terminus.

Observed matching behavior:

- Unique ships pass the retro skin target helper before class matching.
- Non-unique ships use class matching:
  - Retro Shuttle and Retro Scorpion: Shuttle
  - Retro Frigate and Retro Devastator: Frigate
  - Retro Assassin and Retro Invader: Assassin
  - Retro Corvette and Retro Cruiser: Cruiser
  - Retro Destroyer and Retro Dreadnaught: Destroyer
  - Retro Titan and Retro Battleship: Battleship
  - Retro Executioner and Retro Flagship: Flagship
  - Retro Annihilator and Retro Carrier: Carrier
  - Retro Flayer, Retro Despoiler, and Retro Reaper: Hades
  - Retro Hades and Retro Terminus: Emperor

Needs confirmation:

- The unique-ship shortcut should be verified in live UI before saying any retro skin works on any unique ship.
- Public naming should use exactly the display names from item extraction.

## Public Page Candidates

Potential public updates from this pass:

- `Structures.md`: add defense attack and deployment rules, but keep strategy elsewhere.
- `Abilities.md` or `Technology.md`: add ability validation gates and power requirements.
- `Items.md` or an Item Management page: add engineering, repair, scrap, deconstruct, and auction rules.
- `Specials.md`: add Technician, Deflector, Battle Ram, Hack Ram, and Nova Death helper findings.
- `Deception.md`: add hidden slot thresholds after display terminology is confirmed.
- `Relics.md` or Structures/world-objects page: add relic shrine naming and faction mapping.

## Needs Confirmation List

- Exact configured gear score requirement for attacking defense units.
- Exact configured Tech Point deployment cost.
- Exact configured minimum for Hack, Grapple, and Drain power.
- Public names for sector flags: Space Lane, Jump Gate, Jump Gate destination.
- Whether repair quality degradation is server-authoritative or only client-predicted.
- Exact engineering kit names and their public effects.
- Public terms for Purge removable statuses.
- Unique-ship retro skin behavior.
- Nova Death size/unique eligibility.
