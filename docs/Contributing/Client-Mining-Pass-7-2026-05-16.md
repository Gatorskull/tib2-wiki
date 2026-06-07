# Client Mining Pass 7 - Ownership, Fleet, Corp, Alliance, Auction Gates

Date: 2026-05-16

Scope: Current Steam client decompile under `E:\TIB2 DEV FOLDER\2.1.0 Steam Client\Decompiled\Assembly-CSharp`.

This note covers five more extraction areas after `Client-Mining-Pass-6-2026-05-16.md`:

19. Shared ownership and modification validators
20. Ship deployment, recall, scrap, and ship auction gates
21. Corporation invites, creation, renaming, and alliance membership gates
22. Auction setup, bidding, buyout, and sale restrictions
23. Jump gates, jettison, and loot interaction gates

Public wiki rule: these are client-observed rules. Public pages should phrase them as reference mechanics and avoid strategy recommendations.

## 19. Shared Ownership and Modification Validators

Useful source file:

- `IKOLEGFOADL.cs`

### `ValidateMyShip(...)`

`ValidateMyShip(...)` is a shared gate used by abilities, travel, jettison, deployment workflows, and other ship actions.

Observed behavior, depending on caller flags:

- The ship must exist.
- The ship must be controlled by the player.
- Some actions require the ship to be deployed first.
- Some actions require the ship not be destroyed.
- Some actions block Corp Defender ships.
- Some actions block Shuttles.
- Some actions block the free starter ship.
- Some actions block while the ship is in combat.
- Some actions block while the ship is in Arena queue.
- Some actions block while the ship is in Arena.
- Some actions block if the ship has temporary item rarity upgrades.

Public use:

- This explains why many actions produce the same broad error messages.
- Public pages should document the specific caller behavior, not the internal flag list.

### `CanModifyEntity(...)`

`CanModifyEntity(...)` is the shared ownership/rank validator for ships and defense entities.

Stable behavior:

- Missing targets cannot be modified.
- Defense entities can only be modified by members of the owning corporation.
- Defense entity modification can require a minimum corporation rank.
- Ships can only be modified by their owner.
- Optional caller flags block modification while the entity is for sale, in combat, in Arena queue, or in Arena.
- Entities in trade cannot be modified.

Public use:

- The Structures reference can use this as the canonical rule for who may modify corp defense units.
- Item/ship management pages can link back to shared modification restrictions instead of repeating the same explanation everywhere.

## 20. Ship Deployment, Recall, Scrap, and Ship Auction Gates

Useful source file:

- `IKOLEGFOADL.cs`

### Deploying ships

The deploy-ship validator checks ship state, player level, fleet limits, ultimate ship limits, size requirements, and next-ship level requirements.

Stable behavior:

- The player must be allowed to modify the ship.
- A ship at 0% durability is treated as destroyed and cannot deploy.
- A ship already deployed to a sector cannot be deployed again.
- The player must meet the ship's own required player level.
- The fleet cannot already be at the configured maximum size.
- Only one Ultimate ship can be deployed at a time.
- Large fleets require small/medium coverage:
  - Up through 7 deployed ships passes automatically.
  - 8-ship fleets require at least one Medium-or-smaller ship.
  - 9- and 10-ship fleets require at least one Small ship and at least one Medium-or-smaller ship.
- The player must also meet the configured level requirement to deploy the next ship.

Public use:

- This confirms the existing fleet-size text and gives us the exact helper logic.
- The public Ships or Fleet Limits page should link to this instead of repeating fleet deployment rules across beginner guides.

Needs confirmation:

- The public wording should reconcile the client error message that says "9 and 10" with the helper condition that checks the fleet count after the requested deployment.

### Recalling ships and entities

`CanRecallEntity(...)` reuses `CanModifyEntity(...)` and then applies recall-specific gates.

Stable behavior:

- The target must already be deployed.
- Entities cannot be recalled from Arena.
- Ships cannot be recalled if doing so would leave the player with zero deployed ships.
- Corp Defender ships cannot be manually recalled; the client says they automatically recall after combat ends.
- Ships cannot be recalled from a defense unit engagement when an enemy active defense unit is found in linked/nearby sectors.

Public use:

- This belongs on ship management and Corp Defender reference pages.

### Scrapping ships

`CanScrapShip(...)` exposes ship scrap restrictions.

Stable behavior:

- Missing/deleted ships cannot be scrapped.
- The player must own the ship.
- The ship must be scrappable.
- A listed ship must have its sale cancelled first.
- Ships in trade cannot be scrapped.
- Deployed/recalled-state checks require the ship to be recalled first.
- Corp Defender ships cannot be scrapped.
- Ships in Arena queue or Arena cannot be scrapped.
- All equipped items must be removed first.

Public use:

- Ship scrapping rules should live in one management/economy reference and be linked from ship pages.

### Ship auction eligibility

`CanShipBeAuctioned(...)` is the shared pre-check for ship sale, bid, and buyout flows.

Stable behavior:

- Missing/deleted ships cannot be auctioned.
- Free starter ships cannot be bought, traded, or sold.
- Account-bound ships cannot be bought, traded, or sold.
- The ship must be in a player's garage.
- Deployed ships cannot be auctioned.
- Corp Defender ships cannot be auctioned.
- Ships with equipped items cannot be auctioned.
- Ships in Arena queue or Arena cannot be auctioned.
- Ships in trade cannot be auctioned.

Needs confirmation:

- One obfuscated helper near the ship auction code has misleading string fragments; use `CanShipBeAuctioned(...)` as the clean public evidence and ignore the corrupted helper until deobfuscated.

## 21. Corporation Invites, Creation, Renaming, and Alliance Membership Gates

Useful source file:

- `IKOLEGFOADL.cs`

### Corporation rank helpers

Observed rank helpers:

- A player is a corporation commander when they are in a corporation and their rank is at least `Commander`.
- A player is a corporation leader when they are in a corporation and their rank is at least `Leader`.
- A player is treated as a citizen-style account when they are not AI, are young enough by account age/window, and meet the configured citizen player level.

Needs confirmation:

- The exact account-age field behind the citizen-style helper should not be public until named cleanly.

### Inviting players to a corporation

`CanCorpInvite(...)` validates corporation invites.

Stable behavior:

- The target player must exist.
- The inviter must be an officer of a corporation.
- The target must not already be in a corporation.
- AI players cannot be invited.
- If the target has not previously been in the inviter's corporation and meets the configured citizen player level, alliance citizen-cap rules apply.
- Inviting a citizen over the alliance cap can create a Corp Tech Point cost.
- If the over-cap amount is too high, or if a non-commander tries to invite with an over-cap cost, the invite is blocked.
- The inviter's corporation must have enough Corp Tech Points for any over-cap invite cost.
- The inviter's corporation must have member capacity.
- Targets can block invites through ignore-invites/chat-filter style settings or by ignoring the inviter.
- Targets in Arena cannot be invited.

Public use:

- Corporation pages can explain why high-level/citizen invites may be limited by alliance-wide caps.
- Exact cap and cost values should come from configuration extraction before publishing fixed numbers.

### Creating and renaming corporations

`CanCreateCorp(...)` and `CanRenameCorp(...)` validate corporation naming and Tech Point costs.

Stable behavior:

- A player already in a corporation cannot create a new corporation.
- Corporation names must pass the guild-name validator.
- Corporation names must be unique case-insensitively.
- Creating a corporation costs configured Tech Points for non-AI players.
- Renaming requires corporation Leader rank.
- Renaming uses the same name validator and uniqueness check.
- Renaming costs configured corporation Tech Points.

Public use:

- Corporation creation/rename pages should reference configured costs rather than hard-coding them until extracted values are confirmed.

### Alliance invites, kicks, and leaving

`CanInviteCorpToAlliance(...)`, `CanKickCorpFromAlliance(...)`, and `CanLeaveAlliance(...)` expose alliance membership gates.

Stable behavior:

- Alliance invitations require the acting player to be a corporation commander.
- Only the alliance leader corporation can invite other corporations into the alliance.
- A target corporation must be valid, non-AI, and not the acting corporation.
- A target already in the same alliance cannot be invited.
- An alliance has a configured maximum number of corporations.
- A target already in a multi-corporation alliance cannot be invited.
- Alliance citizen cap applies when adding another corporation's citizens.
- Inviting a corporation is blocked if the resulting alliance would control more than 10 Relic Shrines.
- Inviting is blocked if either the target alliance side or the acting alliance side has a defense unit under attack.
- Kicking a corporation requires commander rank and alliance leader corporation status.
- Kicking is blocked if the target corporation is not in the actor's alliance.
- Kicking is blocked while an alliance defense unit is under attack.
- Leaving an alliance requires commander rank.
- The alliance leader corporation cannot use the normal leave flow; the client says to kick everyone instead.
- Leaving is blocked while an alliance defense unit is under attack.

Public use:

- The Alliances reference can separate these stable membership rules from alliance-war strategy.

Needs confirmation:

- The 10 Relic Shrine cap is literal in this method. Confirm whether it is still server-authoritative and whether "Relic Shrine" is the best public term for the counted normal maps.

## 22. Auction Setup, Bidding, Buyout, and Sale Restrictions

Useful source file:

- `IKOLEGFOADL.cs`

### Sale setup

`ValidateSetAuction(...)` is used by item and ship auction setup flows.

Stable behavior:

- Already-listed objects must have the sale cancelled before changing the price.
- Starting bid must be at least 500 Credits.
- Starting bid cannot exceed 999,999,999 Credits.
- Buyout cannot be lower than starting bid when buyout is set.
- Buyout cannot be negative or above 999,999,999 Credits.
- Sale duration maximum is 30 days for buyout-style sales where starting bid is at least buyout.
- Sale duration maximum is 5 days for normal auctions.
- Duration must be above zero and within the applicable maximum.

Public use:

- Market pages can use these as fixed client-observed auction limits.

### Item auction and buyout

Item auction findings from this pass and Pass 6 combine into the following stable rules:

- Auctionable items must be in a player's inventory.
- Free starter items cannot be dropped, traded, or sold.
- No Drop items cannot be dropped, traded, or sold.
- Item Lock blocks auction.
- Items in trade cannot be modified or auctioned.
- Items for sale must be in the player's bank.
- No Repair items cannot be sold at 0% durability.
- Buyout requires an active sale with a buyout price.
- Players cannot buy their own item.
- If the buyer is already the high bidder, buyout cost is buyout minus current bid.
- Otherwise buyout cost is the full buyout.

### Ship bidding and buyout

`CanBidOnShip(...)` and `CanBuyoutShip(...)` mirror item auction behavior with ship-specific wording.

Stable behavior:

- The ship must pass `CanShipBeAuctioned(...)`.
- The ship must be for sale.
- Players cannot bid on or buy their own ship.
- Buyout-only sales must be bought out, not bid on.
- A bid must be lower than buyout when a buyout exists.
- Max bid must be between 0 and 999,999,999 Credits.
- If the current player is already the high bidder, a new max bid must be higher than the previous max bid and only the increase is owed.
- If no bidder exists and the auction is in preview mode, bidding is blocked until preview ends.
- Otherwise, bid must meet the computed minimum next bid.
- Ship buyout requires a buyout price.
- If the buyer is already high bidder, buyout cost is buyout minus current bid; otherwise it is the full buyout.

Needs confirmation:

- Preview mode uses a 6-day threshold in the method. Public wording should confirm how this maps to displayed auction duration.

## 23. Jump Gates, Jettison, and Loot Interaction Gates

Useful source file:

- `IKOLEGFOADL.cs`

### Jump Gates

`CanUseJumpGate(...)` validates direct jump-gate use.

Stable behavior:

- The ship must pass the shared my-ship validator.
- Corp Defender ships are blocked by the shared validator.
- Battery must be at least 75% charged.
- The ship must not be waiting on the combined jump/move timer fields; the client displays the remaining seconds.
- The current sector must have a jump gate target.
- The destination map is taken from the sector's jump gate destination.

Public use:

- The Starmap or Movement reference can document the 75% battery gate.

Needs confirmation:

- The two timer fields summed before jump use should be named from movement/jump extraction before public wording mentions exact timer types.

### Jettisoning items

`CanJettisonItem(...)` validates dropping/ejecting items into the current sector.

Stable behavior:

- The acting ship must be deployed and valid.
- Corp Defender ships are blocked by the shared ship validator.
- Temporary item rarity upgrades block the action through the shared ship validator.
- The item must pass the player's item validator.
- Item Lock blocks jettison.
- Items in trade cannot be ejected.
- The ship must have a valid location.
- Items cannot be dropped in Arena sectors.
- Some drop-sensitive items have extra restrictions:
  - Cannot be dropped on enemy defense units.
  - Cannot be dropped at 0% durability.
  - Cannot be dropped in some special solar system states.
  - Cannot be dropped on a jump gate.

Public use:

- Item management pages can document this once item categories with the extra drop-sensitive flag are identified.

Needs confirmation:

- Identify the item flag used for the extra drop restrictions before naming the category publicly.

### Looting cargo

`CanLoot(...)` validates looting with `ValidateTargetedAction(...)`, then dispatches by cargo entity type.

Observed cargo types:

- Cargo Money
- Cargo Item
- Cargo Resource

Public use:

- Cargo and loot pages can say the client treats these as distinct target types, but the detailed per-type loot validators still need a deeper pass.

## Public Page Candidates

Potential public updates from this pass:

- `Ships.md` or a Fleet Limits page: deploy, recall, scrap, and ship sale restrictions.
- `Corporations.md`: invite, create, rename, rank, and member-cap rules.
- `Alliances.md`: alliance invite/kick/leave rules, citizen cap, corporation cap, Relic Shrine cap.
- `Market.md` or Economy page: auction limits, bid/buyout rules, item/ship sale restrictions.
- `Movement.md` or Starmap page: jump gate requirements.
- `Items.md` or Item Management page: jettison restrictions.

## Needs Confirmation List

- Configured maximum fleet size and next-ship level table should be sourced from config extraction.
- Configured corporation creation and rename Tech Point costs.
- Configured alliance corporation cap and citizen cap.
- Configured citizen player level.
- Whether the literal 10 Relic Shrine alliance cap is still server-authoritative.
- Auction preview mode display behavior.
- Public category name for drop-sensitive/jettison-restricted items.
- Per-type cargo loot validators for money, item, and resource cargo.
