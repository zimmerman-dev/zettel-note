 
 ⌚9:38 am  📆 Mon Sep 1
 🔗 **Related Concepts**: #note #cpp
___
```dataviewjs
const pages = dv.pages();
const totalNotes = pages.length;

let totalWords = 0;
let totalBacklinks = 0;
const allTags = new Set();
const allFolders = new Set();

for (let page of pages) {
  // --- WORD COUNT ---
  // Get the file content safely, then split on whitespace
  const content = await dv.io.load(page.file.path);
  const wordCount = content ? content.split(/\s+/).filter(w => w.length > 0).length : 0;
  totalWords += wordCount;

  // --- BACKLINK COUNT ---
  if (page.file.inlinks)
    totalBacklinks += page.file.inlinks.length;

  // --- TAGS ---
  if (page.tags) {
    for (let tag of page.tags)
      allTags.add(tag);
  }

  // --- FOLDERS ---
  const folder = page.file.path.split("/").slice(0, -1).join("/") || "/";
  allFolders.add(folder);
}

dv.header(2, "📊 Vault Overview");

dv.list([
  `📝 Total Notes: ${totalNotes}`,
  `🧮 Total Words: ${totalWords.toLocaleString()}`,
  `🔗 Total Backlinks: ${totalBacklinks}`,
  `🏷️ Unique Tags: ${allTags.size}`,
  `📁 Unique Folders: ${allFolders.size}`
]);
```
### 🔹 Week 6:  **09/30 – 10/06** — Loops, Branches, and Randomness  
📍 **Ch. 8–8.15** — _If_, _Loops, Goto, RNG_  
- [x] **Block 0:** (8 → 8.5) _if, if else, else if, and switch statements_ 
- [ ] **Block 1:** (8.6 → 8.10) Switch scoping, goto, loops: while/do/for  
- [ ] **Block 2:** (8.11 → 8.15) Break/continue, halt, RNG, Mersenne Twister  
- [ ] **Block 3:** Practice problems + reroll logic game  
- [ ] **Weekend:** Chapter 8 quiz + random project 
- [ ] **Block 4:** (9.1 → 9.6) Testing, coverage, semantic errors, `std::cin`, `assert`  