# Knowledge Metadata

> Skills, credentials, and accumulated knowledge.

## Folder Purpose Distinction

### /knowledge vs Other Folders

| Folder | Contains | Example |
|--------|----------|---------|
| `/knowledge/skills` | Abilities user **can do** | "Can code in Python", "Speaks German" |
| `/knowledge/credentials` | Formal **qualifications** | "Bachelor's degree", "AWS certification" |
| `/knowledge/notes` | **Research & learning** records | "Comparison of hosting options", "Notes on color theory" |
| `/values/preferences` | **Opinions & tastes** | "Prefers minimalist design" |
| `/experiences/content` | **Media consumed** | "Watched documentary about X" |

### Key Distinction: Notes vs Experiences/Content

- **Notes**: Active research, learning, reference material → goes to `/knowledge/notes`
- **Content**: Passive consumption of media → goes to `/experiences/content`

Example:
- "Watched a YouTube tutorial about Docker" → `/experiences/content` (consumed media)
- "Research notes: Docker vs Kubernetes comparison" → `/knowledge/notes` (active learning)

## Subfolder Definitions

| Subfolder | Description | Examples |
|-----------|-------------|----------|
| `skills` | Abilities and competencies | Programming, video editing, languages |
| `credentials` | Formal qualifications | Degrees, certifications, licenses |
| `notes` | Research, learning, reference material | Topic research, comparisons, tutorials, insights |

## Notes Categories

The `notes` subfolder handles various types of knowledge capture:

```yaml
note_categories:
  research:      # Investigation into a topic (e.g., "hosting options comparison")
  reference:     # Collected reference material (e.g., "design inspiration sources")
  comparison:    # Evaluating options (e.g., "React vs Vue analysis")
  tutorial:      # How-to guides learned or created
  insight:       # Personal realizations or conclusions
  summary:       # Condensed information from longer sources
  checklist:     # Procedural knowledge (e.g., "deployment checklist")
  troubleshoot:  # Problem-solving records (e.g., "fixing nginx SSL issues")
```

### When to Create Notes

| Input Type | Action |
|------------|--------|
| "Researching X options" | Create `research` note |
| "Found good examples of X" | Create `reference` note |
| "Comparing A vs B" | Create `comparison` note |
| "Learned how to X" | Create `tutorial` note |
| "Realized that X works better when Y" | Create `insight` note |
| "Summary of article about X" | Create `summary` note |
| "Steps to deploy X" | Create `checklist` note |
| "Fixed issue with X by doing Y" | Create `troubleshoot` note |

## Entity Schemas

### Skills
```yaml
---
id: skill-slug
title: Skill Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: knowledge
subtype: skills
status: active | learning | dormant

skill:
  category: technical | creative | language | business | soft | other
  
  proficiency:
    level: beginner | intermediate | advanced | expert
    years_experience: 
    last_used:                   # When last used professionally
    
  # For technical skills
  technical:
    tools: []                    # Related software/frameworks
    versions: []                 # Specific versions (Python 3.11, React 18)
    
  # For languages
  language:
    speaking: native | fluent | conversational | basic
    reading: native | fluent | good | basic
    writing: native | fluent | good | basic
    certification:               # JLPT N1, TOEFL, etc.
    certification_date: 

  # For inferred skills (see Implicit Knowledge Inference in root _metadata.md)
  source: explicit | inferred
  inference_confidence: high | medium | low
  inference_basis:               # What evidence led to this inference

learning:
  started: 
  method:                        # Self-taught, course, degree, etc.
  resources: []                  # Books, courses, tutorials used
  
evidence:
  portfolio: []                  # Links to work demonstrating skill
  endorsements: []               # People who can vouch

notes:                           # Tips, gotchas, personal insights

tags: []
related_timeline: []
related_entities: []             # Link to projects using this skill
---
```

### Credentials
```yaml
---
id: credential-slug
title: Credential Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: knowledge
subtype: credentials
status: active | expired | revoked

credential:
  credential_type: degree | certification | license | award
  
  # For degrees
  degree:
    level: high_school | associate | bachelor | master | phd
    field: 
    major: 
    minor: 
    gpa: 
    honours:                     # Cum laude, etc.
    thesis_title: 
    
  # For certifications/licenses
  certification:
    issuer: 
    credential_id: 
    level:                       # If tiered (Level 1, N1, etc.)
    
  # Universal
  institution: 
  location:                      # Where the institution is
  instruction_language:          # Language of instruction
  date_issued: 
  date_expires:                  # If applicable
  
verification:
  url:                           # Verification link
  document:                      # Path to certificate file

# Implied knowledge from this credential (auto-infer these)
implied_skills: []               # Skills likely gained (e.g., language proficiency)
implied_experiences: []          # Experiences likely had (e.g., living abroad)

cost:                            # Cost to obtain
renewal:                         # Renewal requirements

notes: 

tags: []
related_timeline: []
related_entities: []
---
```

### Notes (Research/Learning)
```yaml
---
id: note-slug
title: Note Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: knowledge
subtype: notes
status: active | archived | superseded

note:
  category: research | reference | comparison | tutorial | insight | summary | checklist | troubleshoot
  topic: []                      # Subject areas
  
  # For research/comparison
  context:                       # Why this research was done
  conclusion:                    # What was decided/learned
  
  # For reference collections
  items: []                      # List of reference items with URLs/descriptions
  
  # For troubleshooting
  problem:                       # What issue was encountered
  solution:                      # How it was resolved
  environment:                   # System/software context
  
source:
  type: original | book | course | article | video | experience | conversation
  title: 
  author: 
  url: 

# For ongoing research
research_status: in_progress | concluded | abandoned
next_steps: []

tags: []
related_timeline: []
related_entities: []             # Link to related skills, projects
---

## Content

<!-- Main note content here -->

## Key Takeaways

<!-- Bullet points of main insights -->

## Action Items

<!-- Things to do based on this learning -->

## Questions

<!-- Unresolved questions for further research -->

## Updates

<!-- Log of updates to this note -->
```

files: []
# Example:


## Credential → Skill Inference Rules

When a credential is recorded, consider creating inferred skill entries:

| Credential Type | Likely Inferred Skills |
|-----------------|----------------------|
| Foreign university degree | Language proficiency (instruction language), cross-cultural experience |
| Cloud certification (AWS/GCP/Azure) | Cloud infrastructure, relevant programming, DevOps basics |
| Project management cert (PMP/PRINCE2) | Project management, stakeholder communication, team leadership |
| Photography/videography certificate | Camera operation, editing software, visual composition |
| Culinary degree | Cooking techniques, food safety, kitchen management |
| Music conservatory degree | Instrument proficiency, music theory, performance skills |
| Medical degree | Clinical skills, patient communication, medical knowledge |
| Law degree | Legal research, argumentation, regulatory knowledge |

### Recording Inferred Skills

When creating a skill entry inferred from a credential:

```yaml
source: inferred
inference_confidence: high
inference_basis: "Holds [credential type] from [institution in location]"
related_entities: ["[[credential-file]]"]
```

Example:
- User has MBA from INSEAD (France)
- Infer: French language (medium confidence), business/finance skills (high), European business context (medium)

## Notes Best Practices

1. **Title clearly**: Use descriptive titles like "Hosting Options Comparison 2025" not "Research"
2. **Link to decisions**: When research leads to action, link to related projects/purchases
3. **Update, don't duplicate**: If researching same topic again, update existing note
4. **Mark status**: Use `superseded` when newer research replaces old
5. **Capture context**: Record WHY research was done, not just WHAT was found

## Cross-Folder Relationships

Knowledge entities often relate to other folders:

| Knowledge Type | Related Folders |
|----------------|-----------------|
| Technical skill | `/work/projects`, `/assets/gear` |
| Language skill | `/experiences/places`, `/credentials` |
| Research note | `/values/preferences` (if led to preference), `/assets` (if led to purchase) |
| Credential | `/experiences/places` (study location), `/work/companies` (employer requirement) |

---

## Skill Dependency & Cascading Updates

When a skill or credential changes, check for related updates.

### Language Skill Dependencies

| Change | Check/Update |
|--------|--------------|
| Language level ↑ | Translation skill (if exists) |
| Language level ↑ | Interpretation skill (if exists) |
| Language certification acquired | Update base language skill level |
| Language reaches "fluent" | Consider creating translation/interpretation skills |

Example:
```
Input: "Passed JLPT N1"
Actions:
1. Create/update: credentials/260107-jlpt-n1.md
2. Update: skills/japanese.md → level: advanced or expert
3. Check: skills/japanese-translation.md → consider upgrade
4. Check: skills/japanese-interpretation.md → consider upgrade
5. Log all changes
```

### Technical Skill Dependencies

| Change | Check/Update |
|--------|--------------|
| Framework mastery ↑ | Base language skill level |
| New cloud certification | Cloud infrastructure skill |
| New tool proficiency | Related workflow skills |

Example:
```
Input: "Got AWS Solutions Architect certification"
Actions:
1. Create: credentials/260107-aws-sa.md
2. Update/create: skills/aws.md → level based on cert level
3. Check: skills/cloud-infrastructure.md → consider upgrade
4. Check: skills/devops.md → consider upgrade
```

### Creative Skill Dependencies

| Change | Check/Update |
|--------|--------------|
| New camera gear acquired | Photography skill evidence |
| Editing software mastery ↑ | Related production skills |
| Published work | Add to skill portfolio evidence |

### Cascading Rules

1. **Certification → Skill**: Always update matching skill when cert acquired
2. **Skill upgrade → Related skills**: Check if dependent skills should upgrade
3. **Evidence added → Skill level**: New portfolio items may justify level increase
4. **Do NOT auto-upgrade without evidence**: Flag for review instead

### Recording Skill Changes

When updating a skill due to related change:
```yaml
# In the skill file's Change Log:
| 2025-01-07 | Level: intermediate → advanced | AI |
| 2025-01-07 | Reason: JLPT N1 certification | AI |
```
