# Relationships Metadata

> People, pets, and communities in the user's life.

## Subfolder Definitions

| Subfolder | Description | Examples |
|-----------|-------------|----------|
| `family` | Blood relatives, in-laws, adopted family | Parents, siblings, spouse, children |
| `friends` | Personal friends (non-professional) | School friends, hobby friends, neighbours |
| `professional` | Work-related contacts | Colleagues, clients, mentors, industry contacts |
| `pets` | Animals user cares for | Cats, dogs, etc. |
| `communities` | Groups and organisations | Clubs, alumni associations, online communities |

## Entity Schema

```yaml
---
id: slug                         # Unique identifier (e.g., "jane-doe")
title: Full Name                 # Display name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: relationships
subtype: family | friends | professional | pets | communities
status: active | inactive | archived

# Relationship Details
relationship:
  to_user:                       # How they relate to user (friend, mother, client, etc.)
  met_date:                      # When first met
  met_context:                   # How they met (school, work, event, etc.)
  
# Basic Info (for people)
person:
  nickname:                      # What user calls them
  birthday: 
  location: 
  occupation: 
  contact:
    phone: 
    email: 
    social: []

# For Pets
pet:
  species: 
  breed: 
  birthday: 
  adopted_date: 

# For Communities
community:
  type:                          # Club, alumni, online, etc.
  platform:                      # Where it exists
  joined_date: 
  role:                          # Member, admin, founder, etc.

# Lifecycle (for ended relationships)
lifecycle:
  started:                       # When relationship began
  ended:                         # When relationship ended
  end_reason: ended | lost_touch | moved_away | deceased | left | disbanded | rehomed
  end_notes: |
    # Context about the ending, memories to preserve

# Metadata
tags: []
related_timeline: []
related_entities: []
---

## About

[Description of this person/pet/community]

## How We Met

[Story of first meeting]

## Memorable Moments

[Key memories, can link to timeline entries]

## In Memory

[Only for deceased — tribute, impact on life]

## Notes

[Additional context]

---
## Change Log

| Date | Change | By |
|------|--------|-----|
| YYYY-MM-DD | Created | AI/User |
```

## Handling Relationship Endings

### For People (friends, professional)
- Set `status: archived`
- Add `lifecycle` with `end_reason`
- Preserve all timeline links
- Add context in `end_notes` if desired

### For Family (deceased)
- Set `status: archived`
- Add `lifecycle` with `end_reason: deceased`
- Add "In Memory" section
- Handle with sensitivity in all AI responses

### For Pets (deceased/rehomed)
- Set `status: archived`
- Add `lifecycle` with appropriate reason
- Preserve all memories
- Add "In Memory" section if deceased

### For Communities (left/disbanded)
- Set `status: archived`
- Add `lifecycle` with reason
- Preserve membership history



## Notes

- For people: Include relationship context, not just contact info
- For pets: Track health info in /health if needed
- For communities: Link to related people who are also members
- Update `related_timeline` whenever this relationship appears in timeline
