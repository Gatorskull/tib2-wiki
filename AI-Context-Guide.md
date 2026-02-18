# TIB2 Wiki — AI Context Guide

**Use this document to give an AI (or new contributor) full context in one place.** Copy it, paste it, or reference it with `@AI-Context-Guide.md` in Cursor so the AI understands the project, structure, and how to work with the wiki.

---

## 1. Project Summary

- **What:** Unofficial community wiki for **The Infinite Black 2** (TIB2), a cross-platform space MMO by Spellbook.
- **Goal:** A professional, ad-free, high-quality knowledge base using a **docs-as-code** approach: strict control over content, easy collaboration for a small team (~3 people).
- **Audience:** Players (new and veteran), contributors, and anyone needing accurate TIB2 reference material.

---

## 2. Tech Stack & Workflow

| Layer | Tool |
|-------|------|
| **Site generator** | MkDocs with **Material** theme |
| **Hosting** | GitHub Pages (public repo) |
| **Editing** | Obsidian (open `tib2-wiki` folder as vault) |
| **Version control** | Git (GitHub Desktop recommended) |
| **Deploy** | GitHub Actions (auto-build on push to `main`) |

- **Never push directly to `main`.** All changes go through a **branch → pull request → review → merge**.
- Commit tags: `[Content]`, `[Fix]`, `[Assets]`, `[Config]`.
- Full workflow: see **Contributor Workflow.md** in the repo root.

---

## 3. Repository Layout

```
tib2-wiki/
├── docs/                    ← ALL wiki content (Markdown)
│   ├── index.md            ← Homepage
│   ├── .pages              ← Top-level nav order
│   ├── Entities/           ← Structures, Currencies, Corporations
│   ├── Gameplay/           ← Activities (PVP, PVE, Arena, Invasions)
│   ├── World/              ← Maps, Security Rating, navigation
│   └── Contributing/       ← How to contribute, style, examples
├── Gathered Training Data/ ← SOURCE: in-game wiki export & Discord data
│   ├── In Game WIKI.md     ← Primary source (v1.5.0 export, [[[Topic]]] format)
│   └── Raw Training Data*.md
├── mkdocs.yml              ← Site config (admins only)
├── AI-Context-Guide.md     ← This file
├── AI prompt.md            ← Short project blurb for pasting
└── Contributor Workflow.md
```

---

## 4. Docs Structure (What Exists vs What’s Linked)

- **Every navigable section** has an **`index.md`** as the landing page.
- **Navigation** is filesystem + **`.pages`** files (awesome-pages plugin). Order and visibility are set in `.pages`; not every file must appear in the sidebar.
- **Broken or missing targets:** The homepage links to **Ships** and **Weapons** — these sections do **not** exist yet; they are placeholders. Create `docs/Ships/` and `docs/Weapons/` when filling content.

**Current `docs/` outline:**

| Section | Purpose | State |
|---------|---------|--------|
| **Entities** | Structures, Currencies, Corporations | Partially filled (Structures + Currencies have content; Corps index only) |
| **Gameplay** | PVP, PVE, Arena, Invasions | Stubs / placeholders |
| **World** | Maps, Security Rating, navigation | Some content (World + Security Rating); Maps index is placeholder |
| **Contributing** | How to add/edit, style, links, examples | Filled (reference for all new pages) |

---

## 5. Linking Rules (Critical for Interlinking)

- **Link to the `.md` file**, not to a URL slug. Use paths under `docs/`.
- **Within one section:** Prefer **relative** links (e.g. `[Credits](Credits.md)`, `[Deployment](Deployment.md)`).
- **Across sections:** Use **absolute** from `docs/` root (e.g. `[Ships](/Ships/index.md)`, `[Contributing](/Contributing/index.md)`).
- **Obsidian:** WikiLinks `[[PageName]]` work via the wikilinks MkDocs extension; for clarity and portability, explicit `[text](path/to/Page.md)` is also fine and recommended in templates.
- Full rules: **docs/Contributing/Getting Started/Markdown Links.md**.

---

## 6. Content Source: In-Game Wiki Export

The file **`Gathered Training Data/In Game WIKI.md`** is the main **source of truth** for game mechanics and topics. It is an export of the in-game wiki (v1.5.0) with:

- **Topic blocks:** `[[[TopicName]]]` … content … next topic.
- **In-game links:** `<u><link="Target">Label</link></u>`. When creating wiki pages, convert these to Markdown links to the corresponding wiki doc (e.g. `[Label](Target.md)` or the correct path under `docs/`).
- **Coverage:** How To Play, FAQ, Corporations, Ships, Stats, Technology, Skills, Items, Crafting, PvP, Defense Structures, Factions, Artifacts, Relics, Alliances, Missions, Currencies, Events, Ship Mods, Abilities (Grapple, Hack, Drain, Technician, Taunt, Deflector, Junker), and more.

When adding or expanding a page, **pull wording and structure from this file**, then adapt to wiki style (headings, tables, admonitions, relative/absolute links).

---

## 7. Style & Formatting (MkDocs Material)

- **Admonitions:** `!!! info "Title"` / `!!! danger "Title"` / `!!! tip "Title"` for callouts.
- **Collapsible:** `??? note "Title"` for spoilers or optional detail.
- **Images:** Store in `docs/assets/`; use `![alt](assets/filename.png)`.
- **Tables:** Standard Markdown tables; use for stats, limits, comparisons.

---

## 8. How to Use This With an AI

- **Paste this entire guide** into a new chat when starting a wiki-related task.
- Or in Cursor: **@AI-Context-Guide.md** so the AI has repo structure, linking rules, and content source in context.
- For the **step-by-step plan to fill the wiki** (which topics to add, where, and in what order), use **docs/Contributing/Wiki-Fill-Out-Plan.md** in addition to this guide.

---

## 9. Quick Reference: Key Files

| Need | File |
|------|------|
| Workflow (branch, PR, merge) | **Contributor Workflow.md** |
| Link rules (relative vs absolute) | **docs/Contributing/Getting Started/Markdown Links.md** |
| Content source (game text) | **Gathered Training Data/In Game WIKI.md** |
| Plan to fill wiki (steps + map) | **docs/Contributing/Wiki-Fill-Out-Plan.md** |
| Short project blurb | **AI prompt.md** |

---

*Last updated for wiki structure as of Feb 2025.*
