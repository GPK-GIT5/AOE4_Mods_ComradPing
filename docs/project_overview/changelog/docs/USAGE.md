# Changelog Usage Guide

┌─────────────────────────────────────────────────┐
│          📋 CHANGELOG QUICK REFERENCE          │
├─────────────────────────────────────────────────┤
│                                                 │
│  📝 Add Entry     → validate → append → gen    │
│  🔍 View Changes  → open 2026-02.md            │
│  📊 Update Views  → generate-overview.ps1      │
│  📖 Full Details  → generate-detailed-entries  │
│                                                 │
└─────────────────────────────────────────────────┘

---

## ➕ Add New Entry

### Step 1: Copy Template

📂 Location: `docs/project_overview/changelog/docs/entry-template.jsonl`

```json
{"timestamp":"2026-02-24T00:00:00Z","file":"path/to/file","status":"added","type":"markdown","change":"Brief description of what changed","impact":"minor","category":"reference","audience":"users","tags":"example,tag"}
```

### Step 2: Validate Entry

```powershell
# Paste your entry here (replace the JSON string)
$entry = '{"timestamp":"2026-02-24T00:00:00Z",...}'
.\scripts\validate-entry.ps1 -Entry $entry
```

✅ **Expected:** Green checkmark "VALID ENTRY"  
❌ **If errors:** Fix the highlighted field and re-validate

### Step 3: Choose Scope

- Changed files starting with `Scenarios/` or `Gamemodes/`? → Use `output/mods/{YYYY-MM}/{YYYY-MM-DD}.jsonl`
- Changed files in `docs/project_overview/changelog/`? → Use `output/system/{YYYY-MM}/{YYYY-MM-DD}.jsonl`
- Changed anything else? → Use `output/workspace/{YYYY-MM}/{YYYY-MM-DD}.jsonl`

### Step 4: Append to Daily Log

```powershell
# Replace <scope> with: mods, system, or workspace
# Replace <month> and <date> with current YYYY-MM and YYYY-MM-DD
$entry | Out-File -FilePath output\<scope>\<month>\<date>.jsonl -Append -Encoding utf8 -NoNewline
"`n" | Out-File -FilePath output\<scope>\<month>\<date>.jsonl -Append -Encoding utf8 -NoNewline
```

### Step 5: Generate Changelog

```powershell
# Replace <scope> and <month> with your chosen values
.\scripts\generate-overview.ps1 -Scope <scope> -Month <month>
.\scripts\generate-detailed-entries.ps1 -Scope <scope> -Month <month>
```

📂 **Output:** `output/<scope>/<month>/INDEX.md` updated with your entry

---

## 🔍 View Changelogs

📂 **File Locations:**
- Workspace changes: `output/workspace/{YYYY-MM}/INDEX.md`
- System changes: `output/system/{YYYY-MM}/INDEX.md`
- Mod changes: `output/mods/{YYYY-MM}/INDEX.md`

**What's inside:**
- Dashboard with health metrics at top
- Quick overview table (with links to daily .jsonl files)
- Detailed entries (scroll down past `---`)

---

## 🔎 Query Examples

### Find all critical changes

```powershell
Get-ChildItem output -Recurse -Filter *.jsonl | Get-Content |
  ConvertFrom-Json | 
  Where-Object { $_.impact -eq "critical" }
```

### Find changes to a specific file

```powershell
Get-ChildItem output\workspace -Recurse -Filter *.jsonl | Get-Content |
  ConvertFrom-Json | 
  Where-Object { $_.file -like "*INDEX.md*" }
```

### Count entries by impact

```powershell
Get-ChildItem output\workspace -Recurse -Filter *.jsonl | Get-Content |
  ConvertFrom-Json | 
  Group-Object impact | 
  Select-Object Name, Count
```

### Find all changes in last 7 days

```powershell
$cutoff = (Get-Date).AddDays(-7)
Get-ChildItem output -Recurse -Filter *.jsonl | Get-Content |
  ConvertFrom-Json | 
  Where-Object { [DateTime]$_.timestamp -gt $cutoff }
```

### Group changes by file

```powershell
Get-ChildItem output\workspace -Recurse -Filter *.jsonl | Get-Content |
  ConvertFrom-Json | 
  Group-Object file | 
  Select-Object Name, Count | 
  Sort-Object Count -Descending
```

---

## ⚠️ Common Issues

**Validation fails with "Field missing"**  
→ Check template has all 9 required fields (timestamp, file, status, type, change, impact, category, audience, tags)

**Dashboard not updating**  
→ Run both scripts: `generate-overview.ps1` then `generate-detailed-entries.ps1`

**Emoji showing as boxes/question marks**  
→ Normal in older terminals. Functionality still works.

**Entry appears twice**  
→ You appended to wrong scope. Check file path routing in Step 3.

**Invalid impact value error**  
→ Use only these values: `critical`, `major`, `minor`, `bugfix`, `documentation`, `refactor`, `internal`, `other`

**JSONL file corrupted**  
→ Each line must be valid JSON. Check for missing commas, quotes, or braces. Use a JSON validator.

---

## 📂 File Locations

```
docs/project_overview/changelog/
├── 📜 USAGE.md              ← You are here
├── 📜 QUICKSTART.md         ← Detailed onboarding guide
├── 📜 README.md             ← Full system documentation
│
├── 🔧 validate-entry.ps1    ← Step 2: Validation script
├── 🔧 generate-overview.ps1 ← Step 5a: Dashboard generator
├── 🔧 generate-detailed-entries.ps1 ← Step 5b: Entry generator
│
├── templates/
│   └── entry-template.jsonl ← Step 1: Copy this
│
├── workspace/               ← Most changes go here
│   ├── INDEX.jsonl          ← Append entries here
│   └── 2026-02.md          ← View results here
│
├── system/                  ← Changelog infrastructure changes
│   ├── INDEX.jsonl
│   └── 2026-02.md
│
└── mods/                    ← Mod-specific changes
    ├── INDEX.jsonl
    └── 2026-02.md
```

---

## 📚 Additional Resources

- **Full Documentation:** [README.md](README.md)
- **Quick Start Guide:** [QUICKSTART.md](QUICKSTART.md)
- **Schema Reference:** [README.md#schema](README.md#schema)
- **Health Scoring:** [README.md#health-scoring](README.md#health-scoring)

---

## 🎯 Quick Tips

✨ **Copy the template** → Always start with `entry-template.jsonl`  
🔍 **Validate first** → Catch errors before appending  
📂 **Right scope** → Use file path to determine scope  
🔄 **Run both scripts** → Overview + detailed entries  
🧹 **Keep it clean** → One entry per logical change
