---
id: 
title: 
created: {{date:YYYY-MM-DD}}
updated: {{date:YYYY-MM-DD}}
type: relationships
subtype: friends # family | friends | professional | pets | communities
status: active
last_verified: {{date:YYYY-MM-DD}}

# Core Properties (Flat)
relationship_type: 
met_date: 
met_context: 
nickname: 
birthday: 
location: 
occupation: 

# Contact
phone: 
email: 
social: []

# Description (Key context for RAG/Quick answers)
description: |
  # TODO: One-paragraph summary of who this is, key traits, and relationship dynamics.
  # Example: College friend, reliable, tech-savvy. Usually meet for coffee.

# History Log (Self-contained history to avoid reading timeline files)
# Format: { date: YYYY-MM-DD, event: "Event Name", summary: "What happened" }
semantic_history: []

# Links
related_timeline: []
related_entities: []

tags: []
---

## 📝 Notes & Context

<!-- Detailed relationships context, shared interests, ongoing topics -->

## ⏳ Interaction Log

<!-- AI will append key interactions here from `semantic_history` for human readability -->

---
## Change Log

| Date | Change | By |
|------|--------|-----|
| {{date:YYYY-MM-DD}} | Created | AI |
