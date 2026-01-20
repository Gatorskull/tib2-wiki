# Contributor Workflow: The Infinite Black 2 Wiki

Welcome to the team! We use a "Docs-as-Code" approach to build this wiki.
**Do not edit files directly on GitHub.** Follow the workflow below to ensure the site doesn't break.

## 🛠️ Required Tools
1.  **Obsidian** (The Editor) - [Download](https://obsidian.md/)
2.  **GitHub Desktop** (The Sync Tool) - [Download](https://desktop.github.com/)

---

## 🚀 The Workflow Loop
**Always follow this order:**

### 1. Start Fresh (The "Pull")
Before you write a single word, open GitHub Desktop and click **"Fetch origin"** (and "Pull origin" if updates are found).
* *Why?* If you edit an old version of the site, you will cause "Merge Conflicts" that break the build.

### 2. Write (The "Editor")
Open the `tib2-wiki` folder as a Vault in Obsidian.
* **Where to write:** All content pages must go inside the `docs/` folder.
* **Images:** Drag and drop images into Obsidian. They will auto-save to the `docs/assets` folder.
* **Linking:** Use standard WikiLinks: `[[Stinger]]` links to the Stinger page.

### 3. Save & Commit (The "Save Point")
When you are done:
1.  Open **GitHub Desktop**.
2.  You will see your changed files on the left.
3.  **Write a Summary:** Use our standardized tag format (see below).
4.  Click **Commit to main**.

### 4. Publish (The "Push")
Click **"Push origin"** in the top right.
* *Result:* The automated robot (GitHub Actions) will rebuild the website.
* *Time:* Changes go live in ~60 seconds.


---

## 📝 Style & Standards

### Commit Message Format
We use `[Tag] Description` to keep our history clean.

* `[Content]` - Adding or editing text (e.g., `[Content] Add stats for Nukes`)
* `[Fix]` - Correcting typos or errors (e.g., `[Fix] Correct damage cap on T5`)
* `[Assets]` - Uploading images/icons (e.g., `[Assets] Add corp logos`)
* `[Config]` - Changing site settings (⚠️ Admins Only)

### Formatting Cheat sheet
This wiki uses **MkDocs Material**. You can use special blocks:

**Admonitions (Info Boxes):**
To create a colored box, use `!!! type "Title"`. **Crucial:** The text inside must be indented by **4 spaces (or 1 tab)**.

!!! info "Pro Tip" 
	Always check your ammo before leaving the station. This text is inside the box because it has 4 spaces before it.

!!! danger "High Security Zone" 
	Do not enter this sector without a T5 shield. You will lose your ship immediately.

??? note "Show Drop Rates" 
	* Common: 50% * Rare: 10% * Legendary: 1%

**3. Images** 
Just drag and drop them! Obsidian handles the code:
`![[image-name.png]]` 

--- 

## 🚫 The "Don't Touch" List 

Unless you are the Tech Lead, **DO NOT** touch these files: 
* `mkdocs.yml` (Controls the entire site engine) 
* `.github/` folder (Controls the automation robots) 
## 🆘 Troubleshooting 
* **"Merge Conflict":** Stop. Do not force push. Contact the Lead. 
* **Site 404s:** Wait 2 minutes. If it's still down, check the "Actions" tab on GitHub to see why the build failed.