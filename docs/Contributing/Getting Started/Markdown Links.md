# Markdown Links

This guide explains **how to link pages correctly** in this wiki, with clear rules for **when to use relative vs absolute links**. Following these conventions keeps links predictable, portable, and compatible with both **MkDocs** and **Obsidian**.

---

## The Golden Rule

> **Links should point to source files, not rendered URLs.**
> 
> Always link to the `.md` file path inside `docs/`, never to a slug like `/hello-world`.

---

## Link Types at a Glance

|Situation|Use|Example|
|---|---|---|
|Same folder|Relative|`page.md`|
|Child folder|Relative|`Folder/index.md`|
|Parent folder|Relative|`../index.md`|
|Distant section|Absolute|`/Section/Page.md`|
|Templates / global refs|Absolute|`/Contributing/index.md`|

---

## Relative Links (Recommended)

### When to use them

Use **relative links** when linking to pages that are:

- In the **same folder**
- In a **child** or **parent** folder
- Part of the **same section** that might be moved together

### Why

- Mirror the file system
- Survive navigation changes
- Work in both MkDocs and Obsidian
- Easy to reason about

### Examples

Assume this file:

```
docs/World/hello.md
```

**Same folder**

```
[Maps](maps.md)
```

**Child folder**

```
[Planets](Planets/index.md)
```

**Parent folder**

```
[World overview](../index.md)
```

**Sibling folder**

```
[Ships](../Ships/index.md)
```

> 💡 **Tip:** If you could reach it with `cd` in a terminal, you can link to it relatively.

---

## Absolute Links (Root-Anchored)

### When to use them

Use **absolute links** when:

- Linking across **distant sections**
- Referring to **canonical pages** (FAQ, Contributing, Index pages)
- Writing **templates or examples** meant to be copied

### Format

Absolute links always start at the `docs/` root:

```
/Section/Page.md
```

### Examples

From a page in `Contributing/Getting Started/`, use relative paths to other sections:

```
[Contributing guide](../index.md)
[FAQ](../FAQ.md)
[Ship classes](../../Ships/index.md)
```

From the `docs/` root, links are simply `Section/Page.md` (e.g. `Ships/index.md`, `Entities/Currencies/index.md`).

### Filenames or folders with spaces

Use the **literal space** in the path so the link matches the file or folder name on disk (e.g. `Tech Points.md`, `Jump Gates.md`, `Player vs Player (PVP)/Arena.md`). Do not use `%20` in internal links — that can break resolution in some builds.

---

## What Not To Do

### Don’t link to rendered URLs

```
/hello-world
```

Rendered slugs depend on titles and theme behavior and may change.

---

## Recommended Style Rules (Summary)

- Prefer **relative links** within a section
- Use **absolute links** for site-wide references
- Always link to the **`.md` file**, not a rendered URL
- Do not rely on titles or slugs for navigation

---

## One-Sentence Mantra

> **If you can trace the file path with your eyes, use a relative link.**  
> **If you want a global reference, use an absolute one.**

---
## External Links (Off‑Wiki References)

Markdown links can also point to **external websites** (outside the wiki). While these are sometimes necessary, they should be used **sparingly and intentionally**.

### When External Links Are Appropriate

Use an external link when:

- The information is **authoritative and primary** (e.g., official developer posts, patch notes, or APIs).
- The content is **too large or out of scope** to reasonably mirror on the wiki.
- The link provides **verification**, not opinion (e.g., source citations).

Example:

```
For official patch notes, see the [developer announcement](https://example.com/patch-notes).
```

### Why External Links Should Be Minimized

Excessive external linking can introduce problems:

- **Bias**: Linking selectively to certain creators, forums, or communities can imply endorsement or favoritism.
- **Link rot**: External pages can change, move, or disappear over time.
- **Fragmented knowledge**: Readers are pushed off‑site instead of finding answers within the wiki.

As a rule:

> **If the information can live on the wiki, it should live on the wiki.**

### Best Practices

- Prefer **internal pages** over external links whenever possible.
- If an external link is needed, ensure it is:
    - Neutral and factual
    - Clearly labeled (what the reader should expect)
    - Not required to understand the core content
- Avoid linking to:
    - Opinion pieces
    - Monetized content (ads, referral links)
    - Single‑person interpretations when a neutral summary can be written instead

### Recommended Pattern

Write the content locally, then optionally add a source:

```
This mechanic was introduced in version 1.4 to rebalance fleet combat. 

*Source: [Official patch notes](https://example.com/patch-notes)*
```

This keeps the wiki **self‑contained, neutral, and durable**, while still allowing readers to verify information if they choose to.