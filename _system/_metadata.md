---
version: 1.0.0
last_updated: 2025-01-08
---

# Vault Metadata

> **AI INSTRUCTION FILE**: Read this file first to understand the database structure and operation rules. Located at `_system/_metadata.md`.

## Overview

This is a personal knowledge database with structured folders for different aspects of life. Data flows from natural language input → timeline → entity files.



## File Reading Strategy

To minimise token usage, read files in this order based on operation type:

### For READ Operations (Queries)
```
1. _system/_metadata.md → Section "Folder Structure" only (understand what folders exist)
2. Target folder/[folder]_overview.md → Get file listings, counts, summaries
3. Specific entity files → Only if needed to answer query
```

### For WRITE Operations (Adding/Updating Data)
```
1. _system/_metadata.md → Full read (need all rules)
2. `_system/metadata_[folder].md` → Full read (need schema)
3. Target folder/[folder]_overview.md → Check existing files
4. Create/update entity files
5. Update [folder]_overview.md with new file info
6. Log to `_logs/YYMMDD_log.md`
```

### Quick Reference: Which File to Read

| Task | Read This |
|------|-----------|
| "What anime have I watched?" | `experiences/experiences_overview.md` |
| "Tell me about Alex" | `relationships/relationships_overview.md` → find path → read file |
| "Add new friend Sarah" | `_system/metadata_relationships.md` (need schema) |
| "What did I do last week?" | `timeline/timeline_overview.md` → specific date files |
| "List my camera gear" | `assets/assets_overview.md` |
| "What are my goals?" | `values/values_overview.md` |

### Metadata File Sizes (Approximate)

| File | Tokens | When to Read |
|------|--------|--------------|
| `[folder]_overview.md` | 200-500 | Queries, listings |
| `_metadata.md` | 2000-4000 | Writing, schema reference |
| `_system/_metadata.md` | 4000-6000 | First read, writing |

### Sectional Reading of System _metadata.md

If token-constrained, read only relevant sections:

| Section | Read When |
|---------|-----------|
| Folder Structure | Always (orientation) |
| File Naming Rules | Writing new files |
| Data Flow: Input Processing | Processing user input |
| Data Flow: Query Processing | Answering questions |
| Universal Frontmatter Schema | Writing any file |
| Content Merging Rules | Updating existing data |
| me.md Update Rules | User status changes |
| Correction & Amendment Flow | Fixing errors |
| Implicit Knowledge Inference | Analysing user input |
| AI Operational Rules | Always |
| Logging Requirements | After any write |

## Folder Structure

| Folder | Purpose | Subfolders |
|--------|---------|------------|
| `/relationships` | People, pets, communities in user's life | family, friends, professional, pets, communities |
| `/work` | Career and professional activities | companies, projects, clients, achievements |
| `/experiences` | Things user has consumed or done | content, food, places, activities |
| `/assets` | Things user owns | gear, digital, collections, financial |
| `/knowledge` | What user knows | skills, credentials, notes |
| `/health` | Physical and mental health | medical, biometrics, habits |
| `/values` | Beliefs and preferences | principles, goals, preferences, prompts |
| `/timeline` | Daily diary entries | Organised by year (2025/, 2026/, etc.) |
| `/_system` | System files & Metadata | `_logs`, `_templates`, `_examples`, `_metadata.md` |

## File Naming Rules

```
Timeline:  YYMMDD.md              → 250120.md
Entity:    YYMMDD-slug.md         → 250120-sarah-smith.md
Slug:      lowercase-with-dashes  → example-cafe-tokyo
```

When updating an existing entity, change the date prefix to current date.

## Data Flow: Input Processing

When user provides natural language input:

### Step 1: Always Create/Update Timeline
```
Input: "2025年1月20日和Sarah吃飯"
Action: Create or append to timeline/2025/250120.md
```

### Step 2: Extract Entities
Identify mentions of:
- People/pets → relationships/
- Places → experiences/places/
- Food/restaurants → experiences/food/
- Media (anime, movies, books, games) → experiences/content/
- Activities → experiences/activities/
- Health info → health/
- Work/projects → work/
- Assets/purchases → assets/
- Values/decisions → values/

### Step 3: Create/Update Entity Files
For each extracted entity:
1. Check if file exists (search by slug in relevant folder)
2. If exists: Update the file, change date prefix
3. If new: Create new file with today's date prefix

### Step 4: Establish Links
- In timeline: Add Links section with `[[entity-file]]` references
- In entity: Add `related_timeline` in frontmatter

## Data Flow: Query Processing

When user asks a question:

### Step 1: Classify Query Type
- **Time-based**: "What did I do in November 2025?" → Read timeline
- **Entity-based**: "Tell me about Sarah" → Read relationships
- **Aggregation**: "What anime have I watched?" → Read experiences/content/_metadata.md, then relevant files
- **Cross-reference**: "Who did I meet in Tokyo?" → Read timeline + relationships + places

### Step 2: Read Relevant Metadata
- Read the specific folder's metadata file in `_system/metadata_[folder].md` to get file listings
- Identify which files are relevant

### Step 3: Fetch Specific Files
- Only read files that will answer the question
- Do NOT read entire database

## Universal Frontmatter Schema

Every entity file MUST have these base fields:

```yaml
---
id: unique-slug                    # e.g., "sarah-smith", "example-cafe-tokyo"
title: Display Name                # e.g., "Sarah Smith", "Example Cafe Tokyo"
created: YYYY-MM-DD               # First created date
updated: YYYY-MM-DD               # Last modified date
type: [main-folder]               # relationships, work, experiences, etc.
subtype: [subfolder]              # friends, content, gear, etc.
status: active | inactive | archived
last_verified: YYYY-MM-DD         # Last time info was confirmed accurate

# Entity-specific properties go here (FLAT, not nested)
# e.g., relationship_type: friend (NOT relationship: { type: friend })

description: |
  # High-density summary for RAG retrieval
  
# History log for single-file sufficiency
semantic_history: []

# Links
related_timeline: []              # Links to timeline entries
related_entities: []              # Links to other entities

tags: []                          # Use tags from _system/_tags.md
---
```

### ⚠️ IMPORTANT: Use Flat Properties

**DO** use flat property names:
```yaml
relationship_type: friend
met_date: 2020-09
location: Tokyo
```

**DO NOT** use nested structures:
```yaml
relationship:
  type: friend
  met_date: 2020-09
person:
  location: Tokyo
```

Flat properties are easier for AI to parse and reduce token usage.

## Subfolder Definitions

### /relationships
```yaml
subfolders:
  family: Blood relatives, in-laws, adopted family
  friends: Personal friends (non-professional)
  professional: Colleagues, clients, business contacts
  pets: Animals user cares for
  communities: Groups, clubs, organisations
```

### /work
```yaml
subfolders:
  companies: Employers and own businesses
  projects: Individual projects or productions
  clients: Clients served (for freelancers)
  achievements: Awards, recognition, milestones
```

### /experiences
```yaml
subfolders:
  content: Media consumed (anime, movies, books, games, music, podcasts)
  food: Restaurants, cafes, recipes, ingredients
  places: Countries, cities, landmarks visited
  activities: Sports, hobbies, events attended
```

### /assets
```yaml
subfolders:
  gear: Physical equipment (cameras, computers, bikes)
  digital: Domains, software, crypto, accounts
  collections: Collectibles, memorabilia
  financial: Investments, major purchases
```

### /knowledge
```yaml
subfolders:
  skills: Abilities (technical, soft, languages)
  credentials: Degrees, certifications, licenses
  notes: Research notes, learning summaries
```

### /health
```yaml
subfolders:
  medical: Conditions, medications, doctors, history
  biometrics: Weight, fitness data, test results
  habits: Sleep, diet, exercise routines
```

### /values
```yaml
subfolders:
  principles: Core beliefs, life rules
  goals: Short and long-term objectives
  preferences: Likes/dislikes, settings
  prompts: AI interaction preferences, system prompts
```

### /timeline
```yaml
structure: Organised by year
format: /timeline/YYYY/YYMMDD.md
example: /timeline/2025/250120.md
```

## Content Type Classifications

For `/experiences/content/`, use these content_type values:

```yaml
content_types:
  - anime
  - movie
  - tv_series
  - documentary
  - book
  - manga
  - article
  - game
  - music_album
  - music_track
  - podcast
  - youtube
  - other
```

## Status Values

```yaml
entity_status:
  - active      # Current, ongoing
  - inactive    # Paused, dormant
  - archived    # Historical, no longer relevant
  - completed   # Finished (for projects, content)

relationship_status:
  - active      # In regular contact
  - inactive    # Lost touch
  - archived    # Ended relationship
```

## Link Format

### In Timeline Files
```markdown
---
### Links
- **People:** [[250120-sarah-smith]]
- **Places:** [[tokyo]], [[250120-example-cafe]]
- **Content:** [[250120-mha]]
```

### In Entity Files
```yaml
related_timeline: 
  - "[[timeline/2025/250120]]"
  - "[[timeline/2025/250125]]"
related_entities:
  - "[[250120-sarah-smith]]"
  - "[[tokyo]]"
```

## File Listing Location

File listings are maintained in each folder's `[folder]_overview.md` file (e.g., `relationships/relationships_overview.md`), NOT in the system metadata files.

## Subfolder Creation Rules

When creating entities that belong to a subfolder (e.g., `relationships/friends/`):

### Step 1: Check if Subfolder Exists
```
Does relationships/friends/ exist?
→ NO: Create the folder AND its overview file
→ YES: Proceed to create entity
```

### Step 2: Create Subfolder Overview (if new)
When creating a new subfolder:
1. Create the folder (e.g., `relationships/friends/`)
2. Create `[subfolder]_overview.md` inside it (e.g., `relationships/friends/friends_overview.md`)
3. Use template from `_system/_templates/tpl-subfolder-overview.md`

### Step 3: Update Both Overviews
After creating an entity:
1. Update the **subfolder overview** (e.g., `friends/friends_overview.md`)
2. Update the **parent folder overview** (e.g., `relationships/relationships_overview.md`)

### Auto-Generated Resources
The following resources are created automatically when needed:
- **Subfolders**: Created when first entity of that subtype is added
- **Subfolder overviews**: Created alongside new subfolders
- **Log files**: `_logs/YYMMDD_log.md` created when AI performs operations
- **Year folders in timeline**: Created when first entry of that year is added

## AI Operational Rules

1. **Always read `_system/_metadata.md` first** before any operation
2. **Log before acting** — write to `_system/_logs/YYMMDD_log.md` before making changes
3. **Timeline is mandatory** — every dated input creates/updates timeline
4. **Schema-Driven Instantiation (The Partitioning Rule)**:
   - **Do NOT use subjective judgment** to decide when to create a file.
   - **Check Input against Schemas**: Does the input contain data to fill the **Core Properties** of any defined Entity (Person, Place, Project, etc.)?
     - **YES** (Valid MVE) → **MUST create/update independent entity file**.
     - **NO** (Incomplete Info) → Keep in **Timeline** only.
5. **Preserve existing data** — update, don't overwrite unless instructed
6. **Maintain bidirectional links** — timeline ↔ entities
7. **Use consistent slugs** — same entity = same slug across files
8. **Update file listings** — keep `[folder]/[folder]_overview.md` current
9. **Respect privacy** — don't expose sensitive data in responses unless asked

## Minimum Viable Entity (MVE) Definitions

An entity file **MUST** be created if the input provides:

| Category | MVE Requirements (Must have ALL) |
|----------|----------------------------------|
| **Person** | Name + (Relationship Type OR Context of meeting) |
| **Place** | Name + Location (City/Region) |
| **Project** | Title + (Client OR Goal OR Technology) |
| **Content** | Title + (Type OR Creator OR Opinion) |
| **Food** | Name + Location |
| **Asset** | Item Name + (Brand OR Category) |
| **Goal** | Objective + Deadline/Timeframe |

*Example*:
- "I coded today." → Timeline only (No Project Title).
- "I coded the **Auth Module** for **Client X**." → Timeline + Create `work/projects/auth-module.md` (Matches Project MVE).

## Single File Sufficiency

To ensure high efficiency:
1.  **Atomic Files**: Every MVE gets a file.
2.  **Description**: Every file MUST have a `description` field in Frontmatter (or `DESCRIPTION` in Timeline comments) acting as a high-density summary for RAG.
3.  **Semantic History**: Links MUST include context (date, event, summary) so the AI doesn't need to read the linked file to understand the relationship.

Every AI processing session MUST:
1. Append to `_system/_logs/YYMMDD_log.md` (Create if not exists)
2. **Strict Chronological Order**: Standard append-only format
3. Header: `## YYYY-MM-DD HH:MM:SS - Session ID`
4. Log full input text
5. Document all actions taken with reasons
6. Include rollback instructions

See `_system/metadata_logs.md` for full logging schema if needed.

## Overview Scalability & Maintenance

To ensure `[folder]_overview.md` files remain usable as data grows:

### 1. Categorized Indexing
Do NOT create flat lists. Group entities by subtype or status.
- **Bad**: List of 500 books.
- **Good**:
  - `## Books (Reading)`
  - `## Books (Completed - 5 Star)`
  - `## Books (Technical)`

### 2. The "Active Only" Rule
If an overview file exceeds 500 lines:
- Move `status: archived` or `status: completed` items to `archive/[folder]_archive_YYYY.md`.
- Keep only active/relevant items in the main overview.

### 3. No "Jot Notes"
This system is a **Database**, not a notepad.
- **Random thoughts** → Stay in Timeline.
- **Entities** (reusable concepts) → Get their own files and Overview entries.

---

## Media Handling

**DO NOT** store binary media (images, videos, PDFs) in this Markdown vault.

### Rule: External References
Instead of embedding files, store them in your preferred cloud storage (iCloud, Dropbox, S3) and link them:

```yaml
attachments:
  - name: "Receipt.jpg"
    url: "https://dropbox.com/path/to/receipt.jpg"
  - name: "DesignSpec.pdf"
    path: "/Users/homan/Documents/Media/2025/DesignSpec.pdf" # Local absolute path
```

This keeps the text-based knowledge base lightweight and git-friendly.

---

## Tagging System

To prevent "Tag Entropy" (e.g., `#coding` vs `#dev` vs `#development`):

1. **Consult `_system/_tags.md`** before assigning tags.
2. **Prefer existing tags** over creating new ones.
3. **Hierarchical Tags** are encouraged (e.g., `#work/coding` instead of just `#coding`).

---

## Entity Lifecycle Management

Entities have lifecycles — they begin, change, and sometimes end. This section defines how to handle these transitions while preserving memories.

### Core Principle: Never Delete Memories

When something ends (sold, closed, deceased, etc.):
- **DO NOT** delete the entity file
- **DO** update status to `archived` or appropriate end state
- **DO** add `lifecycle` information
- **DO** preserve all linked timeline entries and relationships

### Lifecycle Schema

Add to any entity that has ended:

```yaml
lifecycle:
  started: YYYY-MM-DD          # When acquired/met/opened
  ended: YYYY-MM-DD            # When sold/closed/ended
  end_reason: [see table below]
  end_notes: |
    Free-form notes about the ending.
    Preserve memories and context here.
```

### End Reasons by Entity Type

| Entity Type | Valid End Reasons |
|-------------|-------------------|
| `assets/gear` | sold, broken, lost, donated, retired, stolen |
| `assets/financial` | sold, closed, matured, transferred |
| `relationships` (people) | ended, lost_touch, moved_away |
| `relationships` (family) | deceased |
| `relationships` (pets) | deceased, rehomed, lost |
| `relationships` (communities) | left, disbanded, inactive |
| `experiences/food` | closed, relocated, rebranded |
| `experiences/places` | demolished, restricted, changed |
| `work/companies` | left, closed, acquired, merged, laid_off, fired |
| `work/clients` | ended, inactive, acquired |
| `work/projects` | completed, cancelled, transferred |

### Handling Sensitive Endings

#### Deceased (People/Pets)
```yaml
lifecycle:
  ended: 2025-01-07
  end_reason: deceased
  end_notes: |
    [Handle with care and respect]
    
# Optional memorial section in body:
## In Memory
[Personal tribute, memories, impact on your life]
```

**AI Behavior**: 
- Handle with sensitivity in all responses
- Preserve all positive memories
- Never casually reference in queries

#### Relationship Ended
```yaml
lifecycle:
  ended: 2025-01-07
  end_reason: ended
  end_notes: |
    [Brief context if desired, or leave blank]
```

**AI Behavior**:
- Respect privacy
- Don't surface unless explicitly asked
- Preserve factual history (shared trips, etc.)

### Lifecycle Change Cascading

When an entity's lifecycle ends, check for cascading updates:

#### Asset Sold/Lost
```
1. Update: asset file (status: sold/lost, add lifecycle)
2. Check: work/projects using this asset
   → Add note: "Equipment sold [date]" if relevant
3. Optional: Create timeline entry for significant items
4. Update: assets/assets_overview.md
```

#### Relationship Ended
```
1. Update: relationship file (status: archived, add lifecycle)
2. DO NOT modify: timeline entries (history is history)
3. DO NOT modify: shared experiences
4. Update: relationships/relationships_overview.md
```

#### Restaurant/Business Closed
```
1. Update: food/place file (status: closed, add lifecycle)
2. Preserve: all visit records
3. Note: In future queries, mention "permanently closed since [date]"
4. Update: experiences/experiences_overview.md
```

#### Left Job/Company
```
1. Update: companies file (add end_date, lifecycle)
2. Update: related project files (status: completed if relevant)
3. Check: client relationships (may become inactive)
4. Preserve: all work history, achievements
5. Update: work/work_overview.md
```

---

## Change Log (Per-Entity History)

Every entity file should include a Change Log section at the bottom to track its own history.

### Format

```markdown
---
## Change Log

| Date | Change | By |
|------|--------|-----|
| 2025-01-07 | Created | AI |
| 2025-01-15 | Updated contact info | User |
| 2025-02-01 | Status: active → sold | AI |
```

### What to Log

| Event Type | Log Entry |
|------------|-----------|
| File created | "Created" |
| Status change | "Status: [old] → [new]" |
| Key info updated | "[Field] updated" |
| Lifecycle ended | "Ended: [reason]" |
| Correction made | "Corrected: [what]" |
| Major addition | "Added: [what]" |

### Two-Layer Logging System

| Layer | Location | Purpose |
|-------|----------|---------|
| Session Log | `_logs/YYMMDD_log.md` | AI operations, rollback capability |
| Entity Log | Each file's Change Log | Entity history, human-readable timeline |

Both should be maintained:
- Session logs for debugging and rollback
- Entity logs for understanding an entity's story

## Error Handling

If uncertain about classification:
1. Ask user for clarification
2. Default to most general category
3. Add `needs_review: true` to frontmatter

If file conflict detected:
1. Check if it's the same entity (compare id/title)
2. If same: merge information
3. If different: create with disambiguated slug (e.g., `peter-chen`, `peter-wong`)

---

## Content Merging Rules

When processing input that overlaps with existing data:

### Same Day, Same Topic
If two inputs on the same day cover the same topic:
- **Merge** into single timeline entry
- **Combine** information in entity file
- Example: Two inputs about design preferences → merge into one `preferences/aesthetic.md`

### Same Topic, Different Days
If inputs on different days cover the same evolving topic:
- **Separate** timeline entries (each day is distinct)
- **Update** the entity file with new information, change date prefix
- Example: Hosting research on Day 1, more research on Day 3 → two timeline entries, one updated `notes/hosting-research.md`

### Conflicting Information
If new input contradicts existing data:
- **Do NOT overwrite** silently
- **Ask user** to confirm which is correct
- **Add note** about the change if confirmed
- Example: "I live in Shibuya" conflicts with existing "lives in Meguro" → ask user

### Complementary Information  
If new input adds to existing data:
- **Append** to existing entity
- **Update** `updated` date
- Example: New restaurant visit → append to visits array in existing restaurant file

---

## me.md Update Rules

`me.md` represents **current state** — update it for present facts, not historical records.

### Update me.md When:
- Current location changes: "I moved to Berlin"
- Job/role changes: "I'm now a PM at Google"
- Contact info changes: "My new email is..."
- Status changes: "I'm now married"

### Do NOT Update me.md When:
- Historical information: "I used to live in Paris"
- Temporary states: "I'm visiting Seoul this week"
- One-time events: "I went to Berlin yesterday"

### Instead, Create/Update:
- `experiences/places/` for places visited or lived
- `timeline/` for events and activities
- `work/companies/` for job history

### Sync Rule
When me.md is updated:
1. Create timeline entry noting the change
2. Archive old state if significant (e.g., job change → update work/companies with end date)

---

## Correction & Amendment Flow

When user indicates previous data was wrong:

### Explicit Correction
User says: "Actually, that restaurant was in Ginza, not Shibuya"
1. **Update** the entity file with correct information
2. **Add to timeline**: Note the correction with context
3. **Add `corrected` field** to entity frontmatter:
```yaml
corrected:
  - date: 2025-01-07
    field: location
    from: Shibuya
    to: Ginza
    reason: User correction
```

### Deletion Request
User says: "Delete the entry about X"
1. **Confirm** with user before deleting
2. **Remove** entity file
3. **Update** related files (remove links)
4. **Note in timeline** if significant

### Retroactive Addition
User says: "I forgot to mention, I also met Sarah that day"
1. **Update** existing timeline entry
2. **Create** new entity if needed (e.g., sarah.md)
3. **Update** `updated` timestamp

---

## Implicit Knowledge Inference

When processing user input, infer background knowledge and skills from context clues. This helps build a more complete picture of the user without explicit statements.

### Inference Categories

#### Language Proficiency
| Clue | Inference |
|------|-----------|
| Watches foreign films without subtitles mention | Likely proficient in that language |
| Reads books in original language | Reading proficiency in that language |
| Works in foreign country | Working proficiency in local language |
| Graduated from foreign university | Academic proficiency in instruction language |
| Uses technical terms in foreign language | Domain-specific vocabulary |

#### Technical Skills
| Clue | Inference |
|------|-----------|
| Asks about framework-specific APIs | Familiar with that framework basics |
| Discusses deployment strategies | Has development experience |
| Uses IDE-specific terminology | Uses that development environment |
| Mentions version control workflows | Software development background |
| Asks about database optimisation | Backend development experience |

#### Domain Knowledge
| Clue | Inference |
|------|-----------|
| Uses industry jargon correctly | Industry experience or education |
| References specific tools of trade | Hands-on experience in field |
| Asks advanced questions in domain | Beyond beginner level |
| Compares professional options | Active practitioner |

#### Life Experience
| Clue | Inference |
|------|-----------|
| Graduated from foreign university | Study abroad experience |
| Works remotely across timezones | International work experience |
| Discusses visa/immigration | Immigration experience |
| Mentions specific local places | Has lived in or frequently visited area |

### Inference Rules

1. **Confidence Levels**
   - **High**: Direct statement ("I speak French")
   - **Medium**: Strong implication (graduated from French university)
   - **Low**: Weak implication (watched one French film)

2. **Recording Inferences**
   When creating/updating skill or knowledge entries from inference:
   ```yaml
   source: inferred
   inference_confidence: high | medium | low
   inference_basis: "Graduated from TU Berlin, instruction language German"
   ```

3. **Do NOT Infer**
   - Sensitive personal attributes
   - Political/religious beliefs
   - Financial status
   - Health conditions
   - Relationship status

4. **Validation**
   - High confidence inferences: Record directly
   - Medium confidence: Record with flag, may confirm later
   - Low confidence: Note in timeline only, don't create entity

### Inference Examples

**Input**: "I need to configure nginx reverse proxy for my Supabase project"
**Inferences**:
- Uses Linux servers (medium confidence)
- Familiar with web server configuration (medium)
- Knows Supabase/backend development (high)
- Self-hosts applications (high)

**Input**: "Looking for good soba restaurants near Shimokitazawa"
**Inferences**:
- Located in or visiting Tokyo (high)
- Familiar with Tokyo neighbourhoods (medium)
- Interested in Japanese cuisine (low - too common)

**Input**: "Need to improve my Lightroom workflow for event photography"
**Inferences**:
- Does photography (high)
- Uses Adobe Lightroom (high)
- Does event photography (high)
- Processes large volumes of photos (medium)

### Cross-Reference Building

When inference suggests a skill/knowledge:
1. Check if explicit record exists in `/knowledge/skills/`
2. If yes: Add inference as supporting evidence
3. If no: Create new skill entry with `source: inferred`

Link related inferences:
- Photography skills → likely owns camera gear → check `/assets/gear/`
- Backend development → likely has hosting/domains → check `/assets/digital/`
- Foreign language → likely has travel/residence history → check `/experiences/places/`
