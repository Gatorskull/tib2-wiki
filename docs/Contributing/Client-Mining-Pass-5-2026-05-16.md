# Client Mining Pass 5 - Commands, PvP, Loot, Vision, Economy

Date: 2026-05-16

Scope: Current Steam client decompile under `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled\Assembly-CSharp`.

This note covers five more extraction areas after `Client-Mining-Pass-4-2026-05-16.md`:

9. Commands and UI workflows
10. PvP, skulls, and structure combat surfaces
11. Loot, reward, and pity surfaces
12. Vision, scan, cloak, and deception
13. Economy, market, repair, scrap, and deconstruction

Public wiki rule: use these findings to build reference pages. Strategy belongs in separate strategy files that link back to the reference pages.

## 9. Commands and UI Workflows

Useful source files:

- `PPKFDLLBBOP.cs`
- `UiManager.cs`
- `GiftClaimPanel.cs`
- `AuctionSearchPanel.cs`
- `ChatPanelSmall.cs`
- `HelpPanel.cs`

### Chat command transport

`PPKFDLLBBOP.DoChat(...)` is the main client method for sending chat text.

Stable behavior:

- The requested channel must pass `CanClientSend()`.
- Chat input is sanitized/prepared with a 200-character limit.
- Empty prepared input is not sent.
- Any message beginning with `:` is forced to the Sector channel before sending.
- The client sends the resulting chat command through `GKHDFFBMNAK.Get(...)`.

Public use: player-facing command pages can safely say colon commands are sent through chat and are treated as sector chat commands by the client.

### Wiki/UI command links

`UiManager.TryChatCommandClick(...)` handles clickable command links embedded in text.

Stable behavior:

- Clickable command links must contain the marker `!COMD!`.
- The client strips the marker payload and sends it as a colon command.
- The command is sent through `DoChat(..., Sector, ":" + command)`.

Public use: wiki pages can use command links where the client supports them, but public docs should still show the literal command text near the link.

### Gift and party commands

`GiftClaimPanel.cs` exposes UI buttons that send:

- `:gift remutate`
- `:gift revoid`
- `:gift retro`
- `:gift deception`
- `:gift majorparty`
- `:gift minorparty`
- `:gift title`
- `:gift random`
- `:partyall`
- `:partygift`

The panel also sends `Score` to Corp chat in one branch.

Needs confirmation:

- Which of these commands are player-facing, admin-only, event-only, or hidden behind specific reward claims.
- Whether the command names should be published as direct player instructions or only documented as internal UI behavior.

### Market and Spaceball commands

Observed UI chat sends:

- `:sell` from `AuctionSearchPanel.cs`
- `:buy` from `AuctionSearchPanel.cs`
- `:sbreport` from `ChatPanelSmall.cs`
- `:sbhistory` from `ChatPanelSmall.cs`

`PPKFDLLBBOP` also has Spaceball betting helpers with separate money checks for Credits and Tech Points.

Public use:

- Market workflow pages can mention `:buy` and `:sell` only after confirming they still open the current auction/search UI.
- Spaceball pages can mention report/history commands after live confirmation.

### Hotkeys and quick controls

`UiManager.cs` maps configurable key bindings to:

- Selecting deployed ships by index.
- Scan.
- Cloak.
- Repair.
- Drain.
- Grapple.
- Hack.
- Strike.
- Zoom in/out.
- Camera movement in 8 directions.

Public use: this belongs on a settings/controls page, not scattered through ability pages.

### Quick jump workflow

`UiManager.OnQuickJumpSelectTarget(...)` calls `DoQuickJumpAll(DAIGJCMHDJK.Defense, targetDefenseUnit)` after selecting a target defense unit.

Old embedded wiki text says Quick Jump can jump ships to any defense unit in the player's alliance or a discovered human-faction jump gate for 1 Tech Point, regardless of number of ships moving. Treat that as a historical/training hint until confirmed with current client/server behavior.

## 10. PvP, Skulls, and Structure Combat Surfaces

Useful source files:

- `AHJEJEBENMA.cs`
- `AHFAPFNMNPJ.cs`
- `AbilityHotbarButton.cs`
- `HPOJDEDIMKH.cs`
- `AJDGBIOKNKA.cs` fallback wiki text

### Leaderboard and achievement surfaces

Confirmed leaderboard/stat surfaces include:

- Players killed
- Hardcore players killed
- Skulls earned
- PvP planets killed
- PvP garrisons killed
- PvP outposts killed
- PvP shipyards killed

`AHJEJEBENMA` displays skull leaderboard text as:

- `Skulls Earned`
- `Collect Enemy Player Skulls`

Achievement families include:

- Player kill ladders.
- Hardcore player kill ladders.
- Planet/Garrison/Outpost/Shipyard kill ladders.
- Faction structure kill ladders for Wyrd, Pirate, Het, and Precursor.
- Repair and level-up achievements for Planet, Garrison, Outpost, and Shipyard.

Public use: achievement/leaderboard pages can list these as tracked categories. They do not by themselves prove exact skull payout formulas.

### Skull currency and skull piles

Skulls appear as a currency/resource in reward and shop-like contexts.

Confirmed achievement labels:

- Craft Skull Pile 10
- Craft Skull Pile 100
- Craft Skull Pile 500
- Craft Skull Pile 1,000

Other strings indicate:

- Trade Offer Skulls.
- GiveSkulls and RemoveSkulls reward/action enums.
- Ship durability repair may use Skulls, based on embedded fallback wiki text and UI strings.

Needs confirmation:

- Current skull payout formulas for player kills and structure kills.
- Whether skull pile crafting is live, event-limited, or legacy.
- Exact use of Skulls in ship durability repair and trade offers.

### Structure combat boundaries

Already-confirmed deployment/structure rules from prior passes should remain the canonical source:

- Defense units cannot deploy in Homeworld systems.
- Defense units cannot deploy in The Arena.
- Defense units cannot deploy on jump gates.
- Deployment can be blocked by enemy proximity or enemy territory.
- Ship construction requires a friendly defense unit.
- Artifact capture requires a deployed friendly Planet or Garrison.

Public use: do not mix target-calling or fleet doctrine into structure rules. Strategy pages can link to the rules.

## 11. Loot, Reward, and Pity Surfaces

Useful source files and existing notes:

- `Client-Extracted-Loot-Rewards.md`
- `AHFAPFNMNPJ.cs`
- `AbilityHotbarButton.cs`
- `HPOJDEDIMKH.cs`
- `AJDGBIOKNKA.cs` fallback wiki text

### Existing extracted page is still canonical

Use `Client-Extracted-Loot-Rewards.md` as the main contributor staging page for reward/pity data. This pass confirms additional surfaces but does not replace that page.

Known reward/pity surfaces already staged include:

- Activity reward types such as Invasion, Planet, Garrison, Shipyard, Outpost, Critical, Repair, Grapple, Hack, and Harvest.
- Party-box rarity affecting maximum task count shown for activity rewards.
- Loot/reward labels that distinguish activity-specific bonuses from general loot item achievements.

### Loot achievement axes

Achievement families confirm item loot tracking by:

- Item category: Weapon, Armor, Storage, Drone, Engine, Computer, Special, Shield, Battery.
- Rarity/rank bucket: R1 through R7 naming in client enums.

General loot-count milestones include:

- 5, 10, 25, 50, 75, 100
- 150 through 1,000 in several steps
- Larger milestones through 500,000

Rarity-specific loot milestones are generated for each rank bucket.

Public use: good for an achievement index; not a loot/drop-rate page.

### Relic tracking

Achievement families confirm relic ladders for:

- Wyrd
- Het
- Human
- Precursor

Observed milestones include 1, 5, 10, 25, 50, 75, 100, 200, 300, 400, 500, and 1,000.

Needs confirmation:

- Current relic source/drop rules.
- Whether Pirate relic handling is absent by design or handled under another label.

### Daily/event reward hints

Embedded fallback wiki text says:

- Holiday event special NPCs can drop rare/powerful items.
- Some event targets are hidden by delayed clues.
- The "Ancient Alien Secrets Hidden In Asteroids" daily event involves real asteroids and special item entry through deconstruct/blueprints.
- The text says lower risk means lower reward and PvP maps give better results.
- Freighter and resource-harvest bonuses may improve those event chances.

Treat this as historical/training text until verified against live behavior or server data.

## 12. Vision, Scan, Cloak, and Deception

Useful source files:

- `DDEIFGPEOMI.cs`
- `DFHOJHHBAMJ.cs`
- `AHFAPFNMNPJ.cs`
- `AbilityHotbarButton.cs`

### Cloak-breaking movement/status events

`AHFAPFNMNPJ.GetBreaksCloak(...)` returns true for:

- Destroyed
- Destroyed Arena
- Depleted
- Jump
- Dragged
- Thrown
- Rammed
- Recalled
- Recalled Arena

Public use: this is strong enough for a cloak reference page, but exact server timing should still be confirmed.

### Cloak and scan technology descriptions

`DFHOJHHBAMJ.cs` confirms display descriptions:

- Cloak ranks hide from enemy vision with Power 1 through Power 7.
- Scan ranks actively reveal Cloaking Rank 1 through Rank 7.
- Advanced Scanning adds +1 Scanning Power and requires Scanning.
- Advanced Cloaking adds +1 Cloaking Power and requires Cloaking.
- Passive Scanning counters sneak attacks and adds +15%, +20%, or +30% detect cloaked enemy chance.
- Cloak Duration ranks add +3, +5, or +7 seconds.
- Speed Scan ranks reduce Scan cooldown by 4/6/8 seconds.
- Speed Cloak ranks reduce Cloak cooldown by 4/6/8 seconds.
- Stealth1 hides movement direction and time.
- Stealth2 hides movement direction and grants immunity to Passive Scan.
- Long Range Vision increases sector vision range.

Public use: technology family pages can use these descriptions directly, but rule pages should still avoid pretending we know server-side detection rolls.

### Which technologies affect vision

`DFHOJHHBAMJ` helper methods identify:

- Stealth-related tech as Cloak1 through cloak-family range.
- Scanning-related tech as PassiveScan1 through scan-family range.
- `GetEffectsVision(...)` returns true for stealth-related or scanning-related tech.
- `GetIsPassiveScanning(...)` returns true for PassiveScan1/2/3.

### Deception visible-item logic

`DDEIFGPEOMI.GetVisibleItems(...)` and `GetTestDeception(...)` show that Deception can hide equipment from some viewers.

Stable behavior:

- If Deception does not apply, all equipped items are returned.
- If Deception applies, only non-hidden slots are returned.
- Deception does not apply when the entity is not using the deception state, when override/inspect flags are active, or when the viewer has a bypass flag.
- Deception does not hide from the owning player.
- Deception does not hide from friends according to the player relationship helper.
- For non-player entities, same-corp viewing can bypass deception.

Needs confirmation:

- Exact item slots hidden by each Deception state/rank.
- Exact player relationship cases that count as friend/allied for deception visibility.

### Sector visibility enum helpers

`AHFAPFNMNPJ` has helpers for sector visibility states:

- `IsExploredOrVisible(...)`
- `IsVisible(...)`

`IsVisible(...)` returns true for `NotExploredButVisible` and `ExploredAndVisible`.

Public use: map exploration pages can mention "visible" and "explored" are separate client states.

## 13. Economy, Market, Repair, Scrap, and Deconstruction

Useful source files:

- `AuctionSearchPanel.cs`
- `PPKFDLLBBOP.cs`
- `AHFAPFNMNPJ.cs`
- `AbilityHotbarButton.cs`
- `CorpInspectPanel.cs`
- `AJDGBIOKNKA.cs` fallback wiki text

### Market and auction surfaces

Observed UI surfaces:

- `AuctionSearchPanel.cs` can send `:sell`.
- `AuctionSearchPanel.cs` can send `:buy`.
- UI strings include `Create Auction Failed`.
- UI strings include `You cannot buy your own item!`.
- The client has a `Market` chat/channel enum usage for one generated search command.

Needs confirmation:

- Current auction fee rules.
- Which item/ship binding flags block market listing.
- Whether `:buy`/`:sell` are still intended public shortcuts or only UI internals.

### Scrap and deconstruct achievement coverage

Achievement families confirm:

- Scrapping ships by ship class and by faction.
- Scrapping Hardcore ship variants.
- Scrapping items by item category and rarity/rank bucket.
- Deconstructing items by item category and rarity/rank bucket.

Item categories match the earlier item axes:

- Weapon
- Armor
- Storage
- Drone
- Engine
- Computer
- Special
- Shield
- Battery

Public use: achievements can list these as tracked actions. Crafting/economy rules still need recipe/cost/resource formulas before public claims.

### Blueprint research hint

The client includes the UI string:

- "You haven't begun any item crafting research! DECONSTRUCT extra items to discover new blueprints!"

This supports the rule that deconstruction is tied to item crafting blueprint discovery, but exact odds/formulas still need data.

### Repair surfaces

Confirmed from prior passes:

- `Oblivion Rule: Items cannot be repaired!` exists in item repair UI paths.
- `Repair Item` appears as a client action label.
- Embedded fallback wiki text says item durability does not affect stat bonuses, but 0% durability prevents equipping and must be repaired.
- Embedded fallback wiki text says ship durability can reduce stats and can be repaired with Skulls.

Needs confirmation:

- Current item repair costs.
- Current ship durability repair costs.
- Exact stat effects of ship durability.
- Whether item durability truly has no stat effect in current live behavior.

### One-way corp economy actions

Already-staged corp strings remain important:

- Corp Tech Point donations are one-way.
- Corp Tech Points stay with the corporation.
- Resource donations to level corporate units are one-way.

Public use: corp economy/reference page; no strategy in that file.

## Public Page Candidates

Do after a review pass:

- `Reference/Commands.md`
- `Reference/Controls-And-Hotkeys.md`
- `Reference/Quick-Jump.md`
- `Reference/Skulls.md`
- `Reference/PvP-Tracked-Stats.md`
- `Reference/Loot-And-Pity.md`
- `Reference/Relics.md`
- `Reference/Vision-Scan-Cloak.md`
- `Reference/Deception.md`
- `Reference/Market-And-Auctions.md`
- `Reference/Repair-Scrap-Deconstruct.md`

Strategy pages can link to these. Do not place fleet doctrine, farming routes, or market pricing advice in the reference pages.

## Needs Confirmation

- Which chat commands are meant for public use in current live client.
- Exact Quick Jump target rules and Tech Point cost.
- Current skull payout formulas.
- Current skull pile crafting behavior.
- Current item/ship market restrictions and fees.
- Current repair costs and durability effects.
- Current relic source/drop rules.
- Current loot/pity odds and server-side reward logic.
- Exact Deception hidden-slot behavior.
- Server-authoritative cloak/scan/passive-scan detection timing and rolls.
