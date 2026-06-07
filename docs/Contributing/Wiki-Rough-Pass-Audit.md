# Wiki Rough-Pass Audit

This page records the first broad cleanup pass across the wiki and training data. It is not a final accuracy review. Treat it as a working list of risks and next actions.

---

## Cleanup completed

- Normalized Markdown and YAML text to plain ASCII punctuation to avoid display issues in terminals and editors.
- Wrapped internal Markdown links whose paths contain parentheses, such as `Player vs Player (PVP)`, in angle brackets.
- Replaced the unsupported Security Rating placeholder table with a source-backed page and a data-needed table.
- Expanded Equip Points, Technology, and Skills enough to remove "coming soon" language while keeping detailed mechanics on their canonical pages.
- Added player-written quick-start guides for cattabliss systems material and LuckyMFer's Arena notes.
- Added canonical pages for recommended settings, common chat commands, and Fleet PvP operations.
- Hid old empty duplicate `Entities/Items`, `Entities/Ships`, and unused corporation stub pages from navigation while leaving files in place for a later deletion/redirect decision.
- Added Pass 2 new-player workflow pages: `Getting-Started/Common-Workflows.md`, expanded `How-To-Play.md`, and tightened FAQ answers to link to canonical pages.
- Added Pass 3 PvE/economy pages: expanded `Gameplay/Missions.md`, added `Open World Farming.md` and `NPC Busts.md`, filled PvE navigation, and removed fixed market-price guidance from currency pages.
- Added Pass 4 PvP/Alliance War pages: filled `Structure Busts.md` as a rules page, added PvP navigation, expanded `Skulls.md` with observed open-world reward rules, and moved PvP/structure strategy into the root `Strategy/` section.
- Added Pass 5 advanced pages: `Items/Specials.md`, `Items/Tech-Computers.md`, `Strategy/Build-Philosophy.md`, `Strategy/Computer-Deconstruction.md`, and `Strategy/Faction-Ship-Notes.md`. Kept exact formulas as Needs data where current sources are guide/chat notes rather than verified mechanics.
- Added cleanup pass after the five planned passes: removed root catch-all navigation, curated World/Maps navigation, hid legacy folders, emptied hidden placeholder files so they are ready for future data, and added contributor changelog notes.

---

## Major structural findings

| Finding | Risk | Suggested action |
|---------|------|------------------|
| Legacy pages exist under `docs/Entities/Ships/`, `docs/Entities/Items/`, and `docs/New Player Guide/`. | Contributors may edit the wrong location or create duplicate pages. | Fixed for now: these are hidden from navigation and now point to canonical pages instead of being empty. Decide later whether to delete them or keep them as redirect-style search landing pages. |
| Placeholder pages exist in miscellaneous entities, PvP activity subpages, exploration, and spawnables. | Empty pages may appear in search or future navigation without useful content. | Fixed for now: hidden placeholder files are intentionally empty until sourced. |
| Old planning docs still exist for old links. | Contributors may follow old tasks that are already complete. | Fixed for now: `Wiki-Fill-Out-Plan.md`, `Wiki-Status.md`, and `Wiki-Review-What-We-Are-Missing.md` are short retired notes and are no longer in contributor navigation. |
| Several pages summarize mechanics that have dedicated pages. | Future changes can drift when the same rule is edited in one place but not another. | Apply the canonical page rule in [Content Standards](Content Standards.md). |

---

## Information likely unsupported or needing verification

| Page | Claim or area | Why it is risky | Action |
|------|---------------|-----------------|--------|
| `World/Maps/Security Rating.md` | Exact NPC counts and recommended hull tiers. | Current client now confirms broad NPC level bands, but does not provide observed ship counts or player-ready recommendations. | Added client level bands; keep counts and recommendations as "Needs data." |
| `Entities/Currencies/Skulls.md` | Typical market value of `~700-800 Credits per Skull`. | Market values are time-sensitive and not durable wiki data. | Fixed: replaced with general market-dependent language. |
| `Entities/Currencies/Star Shards.md` | Star Shard exchange details and cosmetic uses. | The in-game wiki export in this repo does not appear to cover Star Shards in detail. | Verify in game before treating as canonical. |
| `Ships/Ship-Mods.md` / Freighter | Exact Freighter harvesting behavior. | In-game wiki says "doubles harvesting chances"; gootchat says "2x normal amount". | Left as harvesting improvement with Needs data note in Open World Farming until confirmed. |
| `Gameplay/Oblivion-Server.md` | Specific death, durability, and loot multiplier values. | Checked against the in-game wiki export. | Fixed: page now reflects the exported Oblivion rules without source-facing wording. |
| `Gameplay/Activities/Player vs Player (PVP)/Arena.md` | Arena schedule, rewards, modes, and gear-score thresholds. | In-game wiki gives broad Arena rules; Discord notes add more detail and may be current but should be treated as community data. | Fixed for now: 1,000 Gear Score is documented as the queue minimum; full-reward thresholds remain noted as higher and UI-checkable. |
| `Strategy/Structure-Busting.md` | Tactical structure-bust advice and low-GS/effective-structure ideas. | Strategy can shift with meta and balance changes. | Kept outside Gameplay/reference pages; hard rules stay on Structures/Skulls. |
| `Gameplay/Abilities/Grapple.md`, `Hacking.md`, `Drain.md` | Exact formulas and resist thresholds. | Duration/amount formulas and resist breakpoints need live verification. | Fixed for now: public pages keep stable gates, cooldowns, and technology effects while marking exact formulas as Needs data. |
| `Items/Weapons.md` | Weapon-slot and Elite Rank examples. | Some content may be inferred from Elite Rank data rather than directly sourced to Weapons. | Fixed for now: page links to Elite Ranks, documents attack readiness broadly, and avoids duplicating slot tables. |
| `Items/Specials.md` | Exact Special formulas, cooldowns, and rank/rarity breakpoints. | Discord guide notes identify many Specials, but several need current in-game verification. | Added reference list with Needs data flags and links to stable ability pages. |
| `Items/Tech-Computers.md` | Exact Tech Computer stat packages and rarity point values above Rare. | Training data gives unlock cadence but not all stat tables. | Added deconstruction rules and moved planning advice to Strategy. |
| `Strategy/Faction-Ship-Notes.md` | Wyrd shield/capacitor formulas and faction ship comparisons. | Gootchat has useful observations, but they are not yet verified as exact mechanics. | Kept as strategy/source notes; faction pages link out instead of treating them as canonical formulas. |

---

## Training data not yet fully used

The Discord training data contains useful material that is not yet represented as dedicated wiki content:

| Topic | Possible destination | Notes |
|-------|----------------------|-------|
| Recommended settings for new players | `Getting-Started/Settings.md` and quick-start guides | Added; exact UI labels should still be checked in game after major UI patches. |
| Freegift command and Mark upgrade kit | `Getting-Started/Chat-Commands.md` | Added with a command-verification warning because it may change. |
| Lead assist / driver following | `Gameplay/Activities/Player vs Player (PVP)/Fleet-PvP.md`, `Strategy/Fleet-PvP.md`, and quick-start guides | Rules and UI concepts are in Gameplay; tactics are in Strategy. |
| Common click-path workflows | `Getting-Started/Common-Workflows.md` | Added for settings, gifts, repairs, travel, Arena, and fleet assist. |
| CPU / computer deconstruction | `Items/Tech-Computers.md` and `Strategy/Computer-Deconstruction.md` | Added reference rules and separate planning guidance. Exact stat tables still need verification. |
| Specials overview | `Items/Specials.md` | Added reference list for Technician, Prospector, Advanced Munitions, Scout, Stalker, Advanced Propulsion, Alien Hunter, Hacker, Grappling Hook, Nova, Deflector, Vampire, Battle Ram, Advanced Construct, Drone Master, Advanced Shields, Tank, etc. |
| PvP gearing advice | `Getting-Started/Quick-Start-Guides/` and `Strategy/Fleet-PvP.md` | Added as guide/community operational material, not universal build law. |
| Structure warfare strategy | `Strategy/Structure-Busting.md` | Added as strategy guide; reference rules stay on Structures and Skulls. |
| Mission reward details and refresh behavior | `Gameplay/Missions.md` | Discord notes include rewards, refresh limits, and strategy. Verify before adding. |
| Mission planning strategy | `Strategy/Missions.md` | Moved out of Gameplay mission reference. |
| Open-world farming and NPC busts | `Gameplay/Activities/Player vs Environment (PVE)/` plus `Strategy/` | Rules/reference in Gameplay; tactics and economy guidance in Strategy. |
| Faction/build notes | `Strategy/Faction-Ship-Notes.md` and `Strategy/Build-Philosophy.md` | Added as community guidance, with Wyrd shield mechanics marked for confirmation. |

---

## Suggested next pass

1. Audit high-risk precise mechanics before expanding them.
2. Convert unused Discord training data into guide pages, with "community note" labels where needed.
3. Fill intentionally empty hidden placeholder files only when verified data exists and the page has a clear canonical purpose.
