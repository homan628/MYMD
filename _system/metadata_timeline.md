# Timeline Metadata

> Daily diary entries — the source of truth for all dated information.

## Structure

```
/timeline
├── _metadata.md
├── /2024
│   ├── 241215.md
│   └── 241220.md
├── /2025
│   ├── 250101.md
│   ├── 250102.md
│   └── ...
└── /2026
    └── ...
```

## File Naming

- Format: `YYMMDD.md`
- Example: `250120.md` for January 20, 2025
- One file per day (only create if there's content)

## Entry Schema

```yaml
---
date: YYYY-MM-DD
weekday: Monday | Tuesday | ...
weather:                         # Optional
location:                        # Primary location for the day
mood:                            # Optional: great | good | okay | bad | terrible
energy:                          # Optional: high | medium | low
tags: []
---

## Day Title or Summary (Optional)

### Morning

<!-- What happened in the morning -->

### Afternoon

<!-- What happened in the afternoon -->

### Evening

<!-- What happened in the evening -->

<!-- OR just write freely without time sections -->

---
### Links
- **People:** [[entity-links]]
- **Places:** [[entity-links]]
- **Content:** [[entity-links]]
- **Food:** [[entity-links]]
- **Work:** [[entity-links]]
- **Other:** [[entity-links]]
```

## Writing Guidelines

### Natural Language First
Write like a diary. The AI will extract structure.

✓ Good:
```
和Sarah在東京的Example Cafe吃晚飯，牛排很好吃但有點貴。
之後回家看了兩集My Hero Academia，終於追到最新一季了。
```

✗ Avoid:
```
- Person: Sarah
- Restaurant: Example Cafe
- Location: Tokyo
- Anime: My Hero Academia
```

### Links Section
At the end of each entry, list all entities mentioned:

```markdown
---
### Links
- **People:** [[250120-sarah]]
- **Places:** [[tokyo]], [[250120-example-cafe]]
- **Content:** [[mha]]
```

This enables:
- Obsidian graph view connections
- AI to quickly find related entities
- Bidirectional navigation

## Processing Rules (For AI)

When processing a timeline entry:

1. **Parse the natural language content**
2. **Identify entities mentioned:**
   - People → Check/create in /relationships
   - Places → Check/create in /experiences/places
   - Food/restaurants → Check/create in /experiences/food
   - Media → Check/create in /experiences/content
   - Activities → Check/create in /experiences/activities
   - Work mentions → Check/create in /work
   - Health info → Check/create in /health
   - Purchases → Check/create in /assets

3. **For each entity:**
   - If exists: Update `related_timeline` to include this entry
   - If new: Create entity file with basic info

4. **Update the Links section** in the timeline entry

## Querying Timeline

### By Date
```
Read timeline/2025/250120.md
```

### By Date Range
```
List files in timeline/2025/ between 250115 and 250120
```

### By Content
Search for keywords across timeline files, then read relevant entries.

## File Listing & Overview
While individual daily files are too numerous to list, `timeline/timeline_overview.md` **MUST** be updated after every write operation to `timeline/`.

### Overview Schema (`timeline/timeline_overview.md`)

```markdown
# Timeline Overview

## Status
- **Total Entries**: [Calculated Count]
- **Last Entry**: YYYY-MM-DD

## Yearly Statistics

### 2025
- **Dates**: 250101, 250102, ... (Do not list all if >50, just list range or months)
- **Key Events**:
  - 2025-01-20: [Event Name/Link]

### 2024
...
```

### Update Rule
1. When creating `timeline/YYYY/YYMMDD.md`:
2. Open `timeline/timeline_overview.md`.
3. Update **Total Entries** count.
4. Update **Last Entry** date.
5. Under the relevant Year section, ensure the new date is accounted for.
6. IF the entry represents a **Key Event** (Major Trip, Life Event, Milestone), add it to the **Key Events** list.

## Monthly/Yearly Summaries (Optional)

You may create summary files:
- `timeline/2025/_summary-01.md` — January 2025 summary
- `timeline/2025/_summary.md` — Full year 2025 summary

These are optional and can be AI-generated from daily entries.

## Notes

- Timeline is the **primary input** — everything else is derived
- Write freely; don't worry about structure in the content
- The Links section is the key to connecting entries to entities
- If something important happens, it goes in timeline first
- Review and tag entries periodically for better searchability
