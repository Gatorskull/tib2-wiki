
Welcome to the team! We use a **Docs-as-Code** workflow with **branches and pull requests** to keep the wiki stable, reviewable, and easy to collaborate on.

**⚠️ Never push directly to `main`.** All changes must go through a branch and a pull request.

> **Important clarification**
> 
> - You may **create your branch before OR after you start making changes**.
>     
> - A single branch can contain **multiple commits** until the work is finished.
>     

---

## 🛠️ Required Tools

1. **Obsidian** (Editor) – [https://obsidian.md/](https://obsidian.md/)
    
2. **GitHub Desktop** (Local Git) – [https://desktop.github.com/](https://desktop.github.com/)
    
3. **GitHub Website** (Pull Requests & Merging)
    

---

## 🚀 The Workflow Loop

Follow these steps in order for a smooth contribution.

---

### 1. Start Fresh (Update `main`)

Before you begin (or before creating your branch):

1. Open **GitHub Desktop**
    
2. Switch to the **`main`** branch (2)
    
3. Click **Fetch origin** (1)
    
4. If updates are available, click **Pull origin**
    

**Why?** Keeping `main` up to date reduces merge conflicts later.

![[workflow_1.png]]



---

### 2. Create a Branch (Anytime Before You Push)

All work must live in a branch — **not** `main`.

You can create your branch:

- **Before writing**, or
    
- **After making changes locally** (as long as you create the branch before committing or pushing)
    

#### How to create the branch

1. In **GitHub Desktop**, click **Current Branch → New Branch**
    
2. Name your branch using this format:
    

```
[name]-[action]-[topic]
```

**Examples:**

- `bob-update-ships`
    
- `alice-add-weapons`
    
- `sam-fix-drop-rates`
    

3. Create the branch **from `main`** and switch to it
    

> ✅ Once created, **all commits stay on this branch** until the pull request is merged.

![[workflow_2.png]]
![[workflow_3.png]]

---

### 3. Write (Obsidian)

1. Open the `tib2-wiki` folder as a **Vault** in Obsidian
    

**Content rules:**

- **All pages:** `docs/`
    
- **Images:** Drag & drop → saved automatically to `docs/assets/`
    
- **Links:** Use WikiLinks
    

```md
[[Stinger]]
```

---

### 4. Save & Commit (Local)

You can commit **as often as you want** while working.

Each commit should represent a meaningful step (draft, section added, fixes, etc.).

#### To commit:

1. Open **GitHub Desktop**
    
2. Review the changed files
    
3. Write a commit message (see format below)
    
4. Click **Commit to _your branch_** (⚠️ not `main`)
    

> ✅ Multiple commits on the **same branch** are normal and encouraged.

![[workflow_4.png]]

---

### 5. Push the Branch

When you’re ready to share your work:

1. Click **Publish Branch** in GitHub Desktop
    
2. Your branch and commits are uploaded to GitHub
    

You may push multiple times as you continue working.

![[workflow_5.png]]

---

### 6. Open a Pull Request

1. Open the **GitHub repository** in your browser
    
2. Click **Compare & open pull request**
    
    _Or: **Pull Requests → New Pull Request**_
    
3. Verify:
    

- **Base:** `main`
    
- **Compare:** your branch
    

4. Add a clear title and description
    
5. Create the pull request
    

> The pull request represents **all commits on your branch**.

![[workflow_6.png]]

![[workflow_7.png]]

![[workflow_8.png]]



---

### 7. Handle Merge Conflicts (If Any)

After opening the PR:

#### ✅ No conflicts

- Proceed once approved
    

#### ⚠️ Conflicts detected

- If you **know how to fix them**, resolve locally and push updates
    
- If you **do not know how**:
    
    - Leave the PR open
        
    - Comment or label it **“Needs Review – Merge Conflict”**
        

**Do not force-push or guess.** Ask for help.

![[workflow_9.png]]

![[workflow_error.png]]

---

### 8. Merge & Clean Up

When the PR is approved and conflict-free:

1. Click **Squash and merge**
    
2. Confirm the merge
    
3. Click **Delete branch**
    

> GitHub Actions will rebuild the site. Changes go live in ~60 seconds.


![[workflow_10.png]]

---

## 📝 Style & Standards

### Commit Message Format

```
[Tag] Description
```

**Tags:**

- `[Content]` – Adding or editing text
    
- `[Fix]` – Typos or corrections
    
- `[Assets]` – Images/icons
    
- `[Config]` – Site configuration (**Admins only**)
    

---

### Formatting Cheat Sheet (MkDocs Material)

#### Admonitions

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

Drag & drop into Obsidian:

```md
![[image-name.png]]
```

---

## 🚫 Do Not Edit (Unless Tech Lead)

- `mkdocs.yml`
    
- `.github/`
    

---

## 🆘 Troubleshooting

- **Merge conflict:** Stop. Do not force-push. Fix or mark for review.
    
- **Site shows 404:** Wait 2 minutes, then check the **Actions** tab.
    

---

## ✅ Golden Rule

> Update `main` → Branch (anytime before pushing) → Write → Commit (as often as needed) → Push → Pull Request → Merge → Delete Branch