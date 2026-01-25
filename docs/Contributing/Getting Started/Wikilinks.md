## Wikilinks

This wiki uses **Obsidian-style wikilinks** instead of plain Markdown links whenever possible.

Example:

[[Getting Started/index|Getting Started]]
[[Example]]

``` text
[[Getting Started/index|Getting Started]]
[[Example]]
```

### Why wikilinks are preferred

-   They are **easier to read and write**
-   Obsidian can **auto-complete and refactor** them safely
-   Links stay valid if files are moved or renamed
-   They work correctly when the site is built with MkDocs

------------------------------------------------------------------------

### Important rules when using wikilinks

#### 1. Avoid ambiguous links

If two files share the same name, always include the folder path:

``` text
[[Gameplay/Combat]]
[[World/Combat]]
```

Do **not** rely on bare names like `[[Combat]]` if duplicates exist.

------------------------------------------------------------------------

#### 2. Use folder index pages explicitly

Folders do not automatically resolve to their index pages.\
Always link to the index file directly:

``` text
[[Contributing/index|Contributing]]
[[Getting Started/index|Getting Started]]
```

------------------------------------------------------------------------

#### 3. Use readable link text

Prefer clear display text, even if the filename is technical:

``` text
[[Entities/Status Effects|status effects]]
```

------------------------------------------------------------------------

### When plain Markdown links are acceptable

Plain Markdown links are fine when: 
- Linking to external websites 
- Linking to files that must work outside Obsidian 
- You need strict URL control

Otherwise, **default to wikilinks**.