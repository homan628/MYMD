# Experiences Metadata

> Things consumed, places visited, activities done.

## Subfolder Definitions

| Subfolder | Description | Examples |
|-----------|-------------|----------|
| `content` | Media consumed | Anime, movies, books, games, music, podcasts |
| `food` | Culinary experiences | Restaurants, cafes, recipes, ingredients |
| `places` | Locations visited | Countries, cities, landmarks, venues |
| `activities` | Things done | Sports, hobbies, events attended, exhibitions |

## Entity Schemas

### Content (Media)
```yaml
---
id: content-slug
title: Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: experiences
subtype: content
status: completed | watching | reading | playing | dropped | planned

content:
  content_type: anime | movie | tv_series | documentary | book | manga | article | game | music_album | music_track | podcast | youtube | other
  
  # For video/audio
  format: series | film | ova | ona | special
  episodes_total: 
  episodes_watched: 
  runtime:                       # For movies/episodes
  
  # For books/manga
  author: 
  pages: 
  publisher: 
  isbn: 
  
  # For games
  platform: []                   # PS5, PC, Switch, etc.
  playtime: 
  
  # For music
  artist: 
  album: 
  tracks: 
  
  # Universal
  genre: []
  year_released: 
  language: 
  
consumption:
  started_date: 
  completed_date: 
  rating:                        # 1-10 or 1-5
  review:                        # Short review
  would_recommend: true | false
  
source:                          # Where consumed
  platform:                      # Netflix, Kindle, Steam, etc.
  url: 

tags: []
related_timeline: []
related_entities: []
---
```

### Food
```yaml
---
id: food-slug
title: Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: experiences
subtype: food
status: active | closed | relocated

food:
  food_type: restaurant | cafe | bar | recipe | product
  
  # For establishments
  establishment:
    cuisine: []
    price_range:                 # $, $$, $$$, $$$$
    location: 
    address: 
    coordinates:                 # lat, long
    url: 
    phone: 
    hours: 
    
  # For recipes
  recipe:
    cuisine: 
    difficulty: easy | medium | hard
    prep_time: 
    cook_time: 
    servings: 
    ingredients: []
    steps: []
    source:                      # Where you got the recipe
    
  # For products/ingredients
  product:
    brand: 
    where_to_buy: 
    price: 

visits: []                       # Array of visit records
# - date: 2025-01-20
#   with: ["[[sarah]]"]
#   ordered: []
#   rating: 8
#   notes: 

overall_rating:                  # Average or overall impression
favourite_items: []

# Lifecycle (for closed establishments)
lifecycle:
  opened:                        # If known
  closed:                        # When it closed
  end_reason: closed | relocated | rebranded
  end_notes: |
    # Memories of this place
    # Last visit experience
  new_location:                  # If relocated

tags: []
related_timeline: []
related_entities: []
---

## About

[Description of this place/recipe]

## Signature Dishes

[Best items to order]

## Tips

[Recommendations]

## Memories

[For closed places — favourite visits, what made it special]

---
## Change Log

| Date | Change | By |
|------|--------|-----|
```

### Places
```yaml
---
id: place-slug
title: Place Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: experiences
subtype: places
status: visited | lived | planned | closed

place:
  place_type: country | city | neighbourhood | landmark | venue | accommodation
  
  location:
    country: 
    region:                      # State, prefecture, etc.
    city: 
    address: 
    coordinates: 
    
  # For accommodations
  accommodation:
    type: hotel | airbnb | hostel | friend | other
    url: 
    price_per_night: 

visits: []                       # Array of visit records
# - date_start: 2025-01-15
#   date_end: 2025-01-20
#   purpose: vacation | work | transit
#   with: ["[[sarah]]"]
#   highlights: []
#   rating: 9

# For places lived
lived:
  date_start: 
  date_end: 
  address: 
  type: owned | rented

# Lifecycle (for demolished/closed places)
lifecycle:
  closed:                        # When closed/demolished
  end_reason: demolished | closed | restricted | changed
  end_notes: |
    # Memories of this place

tips:                            # Travel tips, recommendations

tags: []
related_timeline: []
related_entities: []
---

## About

[Description]

## Highlights

[Best experiences here]

## Tips & Recommendations

[Practical advice]

## Memories

[For places no longer accessible — what you remember]

---
## Change Log

| Date | Change | By |
|------|--------|-----|
```

### Activities
```yaml
---
id: activity-slug
title: Activity Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: experiences
subtype: activities
status: active | completed | planned

activity:
  activity_type: sport | hobby | event | exhibition | concert | workshop | meetup | other
  
  # For recurring activities (hobbies/sports)
  recurring:
    frequency:                   # weekly, monthly, etc.
    started_date: 
    location: 
    
  # For one-time events
  event:
    date: 
    date_end:                    # If multi-day
    venue: 
    location: 
    organiser: 
    url:                         # Event page
    ticket_price: 
    
  # For sports/fitness
  sport:
    type:                        # cycling, running, gym, etc.
    distance: 
    duration: 
    route:                       # For outdoor activities
    personal_best: 

with: []                         # People involved
rating: 
notes: 
highlights: []

tags: []
related_timeline: []
related_entities: []
---
```

## Content Type Quick Reference

```yaml
anime: Japanese animation series or films
movie: Feature films
tv_series: Non-anime TV shows
documentary: Documentary films or series
book: Physical or ebook
manga: Japanese comics
article: Long-form articles, papers
game: Video games
music_album: Full albums
music_track: Individual songs
podcast: Podcast episodes or series
youtube: YouTube videos or channels
```



## Notes

- For content: Track what you're currently consuming vs completed
- For food: Record visits separately to track return visits
- For places: Link to related food/activities experienced there
- For activities: Distinguish one-time events from recurring hobbies
