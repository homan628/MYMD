# Health Metadata

> Physical and mental health tracking.

## Subfolder Definitions

| Subfolder | Description | Examples |
|-----------|-------------|----------|
| `medical` | Medical history and healthcare | Conditions, medications, doctors, procedures |
| `biometrics` | Body measurements and fitness data | Weight, body fat, FTP, VO2max |
| `habits` | Health routines and tracking | Sleep, diet, exercise, supplements |

## Entity Schemas

### Medical
```yaml
---
id: medical-slug
title: Record Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: health
subtype: medical
status: active | resolved | monitoring

medical:
  medical_type: condition | medication | procedure | vaccination | allergy | doctor | test_result
  
  # For conditions
  condition:
    name: 
    diagnosed_date: 
    diagnosed_by: "[[doctor-id]]"
    severity: mild | moderate | severe
    chronic: true | false
    symptoms: []
    treatment: 
    
  # For medications
  medication:
    name: 
    generic_name: 
    dosage: 
    frequency:                   # Once daily, twice daily, etc.
    purpose:                     # What it treats
    started_date: 
    ended_date: 
    prescriber: "[[doctor-id]]"
    side_effects: []
    
  # For procedures
  procedure:
    name: 
    date: 
    facility: 
    doctor: "[[doctor-id]]"
    reason: 
    outcome: 
    recovery_time: 
    
  # For vaccinations
  vaccination:
    vaccine: 
    date: 
    dose_number:                 # 1st, 2nd, booster
    facility: 
    lot_number: 
    next_due: 
    
  # For allergies
  allergy:
    allergen: 
    severity: mild | moderate | severe | life_threatening
    reaction: 
    diagnosed_date: 
    
  # For doctors/healthcare providers
  doctor:
    name: 
    specialty: 
    facility: 
    address: 
    phone: 
    last_visit: 
    
  # For test results
  test_result:
    test_name: 
    date: 
    facility: 
    results: {}                  # Key-value pairs of results
    normal_range: {}
    notes: 

notes: 

tags: []
related_timeline: []
related_entities: []
---
```

### Biometrics
```yaml
---
id: biometric-slug
title: Metric Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: health
subtype: biometrics
status: active

biometric:
  metric_type: weight | body_composition | fitness | vital | other
  unit:                          # kg, %, bpm, etc.
  
  # Current value
  current:
    value: 
    date: 
    
  # Target
  target:
    value: 
    deadline: 
    
  # History (or link to external tracking)
  history: []
  # - date: 2025-01-20
  #   value: 75.5
  
  tracking:
    method:                      # Scale, app, device
    frequency:                   # Daily, weekly, etc.
    device:                      # Apple Watch, Garmin, etc.

notes: 

tags: []
related_timeline: []
related_entities: []
---
```

### Habits
```yaml
---
id: habit-slug
title: Habit Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: health
subtype: habits
status: active | paused | stopped

habit:
  habit_type: sleep | diet | exercise | supplement | routine | other
  
  # For sleep
  sleep:
    target_hours: 
    target_bedtime: 
    target_waketime: 
    tracking_method:             # App, manual, device
    
  # For diet
  diet:
    type:                        # Keto, intermittent fasting, etc.
    restrictions: []             # Vegetarian, no dairy, etc.
    daily_calories: 
    macros:
      protein: 
      carbs: 
      fat: 
      
  # For exercise
  exercise:
    type:                        # Cycling, gym, running, etc.
    frequency:                   # 3x/week, daily, etc.
    duration:                    # Per session
    location: 
    
  # For supplements
  supplement:
    name: 
    dosage: 
    frequency: 
    purpose: 
    brand: 
    
  started_date: 
  current_streak:                # Days in a row
  longest_streak: 

notes: 

tags: []
related_timeline: []
related_entities: []
---
```



## Privacy Note

Health data is sensitive. Consider:
- Keeping this folder encrypted
- Not syncing to cloud
- Being selective about what to record

## Notes

- For medical: Keep vaccination records updated for travel
- For biometrics: Link to fitness activities in /experiences/activities
- For habits: Track streaks to maintain motivation
- Consider linking to timeline entries for context
