#### 📝 Note: Git 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:21 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #toolchain #note
___
# 🧪 Git Essentials – Quick Reference


### 🔧 Setup


```bash
git config --global user.name "John Zimmerman"
git config --global user.email "you@example.com"
```

---
### 📂 Create or Clone


```bash
git init                 # Start a new repo
git clone <url>          # Clone existing repo
```

---
### 📌 Staging & Committing


```bash
git add .                # Stage all changes
git add file.cpp         # Stage specific file
git commit -m "message"  # Commit staged changes
```

---
### 🔁 Pushing & Pulling


```bash
git pull --rebase        # Pull latest changes and reapply your commits
git push origin main     # Push to GitHub
```

---
### 🧼 Status & Logs


```bash
git status               # See what's changed
git log --oneline        # View commit history (short)
```

---
### 🛠 Branches


```bash
git switch -c new-feature      # Create and switch to a new branch
git switch main                # Return to main
```

---
### 🧯 Undo


```bash
git restore file.cpp           # Discard uncommitted changes
git reset --soft HEAD~1        # Undo last commit (keep changes)
git reset --hard HEAD          # Dangerous: full revert
```

---
### ❌ Delete a tracked file


If you want to delete a file and track that deletion in Git:


```bash
git rm filename
git commit -m "chore: Remove filename"
```

---
### ❌ Delete a directory


```bash
git rm -r foldername
git commit -m "chore: Remove foldername directory"
```

---
### 🛑 If you delete manually (e.g., `rm`), Git will see it as a change:


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
### 🚫 Ignore future deletions with `.gitignore`


```bash
git rm --cached filename
echo filename >> .gitignore
```

---
### ⏳ Git Restore


```bash
git restore filename
```

---
### 🏷 Tags


```bash
git tag v1.0.0 -m "Tag message"
git push origin v1.0.0
```

---
## 📝 Git Commit Types – Cheat Sheet


### ✅ General Guidelines

- Use **lowercase type**, followed by a colon and a space.
- Keep the summary **under 50 characters** if possible.
- Use the body (optional) to explain **why** a change was made.
- You don’t need a type every time—but they help when you do.
- Use the **imperative mood** for commit messages (e.g. `Add`, not `Added` or `Adds`).
- This keeps a consistent, changelog-friendly format and plays nicely with tools like `git log`, release scripts, and CI systems.

---
### 🔧 Common Commit Types

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

---

### 🧠 Example Good Commit

```bash
git commit -m "docs: Add cpp-template banner image to assets/"
```