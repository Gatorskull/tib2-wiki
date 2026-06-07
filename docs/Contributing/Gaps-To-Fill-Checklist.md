# Gaps to Fill -- Information to Collect

Use this as a checklist. For each gap, collect the information listed; once you have it, we can update the wiki.

---

## 1. Security Rating (World/Maps/Security Rating.md)

**What we need:** Fill the remaining non-client fields for each SR (1-9). The current client now confirms broad NPC level bands; we still need observed sector counts and practical readiness guidance.

For **each** Security Rating (SR1 through SR9), please collect:

| Field | Example (current placeholder) | Your data |
|-------|-------------------------------|-----------|
| NPC ship level range | Client band exists; verify if live behavior differs | |
| Max NPC ships per sector | e.g. SR1: 3 | |
| Recommended player level range | e.g. 1-10 | |
| Recommended ship hull tier | e.g. T1-T2 | |
| Any special notes | e.g. "Starter-friendly" | |

**Where to get it:** In-game observation, dev/patch notes, or community notes. If exact numbers aren't available, "best guess" ranges are fine -- we'll mark them as indicative.

---

## 2. Equip Points (Ships/Equip-Points.md)

**What we need:** Add verified Equip Point tables or examples when available.

**Client extraction update:** The current client confirms that a gear set's required EP is `max(0, sum(item EP cost) - sum(item EP bonus))`. It also gives base ship EP by ship class and faction, plus item EP cost formulas for several item families. We still need exact item rank/base `Ep` tables and defense-unit EP max tables.

Please collect (if available):

| Item | Notes |
|------|--------|
| **EP by ship class** | How many Equip Points each ship class (or size) has (e.g. Shuttle 10, Frigate 15, ...). |
| **EP by ship tier/level** | Does EP change with ship level or tier? |
| **Defense unit EP** | How EP works for Planets, Garrisons, Outposts, Shipyards (base and per level if applicable). |
| **Item rank/base Ep tables** | The formulas are known, but exact rank/base `Ep` values for weapons, armor, storage, and shields are still needed. |

**Where to get remaining data:** In-game item inspect, defense unit inspect, in-game wiki, HELP, or deeper client extraction. Ship base EP is now source-backed in `Client-Extraction-Notes.md`.

---

## 3. Technology (Gameplay/Technology.md)

**What we need:** Enough to replace "We'll add a categorized overview here" with real content.

**Client extraction update:** The current client contains the technology enum, display names, descriptions, daily-tech descriptions, and helper methods for stackability/research/artifact/boost/defense eligibility. A raw source-backed staging table now exists in `Client-Extracted-Technology.md`.

Please collect (any that you can):

| Item | Notes |
|------|--------|
| **Categories** | How techs are grouped in-game (e.g. Hull, Weapons, Movement, Crafting). |
| **Public grouping** | Decide which client-extracted techs should become public reference pages versus advanced/strategy notes. |
| **Ranked vs non-ranked** | Helper methods exist in the client, but still need to be mined into a public-ready table. |
| **Sources** | Which techs come from Artifacts vs corp research vs items vs ships (brief list or examples). |

**Where to get remaining data:** Client helper-method extraction for flags, plus in-game HELP/in-game wiki for public grouping and source wording.

---

## 4. Skills (Gameplay/Skills.md)

**What we need:** Enough to replace "Full skill list and recommendations will be added here" with real content.

**Client extraction update:** The current client confirms the skill-upgrade stat list and basic/advanced mod-per-point values. We still need public wording and any max-point/point-source rules before replacing the page.

Please collect (any that you can):

| Item | Notes |
|------|--------|
| **Skill list** | All (or main) captain/ship/corp skills and what they do (e.g. +XP%, Evasion, Hull). |
| **Max points per stat** | e.g. "Up to 10 points per stat, reduced benefit above 5." |
| **New-player recommendations** | 3-5 "get these first" skills (e.g. +XP%, Evasion) and why. |
| **Where points come from** | Leveling, Artifacts, etc. (we already mention Artifacts; confirm or add). |

**Where to get it:** In-game skill tree, in-game wiki, or community guides.

---

## 5. Weapons (Items/Weapons.md) -- optional

**What we need:** Only if you want to go beyond the current overview.

**Client extraction update:** Weapon class display names, alternate variant names, and faction mappings are now staged in `Client-Extracted-Items.md`. We still need the gameplay meaning of the alternate weapon-name argument and exact stat/EP values.

**Stat extraction update:** Runtime item-family stat coverage is staged in `Client-Extracted-Item-Stat-Coverage.md`. We now know which item families have client logic for each stat, but not yet the normalized per-class formulas.

**Formula extraction update:** Raw shield, engine, and battery formula bodies are staged in `Client-Extracted-Item-Stat-Formulas-Narrow.md`. These still need helper-method translation and public wording.

Please collect (optional):

| Item | Notes |
|------|--------|
| **Damage types** | e.g. Kinetic, Energy, etc., if the game shows them. |
| **Weapon tiers/ranks** | How weapon rank affects damage or EP cost. |
| **Formula normalization** | Turn the client stat override methods into clean per-family/per-class tables. |

**Where to get it:** In-game weapon stats, item inspect, or wiki.

---

## 6. Starmap (optional new page)

**What we need:** Only if you want a dedicated **Starmap** page (we already have World index + Maps).

Please collect (optional):

| Item | Notes |
|------|--------|
| **System list** | Names of solar systems (or "50+ systems" and a few examples). |
| **How to open Starmap** | e.g. "Hamburger menu -> Starmap". |
| **What the map shows** | Faction colors, security, jump gates, etc. (we have some of this in Maps; any extra). |

**Where to get it:** In-game Starmap UI and in-game wiki.

---

## 7. Player Guides (Getting Started/Player-Guides.md) -- optional

**What we need:** Only if you want to remove the "Guides in progress" box and lock the list.

| Item | Notes |
|------|--------|
| **Final list** | Which community guides to keep (with titles + URLs). |
| **Short description** | One line per guide (e.g. "New player basics", "Gear and builds"). |

---

## Quick reference: where each goes

| Gap | Wiki page to update |
|-----|----------------------|
| Security Rating data | `docs/World/Maps/Security Rating.md` |
| Equip Points details | `docs/Ships/Equip-Points.md` |
| Technology list/categories | `docs/Gameplay/Technology.md` |
| Skills list/recommendations | `docs/Gameplay/Skills.md` |
| Weapons damage/tiers (optional) | `docs/Items/Weapons.md` |
| Starmap (optional) | New: `docs/World/Starmap.md` or expand `docs/World/index.md` |
| Player guides list (optional) | `docs/Getting-Started/Player-Guides.md` |

---

## Priority order (suggested)

1. **Security Rating** -- One table per SR; high impact for players.
2. **Equip Points** -- A few verified numbers or examples so we can expand the page beyond the basic source-backed overview.
3. **Technology** -- Categories + list (or export) so we can add an overview.
4. **Skills** -- List + new-player tips so we can add content.
5. **Weapons / Starmap / Player guides** -- Optional; collect if you have time.

When you have the data, you can paste it here (or in a comment) and we can turn it into wiki text and update the pages.
