# Examples

This folder contains example files demonstrating how the database works. These are **not real data** — they are fictional examples for reference.

## Contents

```
_examples/
├── README.md                 # This file
├── timeline/
│   └── 250315.md             # Example daily entry
├── relationships/
│   └── 250315-alex.md        # Example person entry (flat properties)
├── experiences/
│   ├── 250315-osaka.md       # Example place
│   ├── 250315-namba-ramen.md # Example restaurant
│   └── 250315-starbound-chronicles.md  # Example content (TV series)
└── logs/
    └── 250315_log.md         # Example AI processing log
```

## How to Use

1. **Review** these examples to understand the file structure
2. **Copy** a template from `_templates/` when creating new entries
3. **Delete** this `_examples/` folder once you're comfortable with the system

## The Example Scenario

All examples are based on a fictional day trip:

> "Spent the day exploring Osaka with Alex. Had lunch at a great ramen shop near Namba. The tonkotsu was rich and creamy. In the afternoon, visited Osaka Castle. Back at the hotel, watched a couple episodes of that sci-fi series everyone's been recommending."

This single input generated:
- 1 timeline entry (`250315.md`)
- 1 relationship entry (`250315-alex.md`)
- 3 experience entries (place, food, content)
- 1 processing log entry

## Key Features Demonstrated

### Flat Properties
All entity files use flat YAML properties instead of nested structures:
```yaml
# ✓ Correct (flat)
relationship_type: friend
met_date: 2020-09
location: Taipei

# ✗ Avoid (nested)
relationship:
  type: friend
  met_date: 2020-09
```

### Single File Sufficiency
Each entity contains:
- `description`: High-density summary
- `semantic_history` or `*_history`: Self-contained history log
- `related_timeline` and `related_entities`: Bidirectional links

### Change Log
Every entity has a Change Log section at the bottom for tracking modifications.

## Review each file to see how the AI would structure and link the data.
