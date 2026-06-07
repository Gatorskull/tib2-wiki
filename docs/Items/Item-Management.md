# Item Management

Item management covers what can be repaired, modified, scrapped, deconstructed, traded, sold, or moved to shared storage. Use [Item Upgrades](Item-Upgrades.md) for rank, rarity, quality, and repair actions; use this page for restrictions that decide whether an item action is allowed.

## Common Restrictions

Many item actions are blocked when the item is in a special state:

| State | What it blocks |
|-------|----------------|
| Missing or deleted item | The item cannot be modified. |
| Item Lock | Blocks scrap, deconstruct, auction, and moving to corporation bank. |
| Listed for sale | Cancel the listing before scrapping, deconstructing, or modifying the item. |
| In trade | Items currently in trade cannot be modified. |
| Temporary rarity upgrade | Temporarily upgraded items cannot be scrapped or deconstructed. |
| Equipped in Arena queue or Arena | Equipped items cannot be modified while the owning ship is queued for Arena or inside Arena. |

Some actions also require the item to be owned by the player and in the correct location, such as inventory or bank.

## Repairs

Equipment can lose durability when ships die. At **0% Durability**, an item cannot be equipped until repaired.

| Repair path | Notes |
|-------------|-------|
| Item inspect -> **Upgrade** -> **Repair** | Repairs the item to full durability, but normal repair can reduce item quality. |
| `:corp repair mytp confirm` | Repairs 5 random equipped items by 10% for every online corporation member and spends Tech Points. |
| `:alliance repair mytp confirm` | Repairs 2 random equipped items by 10% for every online alliance member and spends Tech Points. |

Repair is blocked if the item is already at 100% durability or if the item cannot be repaired. On the [Oblivion Server](../Gameplay/Oblivion-Server.md), item repair is disabled.

## Rank and Rarity Actions

Rank Up and Rank Down are limited to:

- Weapons
- Armor
- Storage
- Shields

Rank Up is blocked when the item's base Equip Point cost is already at the upper limit. Rank Down is blocked when the base Equip Point cost is already at the lower limit.

Rarity upgrades are blocked for Basic items and Ultimate items. On the [Oblivion Server](../Gameplay/Oblivion-Server.md), items cannot be upgraded to Ultimate with Tech Points.

For upgrade effects and known cost gaps, see [Item Upgrades](Item-Upgrades.md).

## Scrap and Deconstruct

Scrapping turns items or resources into Credits. Deconstruction is used for some progression systems, such as [Tech Computers](Tech-Computers.md) and Special blueprints.

Deconstruction is blocked when:

| Restriction | Notes |
|-------------|-------|
| Crafted item | Crafted items cannot be deconstructed. |
| Free starter item | Free starter items cannot be deconstructed. |
| No deconstruction value or chance | Items with no deconstruction result cannot be deconstructed. |
| Temporary rarity upgrade | Temporarily upgraded items cannot be deconstructed. |
| Item Lock, trade, or sale listing | Clear the blocking state first. |

Some consumables cannot be scrapped. Free starter items cannot be scrapped until the player reaches level 3.

## Corporation Bank

Moving an item to the corporation bank requires:

- The player must be in a corporation.
- The corporation bank must have space.
- The item cannot be locked.

Corp-bank storage is shared. Treat deposits as a corporation action, not a personal bank extension.

## Market and Auctions

Auctionable items must be in the player's inventory and cannot be:

- Free starter items
- No-drop items
- Locked items
- Items currently in trade

Items for sale must be in the player's bank. Items with **No Repair** cannot be sold at 0% durability.

Buyout requires an active auction with a buyout price. A player cannot buy out their own auction. If the buyer is already the high bidder, the buyout cost is reduced by their current bid; otherwise the full buyout price is due.

## Free Starter and Bound Items

Free starter items and ships have extra restrictions. Starter items cannot be used in some activities, such as [The Arena](<../Gameplay/Activities/Player vs Player (PVP)/Arena.md>), and cannot be equipped to defense units or Hardcore units.

Account-bound ships and free starter ships cannot be bought, traded, or sold.

## See Also

* [Items](index.md)
* [Item Upgrades](Item-Upgrades.md)
* [Tech Computers](Tech-Computers.md)
* [Credits](../Entities/Currencies/Credits.md)
* [Tech Points](../Entities/Currencies/Tech Points.md)
* [Chat Commands](../Getting-Started/Chat-Commands.md)
