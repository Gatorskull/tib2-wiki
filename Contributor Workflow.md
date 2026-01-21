# Contributor Workflow: The Infinite Black 2 Wiki

Welcome to the team! We use a **Docs-as-Code** workflow with **branches and pull requests** to keep the wiki stable and reviewable.

**⚠️ Do not edit files directly on `main`.** Always work in a branch and submit a pull request.

---

## 🛠️ Required Tools

1. **Obsidian** (The Editor) – [https://obsidian.md/](https://obsidian.md/)
2. **GitHub Desktop** (Local Git) – [https://desktop.github.com/](https://desktop.github.com/)
3. **GitHub Website** (Pull Requests & Merging)

---

## 🚀 The Workflow Loop (Follow in Order)

### 1. Start Fresh (Pull `main`)

Before you write a single word:

1. Open **GitHub Desktop**
2. Make sure you are on the **`main`** branch
3. Click **Fetch origin**
4. If updates are found, click **Pull origin**

*Why?* Working from an outdated `main` causes merge conflicts and broken builds.

---

### 2. Create a New Branch (Required)

All work must happen in a branch.

1. In **GitHub Desktop**, click **Current Branch → New Branch**
2. Name your branch using this format:

```
[name]-[action]-[topic]
```

**Examples:**

* `bob-update-ships`
* `alice-add-weapons`
* `sam-fix-drop-rates`

3. Create the branch **from `main`** and switch to it

---

### 3. Write (The Editor)

Open the `tib2-wiki` folder as a **Vault** in Obsidian.

**Rules:**

* **All content pages go in:** `docs/`
* **Images:** Drag & drop → auto-saved to `docs/assets/`
* **Links:** Use WikiLinks → `[[Stinger]]`

---

### 4. Save & Commit (Local)

When you’re done writing:

1. Open **GitHub Desktop**
2. Confirm your new/edited files are listed
3. Write a **commit message** using the standard format (see below)
4. Click **Commit to your branch** (⚠️ not `main`)

You may commit multiple times while working.

---

### 5. Push the Branch

1. Click **Push origin** in GitHub Desktop
2. Your branch is now uploaded to GitHub

---

### 6. Open a Pull Request (GitHub Website)

1. Go to the **GitHub repo in your browser**
2. You’ll see a banner offering to **Compare & open pull request** → click it

   * Or: **Pull Requests → New Pull Request**
3. Ensure:

   * **Base:** `main`
   * **Compare:** your branch
4. Add a clear title and description
5. Create the pull request

---

### 7. Handle Merge Conflicts (If Any)

After opening the PR:

#### ✅ If **NO merge conflict**

* Proceed to **Squash and merge** (see next step)

#### ⚠️ If a **merge conflict exists**

* If you **know how to fix it**, resolve the conflict and update the PR
* If you **do NOT know how to fix it**:

  * Leave the PR **open**
  * Add a comment or label indicating **“Needs Review – Merge Conflict”**

**Do NOT force-push or guess.** Ask for help.

---

### 8. Merge & Clean Up

If the PR is approved and has no conflicts:

1. Click **Squash and merge**
2. Confirm the merge
3. Click **Delete branch**

*Result:* GitHub Actions will rebuild the site. Changes go live in ~60 seconds.

---

## 📝 Style & Standards

### Commit Message Format

Use:

```
[Tag] Description
```

**Tags:**

* `[Content]` – Adding or editing text
* `[Fix]` – Typos or corrections
* `[Assets]` – Images/icons
* `[Config]` – Site configuration (⚠️ Admins only)

---

### Formatting Cheat Sheet (MkDocs Material)

#### Admonitions (Info Boxes)

Text inside **must be indented by 4 spaces or 1 tab**.

```md
!!! info "Pro Tip"
    Always check your ammo before leaving the station.
```

```md
!!! danger "High Security Zone"
    Do not enter this sector without a T5 shield.
```

```md
??? note "Show Drop Rates"
    * Common: 50%
    * Rare: 10%
    * Legendary: 1%
```

---

### Images

Just drag & drop into Obsidian:

```md
![[image-name.png]]
```

---

## 🚫 The "Don’t Touch" List

Unless you are the **Tech Lead**, do **NOT** edit:

* `mkdocs.yml`
* `.github/` folder

---

## 🆘 Troubleshooting

* **Merge Conflict:** Stop. Do not force-push. Fix it or mark the PR for review.
* **Site 404s:** Wait 2 minutes. If still broken, check the **Actions** tab on GitHub.

---

✅ **Golden Rule:**

> Pull → Branch → Write → Commit → Push → Pull Request → Merge → Delete Branch
