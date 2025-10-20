 ⌚6:49 pm  📆 Wed Aug 13
 🔗 **Related Concepts**: #note #toolchain 
___
## 🛠️ Safe Fedora WSL Update Guide
### 🔹 1. Simulate the Update (Dry Run)
Check what packages *would* be updated without applying changes:
```bash
sudo dnf upgrade --refresh --assumeno
```
- `--refresh` updates repo metadata
- `--assumeno` prevents changes (dry run)
### 🔹 2. Apply All Safe Updates
```bash
sudo dnf upgrade --refresh
```
This pulls in the latest **stable** package versions from enabled repositories.
### 🔹 3. Clean System Post-Upgrade
#### Check for Broken Dependencies:
```bash
sudo dnf check
```
#### List Duplicate Packages:
```bash
sudo dnf repoquery --duplicates
```
#### List Orphaned Packages (no longer in any repo):
```bash
sudo dnf repoquery --extras
```

---
### 🔹 4. (Optional) Double-Check Before `autoremove`
 1. Before confirming package removal, review the list that `dnf autoremove` wants to remove:
```bash
sudo dnf autoremove --assumeno
```

2. To manually inspect any packages:
```bash
rpm -qi <package-name>
```

3. Or see what depends on it (if anything):
```bash
rpm -q --whatrequires <package-name>
```

4. If you'd like to _keep_ something:
```bash
sudo dnf mark install <package-name>
```
This prevents `dnf` from cleaning it up in the future.
#### Clean Up Orphaned Dependencies:
```bash
sudo dnf autoremove
```
### 🔹 5. Restart WSL to Clear Environment
```bash
exit
wsl --shutdown
```
Then reopen your WSL terminal to start fresh.
### 🔹 6. Shutdown / Reboot
```bash
sudo shutdown now
```

```bash
sudo reboot
```

____
## Handling Interruptions
If your `sudo dnf upgrade --refresh` was interrupted, here is a few things you can do to check your problems:
### 🔹 Show Recent Operations
```bash
sudo dnf history list
```
This will show you the most recent operations. If one was interrupted, you'll see it listed as *Incomplete* or *Error*. 

Then check:
```bash
sudo dnf history info last
```
to see what was installed or updated before it stopped.
### 🔹 Quick Fix
If DNF reports a pending transaction, fix it with:
```bash
sudo dnf history redo last
```

Or:
```bash
sudo dnf history rollback last
```
depending on whether you want to finish it or undo it.
___
### 🔹 Clean Up
If it's not obvious what state you're in, do:
```bash
sudo dnf clean all
sudo dnf makecache
```

Then:
```bash
sudo dnf distro-sync
```
`distro-sync` is the nuclear "make my system consistent" button. It compares every installed package against the repos and either upgrades or downgrades as needed to match the current repo versions.
___
### 🔹 Verify the System
Run:
```bash
sudo rpm -Va
```
This command audits installed files for mismatches (modified configs, missing libs, etc.). It's verbose, but it will show you you're broken dependency chain if it exists.
___
###  (Resolve Dependencies)
If DNF throws dependency errors, this usually fixes it:
```bash
sudo dnf check
sudo dnf check --dependencies
```

Or if it's smoked:
```bash
sudo rpm --rebuilddb
```
This is a "break glass if DNF is confused" command and not to be used as a normal maintenance step.
##### What it does
`rpm --rebuilddb` **rebuilds the RPM database**, which is the local record of every installed package, its files, and dependencies. It's sort of acts like Fedora’s internal ledger of what’s on your system. When it gets corrupted or out of sync, DNF and RPM can start throwing weird dependency or “package not found” errors.

It forces RPM to:
- Delete and recreate the index files in that directory,
- Re-scan all `.rpm` headers, 
- Rebuild its internal lookup tables from scratch. 

It doesn’t reinstall anything — it just repairs the bookkeeping.
#####  When to use it
Only if:
- DNF reports database errors (`rpmdb: BDB0113 ...` or “database is malformed”), 
- `dnf check` or `rpm -Va` fail immediately,  
- You suspect metadata corruption after a crash or hard reset.