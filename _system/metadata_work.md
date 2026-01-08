# Work Metadata

> Career, professional activities, projects, and achievements.

## Subfolder Definitions

| Subfolder | Description | Examples |
|-----------|-------------|----------|
| `companies` | Employers and own businesses | Current company, past employers, founded startups |
| `projects` | Individual projects or productions | Video productions, software projects, campaigns |
| `clients` | Clients served (for freelancers/agencies) | Corporate clients, agencies |
| `achievements` | Awards, recognition, milestones | Awards won, certifications earned, records set |

## Entity Schemas

### Companies
```yaml
---
id: company-slug
title: Company Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: work
subtype: companies
status: active | inactive | archived

company:
  full_name: 
  type: employer | own_business | partnership
  industry: []
  founded:                       # If own business
  website: 
  location: 

employment:                      # If employer
  role: 
  department: 
  start_date: 
  end_date: 
  is_current: true | false
  responsibilities: []

# Lifecycle (when employment/company ended)
lifecycle:
  started:                       # Start date
  ended:                         # End date
  end_reason: resigned | laid_off | fired | contract_ended | company_closed | acquired | retired
  end_notes: |
    # Context about leaving
    # What you learned, accomplished
    # Relationships to maintain
  next_step:                     # Where you went next

tags: []
related_timeline: []
related_entities: []             # Link to projects, clients, colleagues
---

## About

[Company description, your role]

## Responsibilities

[What you did]

## Achievements

[Key accomplishments]

## Memories

[For past jobs — favourite moments, lessons learned]

---
## Change Log

| Date | Change | By |
|------|--------|-----|
```

### Projects
```yaml
---
id: project-slug
title: Project Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: work
subtype: projects
status: active | completed | paused | cancelled

project:
  type: video_production | software | consulting | campaign | event | other
  role:                          # Your specific role
  client: "[[client-id]]"        # Link to client if applicable
  company: "[[company-id]]"      # Link to company if applicable
  start_date: 
  end_date: 
  budget: 
  team_size: 
  
deliverables: []                 # What was produced
outcome:                         # Results, impact
url:                             # Link to final product if public

# Lifecycle
lifecycle:
  started: 
  ended: 
  end_reason: completed | cancelled | transferred | on_hold
  end_notes: 

tags: []
related_timeline: []
related_entities: []
---

---
## Change Log

| Date | Change | By |
|------|--------|-----|
```

### Clients
```yaml
---
id: client-slug
title: Client Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: work
subtype: clients
status: active | inactive | archived

client:
  type: corporate | individual | agency | broadcaster | other
  industry: 
  contact_person: 
  first_project_date: 
  
relationship:
  status: active | dormant | ended
  total_projects:               # Count
  total_revenue:                # If tracking

# Lifecycle
lifecycle:
  started: 
  ended: 
  end_reason: completed | budget | acquired | contact_left | relationship_ended
  end_notes: 
  
notes:                          # Working style, preferences, etc.

tags: []
related_timeline: []
related_entities: []            # Link to projects
---

---
## Change Log

| Date | Change | By |
|------|--------|-----|
```

### Achievements
```yaml
---
id: achievement-slug
title: Achievement Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: work
subtype: achievements
status: active | archived

achievement:
  type: award | certification | milestone | recognition | publication
  date_achieved: 
  issuer:                       # Who gave the award/certification
  category:                     # Award category if applicable
  rank:                         # 1st place, finalist, etc.
  description: 

verification:
  credential_id: 
  url:                          # Link to verify

tags: []
related_timeline: []
related_entities: []            # Link to related project/company
---

---
## Change Log

| Date | Change | By |
|------|--------|-----|
```



## Handling Work Endings

### Left Job (Resigned/Laid Off/Fired)
```yaml
lifecycle:
  ended: 2025-01-07
  end_reason: resigned
  end_notes: |
    Left to pursue own business.
    Great team, learned a lot about production workflows.
    Stay in touch with: [names]
  next_step: "Started own company"
```

### Company Closed/Acquired
```yaml
lifecycle:
  ended: 2025-01-07
  end_reason: company_closed  # or acquired
  end_notes: |
    Company acquired by [X].
    Team dispersed to various companies.
```

### Client Relationship Ended
```yaml
lifecycle:
  ended: 2025-01-07
  end_reason: relationship_ended
  end_notes: |
    Completed final project.
    Contact person moved to different company.
```

## Cascading Updates

When work entity status changes:
1. Update the entity file with lifecycle info
2. Update related projects (mark as completed/ended)
3. Check client relationships
4. Create timeline entry for significant changes
5. Update work/work_overview.md

## Notes

- Link projects to clients and companies
- Track achievements with verifiable credentials when possible
- For freelancers: clients subfolder is particularly important
- Update project status as work progresses
- Preserve all history even when leaving jobs
