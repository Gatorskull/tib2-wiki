# Getting Started

This guide walks you through the **three most common contribution
tasks** step by step:

1.  Modifying text on an existing page
2.  Adding a new page
3.  Adding a new folder (section)

You do **not** need to understand the entire system to contribute safely.

------------------------------------------------------------------------

## Modifying text on an existing page

This is the easiest and safest way to contribute.

### Step 1: Find the page

-   Use **search** in Obsidian, or
-   Navigate through folders in the file tree

Open the `.md` file you want to edit.

------------------------------------------------------------------------

### Step 2: Edit the content

-   Change text directly
-   Add or remove sections
-   Fix typos, clarify wording, or expand explanations

Use normal Markdown:

``` md
## Section heading

Some text here.
```

You may also use [Markdown Links](Markdown Links.md) when linking to other pages:

``` md
[[Contributing/FAQ|Frequently Asked Questions]]
[[Contributing/index|Contributing]]
```

------------------------------------------------------------------------

### Step 3: Save and preview

-   Save the file
-   Preview in Obsidian if you want
-   Commit your change when ready

That's it. No navigation changes required.

------------------------------------------------------------------------

## Adding a new page

Add a new page when you're introducing **new content within an existing
section**.

------------------------------------------------------------------------

### Step 1: Choose the correct folder

Pick the folder that best matches the topic.

Example:

    Gameplay/

If you're unsure, check for similar pages nearby and follow that
pattern.

------------------------------------------------------------------------

### Step 2: Create the file

Create a new Markdown file with a clear, descriptive name:

    Gameplay/Status Effects.md

Avoid vague names like: - `Notes.md` - `Stuff.md` - `New Page.md`

------------------------------------------------------------------------

### Step 3: Add basic structure

Start with a title and a short introduction:

``` md
# Status Effects

This page describes status effects that can be applied to entities in the game.
```

Add sections as needed.

------------------------------------------------------------------------

### Step 4: Decide if it belongs in navigation

-   **Important page?**
    -   Add it explicitly to the folder's `.pages` file
-   **Minor/supporting page?**
    -   Let it be included automatically via `...`

If you don't know, default to **automatic**.

------------------------------------------------------------------------

## Adding a new folder (section)

Add a new folder when you're introducing a **new conceptual area**, not
just a single page.

------------------------------------------------------------------------

### Step 1: Create the folder

Example:

    World/Factions/

------------------------------------------------------------------------

### Step 2: Create an index page (required)

Every navigable folder **must** have an `index.md`.

    World/Factions/index.md

Minimum recommended content:

``` md
# Factions

This section documents the major factions that exist in the game world.
```

The `index.md` acts as the **landing page** for the section.

------------------------------------------------------------------------

### Step 3: (Recommended) Add a `.pages` file

Create:

    World/Factions/.pages

Basic template:

``` yml
nav:
  - index.md
  - ...
```

This ensures: 
- The section is clickable 
- The index page appears first 
- Future pages are included automatically

------------------------------------------------------------------------

### Step 4: Add pages inside the folder

Example:

    World/Factions/
    ├─ index.md
    ├─ The Syndicate.md
    ├─ Free Traders.md
    └─ .pages

Use wikilinks between related pages where appropriate.

------------------------------------------------------------------------

## How to know if you're doing it right

You're probably on the right track if:

-   You copied an existing pattern
-   Your folder has an `index.md`
-   You didn't fight the navigation system
-   Your change is easy to understand in isolation

Consistency matters more than perfection.

------------------------------------------------------------------------

##  Examples

For concrete examples you can copy, see:

[[Getting Started/Examples/index|Examples]]

------------------------------------------------------------------------

If something here feels unclear or awkward, let us know!
