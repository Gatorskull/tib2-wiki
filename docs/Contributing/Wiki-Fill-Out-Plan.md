# Wiki Fill-Out Plan

This document is the **detailed plan** to populate the TIB2 wiki: which topics become which files, how they interlink, and in what order to add content. Use it together with **AI-Context-Guide.md** and **Gathered Training Data/In Game WIKI.md**.

For a quick **done vs. left** snapshot, see [Wiki Status](Wiki-Status.md).

---

## 1. Topic-to-File Map (In Game WIKI → docs/)

Map each `[[[TopicName]]]` from **In Game WIKI.md** to a target path under **docs/**.

### 1.1 Core / Getting Started (new or existing)

| In-Game Topic | Target Path | Notes |
|---------------|-------------|--------|
| How To Play | `docs/Getting-Started/How-To-Play.md` or `docs/New-Player-Guide.md` | Consider merging with New Player Guide |
| FAQ | `docs/Getting-Started/FAQ.md` | Convert Q&A; link to relevant deep-dive pages |
| Player Guides | `docs/Getting-Started/Player-Guides.md` | Curated list + external links |
| Device Sharing and Multiple Accounts | `docs/Getting-Started/Device-Sharing-And-Accounts.md` | Policy page |
| Review The Game | `docs/Getting-Started/Review-The-Game.md` | Short; link to stores |
| Oblivion Server Rules | `docs/Gameplay/Oblivion-Server.md` or `docs/World/Oblivion-Server.md` | Distinct ruleset; link from Gameplay & World |

### 1.2 World & Navigation

| In-Game Topic | Target Path | Notes |
|---------------|-------------|--------|
| The Starmap | `docs/World/Starmap.md` or expand `docs/World/index.md` | Overview of systems and factions |
| Security Rating (maps) | **Existing** `docs/World/Maps/Security Rating.md` | Expand from placeholder tables |
| Maps (general) | **Existing** `docs/World/Maps/index.md` | Replace placeholder; link to Security Rating, Sectors |
| Sectors / Collision | `docs/World/Maps/Sectors.md` | Referenced from World/index; create if missing |
| Jump Gates | **Existing** `docs/Entities/Structures/Jump Gates.md` | World/index links here; keep under Entities or add alias under World |
| The Wyrd Alien Faction | `docs/World/Factions/Wyrd.md` | New Factions subfolder |
| The Het Alien Faction | `docs/World/Factions/Het.md` | |
| The Precursor Alien Faction | `docs/World/Factions/Precursor.md` | |
| The Pirate Faction | `docs/World/Factions/Pirates.md` | |

### 1.3 Entities

| In-Game Topic | Target Path | Notes |
|---------------|-------------|--------|
| Corporations | **Existing** `docs/Entities/Corporations/index.md` | Expand from In Game WIKI "Corporations" block |
| Corporation Defense Structures | **Existing** Structures section | Split or expand: Planets, Garrisons, Outposts, Shipyards (already have .md each) |
| Corporate Defender Ships | `docs/Entities/Corporations/Corporate-Defenders.md` or `docs/Gameplay/Corporate-Defenders.md` | Cross-link Entities ↔ Gameplay |
| Credits | **Existing** `docs/Entities/Currencies/Credits.md` | |
| Skulls | **Existing** `docs/Entities/Currencies/Skulls.md` | |
| Tech Points | **Existing** `docs/Entities/Currencies/Tech Points.md` | |
| Star Shards | **Existing** `docs/Entities/Currencies/Star Shards.md` | |
| Relics | `docs/Entities/Currencies/Relics.md` or `docs/Entities/Resources/Relics.md` | Relic Shrines, capture, allocation |
| Artifacts | `docs/Entities/Structures/Artifacts.md` or `docs/World/Artifacts.md` | Tech bonus + study skill point |

### 1.4 Ships & Equipment

| In-Game Topic | Target Path | Notes |
|---------------|-------------|--------|
| Ships | **New** `docs/Ships/index.md` | Fleet size, captain levels, 10 classes, 50 faction variants |
| Ship & Defense Unit Size | `docs/Ships/Size-And-Targeting.md` | Size, movement, targeting, Small Strike Team |
| Ship Crafting | `docs/Ships/Ship-Crafting.md` | Corp shipyards, blueprints, resources, Skulls/Relics |
| Ship Mods | `docs/Ships/Ship-Mods.md` | Medic, Gladiator, Phoenix, Raider, Interdictor, Freighter, Paladin, Ultimate |
| Elite Ranks | `docs/Ships/Elite-Ranks.md` | Skull cost, Striker Gunboat progression |
| Equip Points | `docs/Ships/Equip-Points.md` or `docs/Entities/Equip-Points.md` | Cross-link Items |
| Hardcore Ships & Defense Units | `docs/Ships/Hardcore-Units.md` | Opt-in, bonuses, drop rules |
| Retro Ship Skins | `docs/Ships/Retro-Skins.md` | Sources (events, Steam, rewards) |
| Item Types | **New** `docs/Items/index.md` | Weapon, Armor, Shield, Battery, Storage, Drone, Engine, Computer, Special; Gear Score |
| Stats | `docs/Items/Stats.md` or `docs/Gameplay/Stats.md` | Full stat list from In Game WIKI |
| Item Crafting | `docs/Items/Item-Crafting.md` | Blueprints, quality, skill categories |
| Pity Loot Drops | `docs/Items/Pity-Loot.md` or `docs/Gameplay/Pity-Loot.md` | |
| Void Items | `docs/Items/Void-Items.md` | |
| Mutate Item Kit | `docs/Items/Mutate-Item-Kit.md` | |
| Stat Bonus Diminishing Returns | `docs/Items/Diminishing-Returns.md` or `docs/Gameplay/Diminishing-Returns.md` | |

### 1.5 Abilities & Technology

| In-Game Topic | Target Path | Notes |
|---------------|-------------|--------|
| Technology | `docs/Gameplay/Technology.md` or `docs/Items/Technology.md` | 250+ techs; rank vs non-rank; list in HELP |
| Grapple Ability Action | `docs/Gameplay/Abilities/Grapple.md` | New Abilities subfolder |
| Hacking Ability Action | `docs/Gameplay/Abilities/Hacking.md` | |
| Drain Ability Action | `docs/Gameplay/Abilities/Drain.md` | |
| Technician | `docs/Gameplay/Abilities/Technician.md` | |
| Taunt (Tank) | `docs/Gameplay/Abilities/Taunt.md` | |
| Deflector | `docs/Gameplay/Abilities/Deflector.md` | |
| Junker | `docs/Gameplay/Abilities/Junker.md` | |
| Small Strike Team Bonus | `docs/Gameplay/Small-Strike-Team-Bonus.md` or under Ships | |
| Interdictor Carrier | `docs/Ships/Interdictor-Carrier.md` or under Ship Mods | |
| Deception Module | `docs/Ships/Deception-Module.md` or `docs/Items/Deception-Module.md` | |
| Gravity Drives | `docs/Items/Gravity-Drives.md` | |

### 1.6 Gameplay & Activities

| In-Game Topic | Target Path | Notes |
|---------------|-------------|--------|
| Player vs Player Combat | **Existing** `docs/Gameplay/Activities/Player vs Player (PVP)/index.md` | Expand; link Maps, Skulls, Defense |
| Arena | **Existing** `docs/Gameplay/Activities/Player vs Player (PVP)/Arena.md` | Expand from In Game WIKI |
| Invasions | **Existing** `docs/Gameplay/Activities/Player vs Environment (PVE)/Invasions.md` | Expand PVE index + this page |
| Missions | `docs/Gameplay/Missions.md` | Personal, Corp, Alliance, Universal |
| Alliances | `docs/Entities/Corporations/Alliances.md` or `docs/Gameplay/Alliances.md` | Citizens, caps, defenders |
| Free Daily Gifts | `docs/Gameplay/Events/Free-Daily-Gifts.md` | |
| Holiday Events | `docs/Gameplay/Events/Holiday-Events.md` | |
| Daily Events | `docs/Gameplay/Events/Daily-Events.md` | Love Day, War Day, modifiers |
| Party Boxes | `docs/Gameplay/Events/Party-Boxes.md` | |
| Reward Point Gifts | `docs/Gameplay/Events/Reward-Point-Gifts.md` or under Currencies | |

### 1.7 Meta / External

| In-Game Topic | Target Path | Notes |
|---------------|-------------|--------|
| Spellbook | `docs/About/Spellbook.md` or `docs/Getting-Started/Spellbook.md` | |
| Delete My Account | `docs/Getting-Started/Delete-Account.md` | |
| Spaceball | `docs/Gameplay/Spaceball.md` | Optional; policy note |

---

## 2. New Folders to Create

To support the map above, add these under **docs/**:

| Folder | Purpose |
|--------|---------|
| `docs/Ships/` | index + Size, Ship Crafting, Ship Mods, Elite Ranks, Hardcore, Interdictor, Deception, Retro Skins |
| `docs/Items/` | index (Item Types) + Stats, Crafting, Pity Loot, Void, Mutate, Diminishing Returns, Gravity Drives |
| `docs/Getting-Started/` | How To Play, FAQ, Player Guides, Device Sharing, Review, Spellbook, Delete Account |
| `docs/World/Factions/` | Wyrd, Het, Precursor, Pirates (each with index or single page) |
| `docs/Gameplay/Abilities/` | Grapple, Hacking, Drain, Technician, Taunt, Deflector, Junker |
| `docs/Gameplay/Events/` | Daily, Holiday, Free Gifts, Party Boxes, Reward Point Gifts |
| `docs/Gameplay/` (root-level .md) | Technology, Missions, Alliances, Pity Loot, Diminishing Returns, Oblivion Server, Spaceball (as needed) |

Optional: **docs/About/** for Spellbook and legal/meta pages.

---

## 3. Interlinking Strategy

- **Hubs:** Each section’s **index.md** should list and link to all child topics (like Entities/Currencies and Entities/Structures already do).
- **Cross-section:** When a page mentions another concept (e.g. Skulls, Ships, Corporations), add a Markdown link to the canonical page (relative within section, absolute across sections). See **Markdown Links.md**.
- **Breadcrumbs:** Optional: end each page with a “See also” or “Related” list linking 3–5 related pages.
- **In Game WIKI links:** When converting `<u><link="X">Y</link></u>`, map “X” to the target file in this plan (e.g. “Ships” → `/Ships/index.md`, “Tech Points” → `/Entities/Currencies/Tech Points.md`).
- **Fix broken links:** Homepage currently links to `Ships` and `Weapons`; once **Ships** exists, fix to `[Ships](/Ships/index.md)`. Add **Weapons** under `docs/Items/Weapons.md` or `docs/Ships/Weapons.md` when you have data.

---

## 4. Ordered Steps to Start Filling the Wiki

### Phase 1 — Fix & Foundation (do first)

1. **Create missing section stubs**  
   Add **docs/Ships/index.md** and **docs/Items/index.md** with short placeholder text so the homepage links work. Optionally add **docs/Getting-Started/index.md** and link it from the main nav (e.g. via **docs/.pages**).

2. **Fix homepage links**  
   In **docs/index.md**, change `[Ships](Ships)` and `[Weapons](Weapons)` to proper paths (e.g. `[Ships](/Ships/index.md)`, `[Weapons](/Items/Weapons.md)` or a stub).

3. **Update docs/.pages**  
   Add **Ships**, **Items**, and **Getting-Started** (and any new top-level sections) to **docs/.pages** in the order you want in the sidebar.

### Phase 2 — High-Value, High-Traffic Pages

4. **Getting Started**  
   From In Game WIKI: **How To Play**, **FAQ**. Create `Getting-Started/How-To-Play.md` and `Getting-Started/FAQ.md`; interlink and link to deeper pages (Ships, Corporations, Maps).

5. **Ships overview**  
   Fill **Ships/index.md** from the “Ships” block: 10 classes, fleet size, captain levels, 50 variants, link to Ship Crafting, Elite Ranks, Ship Mods.

6. **Corporations & Alliances**  
   Expand **Entities/Corporations/index.md**; add **Alliances** (page or section). Link to Structures, Artifacts, Relics, Corporate Defenders.

7. **Currencies**  
   Ensure **Credits**, **Skulls**, **Tech Points**, **Star Shards** are complete (already present; enrich from In Game WIKI). Add **Relics** as a page under Entities or Resources.

### Phase 3 — Structures & World

8. **Structures**  
   Expand **Planets**, **Garrisons**, **Outposts**, **Shipyards** (and **Deployment**, **Jump Gates**) from “Corporation Defense Structures” and related blocks. Add **Artifacts** if not under Structures.

9. **World / Maps**  
   Replace **World/Maps/index.md** placeholder. Expand **Security Rating** table; add **Starmap** and **Factions** (Wyrd, Het, Precursor, Pirates) from In Game WIKI.

### Phase 4 — Items & Combat

10. **Items hub**  
    Fill **Items/index.md** (Item Types, Gear Score, drones). Add **Stats** (full list), **Item Crafting**, **Pity Loot**, **Void Items**, **Mutate Item Kit**, **Diminishing Returns**.

11. **PVP & Arena**  
    Expand **Gameplay/Activities/Player vs Player (PVP)/index.md** and **Arena.md** (rules, rewards, Skulls). Link to Skulls, Defense Structures, Maps.

12. **PVE & Invasions**  
    Expand **Player vs Environment (PVE)/index.md** and **Invasions.md**. Link to Missions, Events.

### Phase 5 — Abilities, Tech, Events

13. **Abilities**  
    Create **Gameplay/Abilities/** and pages for Grapple, Hack, Drain, Technician, Taunt, Deflector, Junker. Link to Stats (Hit Chance, Evasion, etc.) and Ships/Items where relevant.

14. **Technology**  
    Single page **Gameplay/Technology.md** (or **Items/Technology.md**) summarizing tech sources (Artifacts, corp, items, ships); link to HELP in-game list.

15. **Events**  
    Create **Gameplay/Events/** and pages for Daily, Holiday, Free Gifts, Party Boxes, Reward Point Gifts. Link to Currencies and Missions.

### Phase 6 — Polish & Optional

16. **Ship Mods, Elite Ranks, Hardcore**  
    Dedicated pages under Ships (or linked from Ships index). Interlink with Arena, Invasions, Oblivion.

17. **Oblivion Server**  
    Single page; link from Gameplay and World. List rule differences from primary server.

18. **About / Meta**  
    Spellbook, Delete Account, Review The Game, Player Guides (with external links). Optional Spaceball policy.

19. **Weapons**  
    When you have data (tiers, damage types), add **Items/Weapons.md** or **Ships/Weapons.md** and link from Items/Ships index.

20. **Consistency pass**  
    Every index.md lists its children; every cross-reference uses the correct relative/absolute link; “See also” where useful.

---

## 5. How to Use This Plan

- **Per task:** Pick a step (e.g. “Phase 2, step 5 — Ships overview”). Open **In Game WIKI.md**, find the matching `[[[Topic]]]`, copy and adapt content into the target file, then add links to other wiki pages using the map above.
- **With AI:** Share **AI-Context-Guide.md** + this file + (optionally) the relevant slice of **In Game WIKI.md** so the AI can draft or expand a page and suggest links.
- **Tracking:** Check off steps or move them to a “Done” section as you go; add new topics to the map when the in-game wiki or community adds them.

---

*This plan aligns with the current docs structure and In Game WIKI v1.5.0. Adjust paths if you rename folders or adopt a different hierarchy.*
