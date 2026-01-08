# Assets Metadata

> Things owned — physical, digital, and financial.

## Subfolder Definitions

| Subfolder | Description | Examples |
|-----------|-------------|----------|
| `gear` | Physical equipment | Cameras, computers, bikes, audio equipment |
| `digital` | Digital assets | Domains, software licenses, crypto, accounts |
| `collections` | Collectibles and memorabilia | Figures, art, stamps, cards |
| `financial` | Investments and major purchases | Stocks, property, vehicles |

## Entity Schemas

### Gear
```yaml
---
id: gear-slug
title: Item Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: assets
subtype: gear
status: active | sold | broken | lost | donated | retired

gear:
  category: camera | lens | computer | audio | cycling | vehicle | other
  
  product:
    brand: 
    model: 
    variant:                     # Color, size, etc.
    serial_number: 
    
  acquisition:
    date: 
    price: 
    currency: 
    source:                      # Store, person, etc.
    condition: new | used | refurbished
    
  current:
    condition: excellent | good | fair | poor
    location:                    # Where it's stored
    estimated_value: 
    
  specs: {}                      # Category-specific specifications
  
warranty:
  expires: 
  provider: 
  
maintenance:
  last_serviced: 
  service_history: []
  # - date: 
  #   type: 
  #   cost: 
  #   notes: 

# Lifecycle (when no longer owned)
lifecycle:
  started:                       # Acquisition date
  ended:                         # When sold/lost/etc.
  end_reason: sold | broken | lost | donated | retired | stolen
  end_notes: |
    # Details about ending
    # For sold: sale price, buyer info, memories
    # For broken: what happened
    # For lost/stolen: circumstances
  sale_details:
    price: 
    buyer: 
    platform:                    # Where sold

accessories: []
notes: 

tags: []
related_timeline: []
related_entities: []
---

## About

[Description, why you got it, what it meant to you]

## Usage History

[How you used it, notable projects/moments]

## Specifications

[Technical specs]

## Maintenance Log

[Service records]

## Memories

[For sold/lost items — what you remember, why it mattered]

---
## Change Log

| Date | Change | By |
|------|--------|-----|
| YYYY-MM-DD | Created | AI/User |
```

### Digital
```yaml
---
id: digital-slug
title: Asset Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: assets
subtype: digital
status: active | expired | sold | closed

digital:
  digital_type: domain | software | subscription | crypto | account | license
  
  # For domains
  domain:
    registrar: 
    expiry_date: 
    auto_renew: true | false
    dns_provider: 
    
  # For software/subscriptions
  software:
    license_type: perpetual | subscription | free
    license_key: 
    expiry_date: 
    seats:                       # Number of licenses
    
  # For crypto
  crypto:
    currency:                    # BTC, ETH, etc.
    wallet_address: 
    amount: 
    purchase_price: 
    current_value: 
    
  # For accounts
  account:
    platform: 
    username: 
    email: 
    created_date: 
    url: 

cost:
  initial: 
  recurring:                     # Monthly/yearly cost
  currency: 

# Lifecycle
lifecycle:
  started: 
  ended: 
  end_reason: expired | sold | closed | transferred | deleted
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

### Collections
```yaml
---
id: collection-slug
title: Item/Collection Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: assets
subtype: collections
status: active | sold | lost | donated

collection:
  category: figures | art | books | cards | memorabilia | other
  
  item:
    brand: 
    series: 
    name: 
    edition:                     # Limited, first edition, etc.
    condition: mint | near_mint | good | fair | poor
    
  acquisition:
    date: 
    price: 
    source: 
    
  value:
    estimated_current: 
    last_appraised: 

display:
  location:                      # Where displayed/stored
  insured: true | false

# Lifecycle
lifecycle:
  started: 
  ended: 
  end_reason: sold | lost | donated | damaged
  end_notes: 
  sale_details:
    price: 
    buyer: 

tags: []
related_timeline: []
related_entities: []
---

---
## Change Log

| Date | Change | By |
|------|--------|-----|
```

### Financial
```yaml
---
id: financial-slug
title: Asset Name
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: assets
subtype: financial
status: active | sold | closed | matured

financial:
  financial_type: stock | fund | property | vehicle | insurance | other
  
  # For investments
  investment:
    ticker:                      # Stock symbol
    platform:                    # Brokerage
    shares: 
    cost_basis: 
    purchase_date: 
    current_value: 
    
  # For property
  property:
    type: residential | commercial | land
    address: 
    purchase_date: 
    purchase_price: 
    current_value: 
    mortgage:
      lender: 
      remaining: 
      monthly_payment: 
      
  # For vehicles
  vehicle:
    type: car | motorcycle | bicycle | other
    make: 
    model: 
    year: 
    plate_number: 
    mileage: 
    purchase_date: 
    purchase_price: 
    
  # For insurance
  insurance:
    type: life | health | property | vehicle
    provider: 
    policy_number: 
    premium: 
    coverage: 
    expiry: 

# Lifecycle
lifecycle:
  started: 
  ended: 
  end_reason: sold | closed | matured | totaled | transferred
  end_notes: |
    # For vehicles: memories, road trips, why you sold
    # For property: memories of living there
  sale_details:
    price: 
    buyer: 
    gain_loss:                   # Profit or loss

tags: []
related_timeline: []
related_entities: []
---

## About

[Story of this asset — why you got it, what it meant]

## Memories

[For sold items — favourite moments, trips, experiences]

---
## Change Log

| Date | Change | By |
|------|--------|-----|
```

## Handling Asset Endings

### Sold
```yaml
lifecycle:
  ended: 2025-01-07
  end_reason: sold
  end_notes: |
    Sold after 30 years of ownership. Many great memories.
    Road trips to Hokkaido, weekend drives through mountain passes.
  sale_details:
    price: 15000000
    buyer: "Collector from Osaka"
```

### Broken/Totaled
```yaml
lifecycle:
  ended: 2025-01-07
  end_reason: broken  # or "totaled" for vehicles
  end_notes: |
    What happened and context.
    Memories of using this item.
```

### Lost/Stolen
```yaml
lifecycle:
  ended: 2025-01-07
  end_reason: lost  # or "stolen"
  end_notes: |
    Circumstances of loss.
    Police report filed: [yes/no]
    Insurance claim: [status]
```

## Cascading Updates

When asset status changes:
1. Update the asset file with lifecycle info
2. Check `work/projects` for projects using this asset
3. Create timeline entry for significant items
4. Update `assets/assets_overview.md`

files: []


## Notes

- For gear: Track serial numbers for warranty/insurance
- For digital: Set reminders for expiring domains/licenses
- For financial: Keep sensitive details secure (consider encryption)
- Link gear to projects where they're used
