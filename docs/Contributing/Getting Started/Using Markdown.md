
This page provides **canonical examples** for writing and formatting content on the *The Infinite Black 2 Wiki*.  
All contributors should follow these conventions to keep the wiki clean, consistent, and professional.

---
## Headings

Use headings to structure pages logically. Do **not** skip levels.
```md
# Page Title (H1 – only one per page)

## Major Section (H2)

### Subsection (H3)

#### Minor Details (H4)
```

Rules
- Each page must have exactly one H1 at the top.
- Use sentence case for headings.
- Avoid emojis in headings (allowed in body text if appropriate).

Paragraphs & Line Breaks

Write in clear, concise paragraphs.
```md
This is a paragraph. It should explain a single idea clearly.

This is a new paragraph. Avoid walls of text.
```

Do **not** manually add line breaks inside paragraphs.

---
## Emphasis

```
*Italic*  
**Bold**  
***Bold Italic***
```

**Guidelines**
- Use **bold** for important terms or first mentions.
- Use _italic_ sparingly (titles, emphasis, flavor).

---
## Lists

### Unordered Lists
```
- Fast 
- Durable
- Expensive
```

### Ordered Lists
```
1. Warp to target 
2. Engage shields 
3. Deploy drones
```

### Nested Lists
```
- Weapons
  - Lasers
  - Missiles
- Defenses  
  - Shields  
  - Armor
```

---
## Links
Standard Markdown Links (External)

Use for **external sites only**.
```md
[Official Website](https://example.com)
```

---
## Wikilinks (Internal Pages)
Use Obsidian-style wikilinks for all internal wiki references.
```
[[Ship Classes]]
[[Weapons]]
[[Faction: Wyrd]]
```

Display Text
```
[[Ship Classes|classes of ships]]
```

**Rules**
- Prefer wikilinks over regular markdown links for internal pages.
- Do not include file extensions (`.md`).
- Link the **first meaningful mention** of a page on each article.

---
## Naming Conventions (Pages)
Consistency matters more than perfection.

### Page Titles
- Use **Title Case**
- Be descriptive, not vague

**Good**
- `Carrier`
- `Ship Classes`
- `Harvest Drones`
- `Faction: The Pirates`

**Avoid**
- `car`
- `Ships2`
- `Stuff`
- `Guide_final_v3`

---
## Code & Inline Code

### Inline Code
Use for commands, keys, or filenames.

```
Press `F` to interact. Edit the `mkdocs.yml` file.
```

### Code Blocks

```yaml 
site_name: The Infinite Black 2 Wiki 
theme:   
  name: material
```

---
## Admonitions (Info Boxes)
Material for MkDocs supports admonitions.

```
!!! info
	This ship excels at hit-and-run tactics.
```

```
!!! warning
	This information may change in future patches.
```

```
!!! danger
	Using multiple accounts may result in a ban.
```

---
## Collapsible Sections (Spoilers)
Use for spoilers or optional deep dives.

```
??? spoiler "Story Spoilers"
	The player captain is a mass-produced clone with no moral compass.
```

---
## Tone & Style
- Write in **neutral, informative language**
- Avoid speculation unless clearly labeled
- No first-person opinions (`I think`, `In my experience`)
- Assume the reader is intelligent but new

**Good**
> This weapon is commonly used in PvP engagements due to its high burst damage.

**Avoid**
> I think this weapon is really good and I always use it.

---
## Final Notes
- When in doubt, **copy an existing good page**
- Consistency beats cleverness
- Ask before inventing new conventions

If something isn’t covered here, bring it up with the project lead.