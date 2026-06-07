# Content Standards

Use this page when creating or revising wiki content. The goal is to keep the wiki accurate, easy to maintain, and free of repeated or invented mechanics.

---

## Source priority

Use sources in this order:

1. **Current client extraction** for mechanics, formulas, validators, item/ship data, and action gates.
2. **Current in-game observation** from players for UI names, behavior that requires server validation, and live-game confirmation.
3. **In-game wiki export** in `Gathered Training Data/In Game WIKI.md` for player-facing descriptions and older official wording.
4. **Developer posts, patch notes, or official Spellbook material** for intent, feature history, and named systems.
5. **Authored guide prose** from trusted contributors, especially cattabliss, for guide pages and polished explanations.
6. **Community notes or Discord training data** for leads, examples, and strategy.

If sources conflict, do not silently merge them. Use the strongest source for the page type, then mark the conflict in a contributor note or audit page.

Client extraction is strong for "what the client checks" but not perfect for everything. It can contain obfuscated junk strings, client-only previews, and gaps where the server has the final say. If a value or rule comes from unclear decompiled code, mark it **Needs confirmation** instead of publishing it as settled fact.

---

## Canonical page rule

Each mechanic should have one canonical page.

Write the full explanation on that page, then link to it from other pages. Do not rewrite the same rules in multiple places.

Strategy should live outside Gameplay/reference pages. Use the root `docs/Strategy/` section for tactical advice, build philosophy, current meta notes, or community guidance. Gameplay/reference pages may link to Strategy pages, but should not contain the strategy themselves.

Canonical page map:

| Mechanic | Canonical page |
|----------|----------------|
| Ship overview, fleet size, deploy slot level gates | `docs/Ships/index.md` |
| Ship classes and size categories | `docs/Ships/Size-And-Targeting.md` |
| Equip Points | `docs/Ships/Equip-Points.md` |
| Elite ranks and Striker progression | `docs/Ships/Elite-Ranks.md` |
| Ship construction | `docs/Ships/Ship-Crafting.md` |
| Carrier fleet movement | `docs/Ships/Carrier-Leadership.md` |
| Ship mods | `docs/Ships/Ship-Mods.md` |
| Interdictor Carrier | `docs/Ships/Interdictor-Carrier.md` |
| Deception Module | `docs/Ships/Deception-Module.md` |
| Hardcore ships | `docs/Ships/Hardcore-Units.md` |
| Retro skins | `docs/Ships/Retro-Skins.md` |
| Item overview and item types | `docs/Items/index.md` |
| Stats | `docs/Items/Stats.md` |
| Diminishing returns | `docs/Items/Diminishing-Returns.md` |
| Equipment slot auxiliary behavior | `docs/Items/Equipment-Slots.md` |
| Item rank, rarity, quality, and repairs | `docs/Items/Item-Upgrades.md` |
| Item management restrictions | `docs/Items/Item-Management.md` |
| Item crafting | `docs/Items/Item-Crafting.md` |
| Void items | `docs/Items/Void-Items.md` |
| Mutate Item Kit | `docs/Items/Mutate-Item-Kit.md` |
| Pity loot | `docs/Items/Pity-Loot.md` |
| Weapons | `docs/Items/Weapons.md` |
| Drones | `docs/Items/Drones.md` |
| Special items | `docs/Items/Specials.md` |
| Tech Computers and CPU deconstruction | `docs/Items/Tech-Computers.md` |
| Gravity Drives | `docs/Items/Gravity-Drives.md` |
| Skills | `docs/Gameplay/Skills.md` |
| Technology | `docs/Gameplay/Technology.md` |
| Missions | `docs/Gameplay/Missions.md` |
| Combat and targeting | `docs/Gameplay/Combat-and-Targeting.md` |
| Outpost missions | `docs/Gameplay/Activities/Outpost-Missions.md` |
| Abilities | `docs/Gameplay/Abilities/index.md` and child pages |
| PvE activity rules | `docs/Gameplay/Activities/Player vs Environment (PVE)/index.md` and child pages |
| PvP rules | `docs/Gameplay/Activities/Player vs Player (PVP)/index.md` |
| Arena rules | `docs/Gameplay/Activities/Player vs Player (PVP)/Arena.md` |
| Events | `docs/Gameplay/Events/index.md` and child pages |
| Sectors, collision, and following | `docs/World/Maps/Sectors.md` |
| Spawnables, exploration, security rating | `docs/World/Maps/` |
| Factions | `docs/World/Factions/index.md` and child pages |
| Structures | `docs/Entities/Structures/index.md` and child pages |
| Artifacts | `docs/Entities/Structures/Artifacts.md` |
| Corporations and alliances | `docs/Entities/Corporations/index.md` and child pages |
| Currencies | `docs/Entities/Currencies/index.md` and child pages |
| New player flows and settings | `docs/Getting-Started/` |
| Quick-start guides | `docs/Getting-Started/Quick-Start-Guides/` |
| Strategy and community tactics | `docs/Strategy/` |

Legacy/duplicate entity pages should be treated carefully. If a mechanic exists in both `docs/Ships/` and `docs/Entities/Ships/`, or both `docs/Items/` and `docs/Entities/Items/`, prefer the newer top-level `docs/Ships/` and `docs/Items/` canonical pages unless we deliberately decide to reorganize that section. Do not expand both copies with the same explanation.

Short summaries are fine, but they should point to the canonical page for details.

---

## Repetition rule

Before adding a paragraph, ask:

- Does a dedicated page already explain this?
- Would changing this information later require editing more than one page?
- Is this page trying to be a guide, a reference, or an index?

If the answer is yes, shorten the text and link out.

Good pattern:

```md
Equip Points limit how much gear a ship can mount. See [Equip Points](../Ships/Equip-Points.md).
```

Avoid:

```md
Equip Points are the capacity your ship has for weapons, armor, shields...
```

unless the page itself is the Equip Points page.

When a page needs context, use one or two sentences and link to the canonical page. If the content would require a table, formula, full rule list, or exception list, it belongs on the canonical page.

Good pattern:

```md
Ship construction can require corp membership time, relics, Skulls, resources, and a valid Shipyard. See [Ship Crafting](../Ships/Ship-Crafting.md).
```

Avoid copying the full ship construction gate stack into corporation, relic, skull, and shipyard pages.

---

## Rules vs strategy

Reference/gameplay pages explain what the game does. Strategy pages explain what players recommend doing.

Put content in a rule page when it answers:

- What is this system?
- What are the requirements?
- What does the client validate?
- What numbers or formulas are known?
- What is still unknown?

Put content in `docs/Strategy/` when it answers:

- What should I build?
- What is best or efficient?
- How do players usually counter this?
- What is the current meta?
- What should a new player prioritize?

Rule pages may have a `See also` link to strategy. Strategy pages may summarize a mechanic briefly, then link back to the canonical rule page.

---

## Accuracy rule

Do not present guesses as facts.

Use player-facing rarity names in public wiki text and tables: **Common**, **Uncommon**, **Rare**, **Ultra-Rare**, **Elite**, **Legendary**, and **Ultimate**.

Internal enum labels may appear in hidden contributor extraction notes only when quoting or preserving raw source context. Do not use numbered rarity shorthand in public pages.

Use one of these labels when data is not fully verified:

- **Needs data** for missing values.
- **Estimated** for community-tested but not official values.
- **Observed** for values seen in game but not confirmed as universal.
- **Source needed** for claims copied from a rough pass without a clear source.

Remove placeholder numbers rather than publishing them as if they were real.

Use these source tags sparingly when they help:

- **Client-confirmed** for rules directly supported by the current client extraction.
- **Observed** for live behavior seen in game.
- **Community guidance** for advice or meta claims.
- **Needs confirmation** for unclear decompiled branches, server-side uncertainty, or source conflicts.

Avoid filling public pages with source tags on every sentence. Use them where the reader could otherwise mistake uncertainty for a settled rule.

---

## Training-data rule

When converting training data into wiki content:

- Keep durable mechanics.
- Avoid copying personal opinions into reference pages.
- Convert advice into neutral guidance.
- Preserve source nuance when data is uncertain.
- Prefer a dedicated guide page for strategy-heavy Discord notes.

Discord training data is useful, but it is rough. Treat it as community notes until confirmed.

### Authored guide prose

Some Discord training-data sections were written as polished guide prose by known contributors. In particular, **cattabliss** is a professional writer and has written several guide sections that should be respected as authored work.

When a cattabliss section fits a wiki page:

- Preserve the wording as-is where practical.
- Keep the structure and explanatory flow when adapting to Markdown.
- Only edit for accuracy, links, formatting, or to avoid duplicating a canonical page.
- If the text is strategy or opinion-heavy, place it in a guide page rather than diluting it into reference prose.

---

## Link rule

Use Markdown links to `.md` source files. For paths with parentheses, wrap the destination in angle brackets:

```md
[PvP](<../Gameplay/Activities/Player vs Player (PVP)/index.md>)
```

See [Markdown Links](Getting Started/Markdown Links.md) for the full linking guide.

---

## Integration checklist

Use this checklist when moving contributor notes into public pages:

1. Pick the canonical page from the map above.
2. Check whether the same rule already exists elsewhere.
3. Move or rewrite the full rule only on the canonical page.
4. Replace duplicate explanations with short summaries and links.
5. Keep strategy out of rule pages.
6. Mark unresolved formulas or suspicious decompiled branches as **Needs confirmation** or **Needs data**.
7. Preserve cattabliss guide prose where it fits, especially in guide or strategy pages.
8. Add `See also` links instead of repeating connected mechanics.
9. Update navigation only when a page should be public and easy to browse.
10. Leave contributor mining notes hidden unless they are being intentionally surfaced.

---

## Page shape

Most pages should follow this pattern:

1. One-sentence definition.
2. Core rules or table.
3. Practical notes only if they are stable.
4. Contributor note if data is missing or uncertain.
5. See also links to canonical related pages.

Index pages should summarize and link. They should not become duplicate reference pages.
