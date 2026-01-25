# Contributing

Welcome!
This section explains **how to contribute to the wiki**, how the **folder structure works**, and where to find **examples and templates** you can copy.

The goal is to make contributing easy, predictable, and low-risk — even if you’re new to MkDocs, Obsidian, or docs-as-code workflows.

---

## How this folder is structured

The `Contributing/` folder is a **self-contained guide** that mirrors how the rest of the wiki is organized.

```
Contributing/
   ├─ index.md ← You are here (section overview)
   ├─ FAQ.md ← Common contributor questions
   ├─ Changelog.md ← Changes to contribution rules/templates
   ├─ Draft Notes.md ← (hidden from navigation)
   ├─ Getting Started/
   │  ├─ index.md ← Step-by-step guides & explanations
   │  └─ Example.md ← Concrete examples you can copy
   └─ .pages ← Navigation rules (infrastructure)
```

A few important notes:

- Every navigable folder has an **`index.md`** that acts as a landing page
- Subfolders represent **logical sections**, not just file storage
- Some files may exist but be **hidden from navigation**
- Navigation order is controlled locally via a `.pages` file

You don’t need to edit `.pages` unless you are changing navigation behavior.

---

## Adding new pages

### Adding a new page to this folder

1. Create a new Markdown file in `Contributing/`
2. Give it a clear, descriptive name
3. If it’s an important page:
   - Add it explicitly to `Contributing/.pages`
4. If it’s minor or supplemental:
   - Let it be picked up automatically via `...`

Example:

```
Contributing/Style Guide.md
```


---

## Adding a new subfolder (section)

When adding a new folder:

1. Create the folder
2. Add an `index.md` inside it (required)
3. (Optional but recommended) Add a `.pages` file to control ordering
4. Update the parent folder’s `.pages` if this is a major section

Example:

```
Contributing/New Section/
   ├─ index.md
   ├─ Examples.md
   └─ .pages
```


---

## How navigation works

Navigation is **filesystem-driven**, not centralized.

- The sidebar is generated automatically from folders and files
- Ordering, visibility, and titles are controlled by `.pages` files
- Some content may exist only for reference and not appear in navigation

If something doesn’t show up in the sidebar:
- Check the nearest `.pages` file
- Look for `hide:` rules
- Look for explicit `nav:` lists

---

## Where to find examples and templates

 **Start here:**  
[[Getting Started/index|Getting Started]]

That section contains:
- Step-by-step examples
- Sample folder layouts
- Pages you can safely copy and adapt
- Explanations of common patterns used across the wiki

If you’re unsure how to structure something, there’s probably an example there already.

---

##  General contribution philosophy

- **Navigation is curated** — not everything needs to be in the sidebar
- **Search is automatic** — content is discoverable even if hidden
- **Folders represent concepts**, not just storage
- **Consistency beats cleverness**

If you’re ever unsure, copy an existing pattern and adjust it slightly.

---

If something here is unclear, outdated, or missing — that’s a contribution opportunity in itself 🙂

