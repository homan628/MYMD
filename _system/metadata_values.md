# Values Metadata

> Beliefs, principles, goals, and preferences that guide decisions.

## Subfolder Definitions

| Subfolder | Description | Examples |
|-----------|-------------|----------|
| `principles` | Core beliefs and life rules | Decision frameworks, moral guidelines |
| `goals` | Objectives and aspirations | Annual goals, bucket list, OKRs |
| `preferences` | Likes, dislikes, settings | Food preferences, work style, pet peeves |
| `prompts` | AI interaction preferences | System prompts, tool settings |

## Entity Schemas

### Principles
```yaml
---
id: principle-slug
title: Principle Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: values
subtype: principles
status: active | revised | retired

principle:
  category: life | work | relationships | money | health | other
  
  statement:                     # The principle in one sentence
  
  origin:                        # Where this principle came from
    source:                      # Book, person, experience
    date_adopted: 
    
  application:                   # How to apply this principle
  
  examples: []                   # Times this principle was applied
  
  exceptions: []                 # When this principle doesn't apply

notes: 
reflection:                      # Personal thoughts on this principle

tags: []
related_timeline: []
related_entities: []
---
```

### Goals
```yaml
---
id: goal-slug
title: Goal Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: values
subtype: goals
status: active | achieved | abandoned | revised

goal:
  goal_type: annual | quarterly | monthly | life | project
  
  timeframe:
    year:                        # For annual goals
    quarter:                     # Q1, Q2, Q3, Q4
    deadline: 
    
  definition:
    objective:                   # What you want to achieve
    key_results: []              # Measurable outcomes (OKR style)
    # - description: 
    #   target: 
    #   current: 
    #   unit: 
    
  motivation:                    # Why this goal matters
  
  progress:
    percentage: 
    last_updated: 
    milestones: []
    # - description: 
    #   target_date: 
    #   completed_date: 
    
  blockers: []                   # What's preventing progress
  
  outcome:                       # Fill in when completed/abandoned
    result: 
    lessons: 
    next_steps: 

notes: 

tags: []
related_timeline: []
related_entities: []
---
```

### Preferences
```yaml
---
id: preference-slug
title: Preference Category
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: values
subtype: preferences
status: active

preference:
  category: food | work | environment | social | aesthetic | communication | other
  
  # For simple list-based preferences
  likes: []
  # - item: 
  #   intensity: love | like | prefer
  #   notes: 
  
  dislikes: []
  # - item: 
  #   intensity: hate | dislike | avoid
  #   notes: 
  
  neutral: []                    # Things you're indifferent to
  
  # For complex descriptive preferences (especially aesthetic/style)
  description: |
    # Free-form description for nuanced preferences that don't fit lists
    # Use this for aesthetic sensibilities, style preferences, etc.
  
  keywords: []                   # Key terms that capture this preference
  
  references: []                 # Examples, inspirations, reference points
  # - name: 
  #   url: 
  #   notes: 
  
  anti_references: []            # Things to avoid / negative examples
  
  # For settings/configurations
  settings: {}                   # Specific settings/configurations
  # e.g., for work preferences:
  # work_hours: "9am-6pm"
  # meeting_free_days: ["Wednesday"]
  # communication_preference: "async"

notes: 

tags: []
related_timeline: []
related_entities: []
---
```

### Preference Categories Explained

| Category | Use For | Example Fields |
|----------|---------|----------------|
| `food` | Dietary preferences, cuisines, restrictions | likes/dislikes lists |
| `work` | Work style, collaboration preferences | settings (hours, async/sync) |
| `environment` | Physical space, living preferences | description + keywords |
| `social` | Interaction style, social settings | settings + description |
| `aesthetic` | Visual style, design taste | description + references + keywords |
| `communication` | How user prefers to communicate | settings + description |
| `other` | Anything else | flexible |

### Aesthetic Preferences (Special Handling)

Aesthetic preferences are often too nuanced for simple likes/dislikes. Use:

```yaml
preference:
  category: aesthetic
  
  description: |
    Prefer organic, flowing designs with natural influences.
    Like muted color palettes with occasional accent colors.
    Appreciate texture and materiality over flat minimalism.
    
  keywords: 
    - organic shapes
    - natural materials
    - muted tones
    - tactile
    - artisanal
    
  references:
    - name: "Kinfolk magazine aesthetic"
      notes: "Clean but warm, natural light"
    - name: "Japanese ceramics"
      notes: "Wabi-sabi, imperfection"
      
  anti_references:
    - name: "Corporate Memphis illustration"
      notes: "Too generic, flat"
    - name: "Aggressive neon tech aesthetic"
      notes: "Too cold, overwhelming"
```

### When to Use Preferences vs Knowledge/Notes

| Input | Goes To |
|-------|---------|
| "I like minimalist design" | `values/preferences/aesthetic` |
| "Researched minimalist design principles" | `knowledge/notes/design-research` |
| "I prefer async communication at work" | `values/preferences/work` |
| "Best practices for async teams" | `knowledge/notes/async-work` |

### Prompts (AI Preferences)
```yaml
---
id: prompt-slug
title: Prompt/Setting Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: values
subtype: prompts
status: active | testing | retired

prompt:
  prompt_type: system_prompt | tool_setting | interaction_rule | persona
  
  target:                        # Which AI/tool this is for
    platform:                    # Claude, GPT, Cursor, etc.
    context:                     # Coding, writing, chat, etc.
    
  content: |
    # The actual prompt content
    
  variables: []                  # Placeholders to fill in
  
  usage:
    when_to_use: 
    examples: []
    
  effectiveness:
    rating:                      # How well it works 1-10
    notes: 
    
  version_history: []
  # - version: 1.0.0
  #   date: 
  #   changes: 

notes: 

tags: []
related_timeline: []
related_entities: []
---
```



## Notes

- For principles: Review periodically — values can evolve
- For goals: Use OKR format (Objective + Key Results) for clarity
- For preferences: Useful for AI to personalise responses
- For prompts: Version control your best prompts
- Link goals to projects in /work when relevant
