♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:21 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #toolchain #note
___
## 📝 Note: Git 
### 🔹 Setup
```bash
git config --global user.name "John Zimmerman"
git config --global user.email "you@example.com"
```
---
### 🔹 Create or Clone
```bash
git init                 # Start a new repo
git clone <url>          # Clone existing repo
```
---
### 🔹 Staging & Committing
```bash
git add .                # Stage all changes
git add file.cpp         # Stage specific file
git commit -m "message"  # Commit staged changes
```
---
### 🔹 Pushing & Pulling
```bash
git pull --rebase        # Pull latest changes and reapply your commits
git push origin main     # Push to GitHub
```
---
### 🔹 Status & Logs
```bash
git status               # See what's changed
git log --oneline        # View commit history (short)
```
---
### 🔹 Branches
```bash
git switch -c new-feature      # Create and switch to a new branch
git switch main                # Return to main
```
---
### 🔹 Undo
```bash
git restore file.cpp           # Discard uncommitted changes
git reset --soft HEAD~1        # Undo last commit (keep changes)
git reset --hard HEAD          # Dangerous: full revert
```
---
### 🔹 Delete a tracked file
If you want to delete a file and track that deletion in Git:

```bash
git rm filename
git commit -m "chore: Remove filename"
```
---
### 🔹 Delete a directory
```bash
git rm -r foldername
git commit -m "chore: Remove foldername directory"
```
---
### 🔹 If you delete manually (e.g., `rm`), Git will see it as a change:
```bash
rm filename
git status  # will show the file as "deleted"
git add filename
git commit -m "chore: Remove filename manually"
```

**Alternative Shorthand**

```bash
git add -u      # stages deletions and modifications
```
---
### 🔹 Ignore future deletions with `.gitignore`
```bash
git rm --cached filename
echo filename >> .gitignore
```
---
### 🔹 Git Restore
```bash
git restore filename
```
---
### 🔹 Tags
```bash
git tag v1.0.0 -m "Tag message"
git push origin v1.0.0
```
---
## 📝 Git Commit Types – Cheat Sheet
**General Guidelines**
- Use **lowercase type**, followed by a colon and a space.
- Keep the summary **under 50 characters** if possible.
- Use the body (optional) to explain **why** a change was made.
- You don’t need a type every time—but they help when you do.
- Use the **imperative mood** for commit messages (e.g. `Add`, not `Added` or `Adds`).
- This keeps a consistent, changelog-friendly format and plays nicely with tools like `git log`, release scripts, and CI systems.
---
### 🔹 Common Commit Types
##### `feat:`  
**Add a new feature.**  
`feat: Add inventory sorting logic`
##### `fix:`  
**Fix a bug or incorrect behavior.**  
`fix: Correct off-by-one error in loop`
##### `docs:`  
**Change only documentation.**  
`docs: Update README with build instructions`  
`docs: Add LICENSE file`
##### `style:`  
**Purely formatting/code style changes. No logic changes.**  
`style: Reformat code with clang-format`
##### `refactor:`  
**Change code structure without changing functionality.**  
`refactor: Extract file parser into separate class`
##### `test:`  
**Add or modify tests only.**  
`test: Add unit test for string tokenizer`
##### `chore:`  
**Routine work or meta stuff (CI, tooling, build scripts).**  
`chore: Add .gitignore and clangd config`  
`chore: Bump CMake minimum version`
___
### 🔹 Example Good Commit
```bash
git commit -m "docs: Add cpp-template banner image to assets/"
```
___
## Git Branch Sync Workflow (Desktop ↔ Laptop)
 ♻️ *subsection*   
 ⌚3:21 am  📆 Sun Oct 19
___
You keep your main development branch (main) on your desktop, and a laptop branch (e.g. `<branch-name>`) on your laptop.

- main = the stable, up-to-date branch that lives on GitHub.
- `<branch-name>` = your working branch used on your laptop to avoid pushing half-done work directly to main.

This note shows how to:
- Pull the latest changes from main to your laptop branch.
- Merge your laptop edits into main when ready.
- Sync those merged changes back down to your desktop.
___
### 1. Desktop setup (baseline)
Make sure your desktop main is up to date before leaving:
```
git checkout main
git pull origin main
git push origin main   # ensures GitHub has your latest
```
Now your remote main matches what’s on your desktop.
### 2. Laptop — pull latest main into your laptop branch
When you sit down with the laptop:
```
git fetch origin         # update remote refs
git checkout main
git pull origin main     # make sure local main is current
git checkout <branch-name>
git merge main           # bring main’s changes into your laptop branch
```
✅ Result:
Your `<branch-name>` branch now includes everything from the latest main.
You can safely code here without disturbing main.
### 3. Laptop — push your edits back up
After you make changes and commit them:
```bash
git push origin <branch-name>
```
You’ll now see your new commits on GitHub under the `<branch-name>` branch.

When ready to merge those edits into main, do it one of two ways:

#### Option A — On GitHub (web merge)
1. Open a Pull Request from `<branch-name>` → main.
2. Merge it using the web UI.
3. Done. *Then skip down to Step 4 (Desktop).*
#### Option B — In terminal (local merge)
```bash
git checkout main
git pull origin main       # ensure main is latest
git merge <branch-name>      # bring your laptop changes into main
git push origin main       # publish to GitHub
```
✅ Result:
Your main on GitHub now includes the laptop branch changes.
### 4. Desktop — pull merged main back down
Once you're back on your desktop, sync up:
```bash
git checkout main
git pull origin main
```
✅ Now your desktop’s main matches GitHub’s main (including all laptop edits).
___
### Optional clean-up
If your `<branch-name>` branch was just a temporary working branch:
```bash
git branch -d <branch-name>         # delete locally
git push origin --delete <branch-name>   # delete remote branch
```

You can recreate it any time with:
```bash
git checkout -b <branch-name>
```
___
### Quick Reference Table

| Task                            | Command                                        | Description                      |
| ------------------------------- | ---------------------------------------------- | -------------------------------- |
| Fetch remote changes            | `git fetch origin`                             | Updates remote tracking branches |
| Sync local main                 | `git checkout main && git pull origin main`    | Ensures main matches GitHub      |
| Merge main into laptop branch   | `git checkout <branch-name> && git merge main` | Keeps laptop branch up to date   |
| Merge laptop edits back to main | `git checkout main && git merge <branch-name>` | Integrates laptop work           |
| Push updated main               | `git push origin main`                         | Uploads latest main to GitHub    |
| Pull updated main on desktop    | `git pull origin main`                         | Updates desktop copy             |
