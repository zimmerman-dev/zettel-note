 
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
#### ✅ To-do: zimmerman-dev TODO   
 ⌚8:58 pm  📆 Sun Nov 2
 🔗 **Related Concepts**: #todo
___
### 🚀 Immediate Action
- [ ] Random Number Generator Notes
---
- [ ]  ch 10 type conversions, type aliases, and type deductions
---
- [ ] ch 11 function overloading and function templates 
---
- [ ]  
---
- [ ] 
---
- [ ] 
---
- [ ] 
---
- [ ] 
---
- [ ] 
---