#### 📝 Note: Fedora Safe Update 
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