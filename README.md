# KupoDB

Free, public API for Final Fantasy Trading Card Game data.

Modeled after [Scryfall's](https://scryfall.com/docs/api) API design — typed JSON responses, cursor-based pagination, and rich search syntax with keyword:value queries.

> *"Kupo! The moogles keep all the records, kupo!"*

## Quick Start

```bash
# Search for cards
GET https://api.kupodb.com/cards/search?q=cloud+t:forward

# Get a card by serial number
GET https://api.kupodb.com/cards/serial/1-001H

# Browse all sets
GET https://api.kupodb.com/sets

# Name autocomplete
GET https://api.kupodb.com/cards/autocomplete?q=cl
```

## API Overview

### Response Format

Every response includes an `object` field for type discrimination:

```json
{
  "object": "list",
  "data": [...],
  "has_more": false,
  "next_page": null,
  "total_cards": 7
}
```

### Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/cards/search?q=...` | Search cards with query syntax |
| `GET` | `/cards/named?exact=...` | Card by exact name |
| `GET` | `/cards/named?fuzzy=...` | Card by fuzzy name match |
| `GET` | `/cards/random` | Random card |
| `GET` | `/cards/autocomplete?q=...` | Name autocomplete (up to 20 results) |
| `GET` | `/cards/:id` | Card by UUID |
| `GET` | `/cards/serial/:serial` | Card by serial number (e.g., `1-001H`) |
| `GET` | `/cards/:code/:number` | Card by set code + collector number |
| `POST` | `/cards/collection` | Batch lookup (up to 75 cards) |
| `GET` | `/sets` | List all sets |
| `GET` | `/sets/:code` | Set by code |
| `GET` | `/catalog/card-names` | All card names |
| `GET` | `/catalog/elements` | All elements |
| `GET` | `/catalog/card-types` | All card types |
| `GET` | `/catalog/jobs` | All jobs |
| `GET` | `/catalog/categories` | All categories |
| `GET` | `/catalog/artist-names` | All artists |
| `GET` | `/catalog/rarities` | All rarities |
| `GET` | `/bulk-data` | Available bulk exports |
| `GET` | `/bulk-data/all-cards` | All cards as JSON |
| `GET` | `/bulk-data/all-sets` | All sets as JSON |

### Search Syntax

Search uses keyword:value pairs with comparison operators. Terms are AND'd by default.

```
# By name (bare words)
cloud

# By type and element
t:forward e:fire

# By cost and power
cost>=3 power>5000

# By rules text
o:"when played"

# By job and category
job:soldier category:vii

# Negation
-t:summon

# Combined
cloud t:forward e:fire cost>=3
```

**Keywords**: `name:` `type:` / `t:` `element:` / `e:` `cost:` / `cp:` `power:` / `pow:` `oracle:` / `o:` `rarity:` / `r:` `set:` / `s:` `job:` / `j:` `category:` / `cat:` `artist:` / `a:` `is:` (ex, multi, reprint, foil)

**Operators**: `:` `=` `!=` `>` `<` `>=` `<=`

## Reporting Issues

- [Bug Report](https://github.com/KupoDB/kupodb/issues/new?template=bug_report.yml)
- [Feature Request](https://github.com/KupoDB/kupodb/issues/new?template=feature_request.yml)
- [Card Data Issue](https://github.com/KupoDB/kupodb/issues/new?template=card-data.yml)
- [Documentation Issue](https://github.com/KupoDB/kupodb/issues/new?template=documentation.yml)

## License

[Apache 2.0](LICENSE)
