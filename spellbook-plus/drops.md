# Drop Tables

Spellbook Plus v2 injects custom drop entries into Hytale's native drop system. When an NPC dies, the native system handles everything in a single pass — both vanilla items and custom materials drop together.

## How It Works

1. On startup, default drop tables are registered in code
2. JSON files in the `drops/` folder override or add new drop tables
3. Each drop table targets a native `ItemDropList` by its asset ID (e.g. `Drop_Spectre_Void`)
4. The plugin reads the existing native drop container, appends custom pools, and re-injects the merged result
5. When an NPC dies, Hytale's native system resolves the merged drop list and spawns all items

## Default Drop Tables

14 drop tables are included by default:

### Void NPCs

| Drop List ID | Custom Pool |
|---|---|
| Drop_Larva_Void | 12%: Arcane Dust (70w) / empty (30w) |
| Drop_Crawler_Void | 18%: Arcane Dust 1-2 (65w) / empty (35w) |
| Drop_Eye_Void | 35%: Arcane Dust 1-2 (40w) / Arcane Shard (30w) / empty (30w) |
| Drop_Spawn_Void | 40%: Arcane Shard (50w) / Arcane Dust 1-2 (25w) / empty (25w) |
| Drop_Spectre_Void | 60%: Arcane Crystal (40w) / Arcane Shard 1-2 (35w) / empty (25w) |

### Elemental Spirits

| Drop List ID | Custom Pool |
|---|---|
| Drop_Spirit_Root | 50%: Spirit Essence (60w) / empty (40w) |
| Drop_Spirit_Thunder | 50%: Spirit Essence (60w) / empty (40w) |
| Drop_Spirit_Frost | 50%: Spirit Essence (60w) / empty (40w) |

### Crystal Golems

| Drop List ID | Pool 1 | Pool 2 | Pool 3 |
|---|---|---|---|
| Drop_Golem_Crystal_Earth | 100%: Golem Core (30w) / Arcane Crystal 1-2 (40w) / empty (30w) | | |
| Drop_Golem_Crystal_Thunder | 100%: Golem Core (30w) / Arcane Crystal 1-2 (40w) / empty (30w) | | |
| Drop_Golem_Crystal_Frost | 100%: Golem Core (30w) / Arcane Crystal 1-2 (40w) / empty (30w) | | |
| Drop_Golem_Crystal_Sand | 100%: Golem Core (30w) / Arcane Crystal 1-2 (40w) / empty (30w) | | |
| Drop_Golem_Crystal_Flame | 100%: Golem Core (guaranteed) | 50%: Ember Heart (guaranteed) | 80%: Arcane Crystal 1-2 (guaranteed) |
| Drop_Golem_Firesteel | 100%: Golem Core (35w) / Arcane Crystal 1-2 (35w) / empty (30w) | | |

*w = weight. Higher weight = more likely to be selected within the pool.*

Native drops (Void Essence, Voidheart, Crystals, etc.) are preserved automatically. Custom pools are added alongside native drops.

## Custom Drop Tables

You can override defaults or add new drop tables by placing JSON files in the `drops/` folder inside the plugin data directory.

### JSON Format

```json
{
  "dropListId": "Drop_Spectre_Void",
  "pools": [
    {
      "chance": 0.60,
      "entries": [
        { "itemId": "Arcane_Crystal", "weight": 40, "min": 1, "max": 1 },
        { "itemId": "Arcane_Shard", "weight": 35, "min": 1, "max": 2 },
        { "weight": 25 }
      ]
    }
  ]
}
```

### Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `dropListId` | string | Yes | Native drop list asset ID to inject into (e.g. `Drop_Spectre_Void`) |
| `pools` | array | Yes | List of custom drop pools |

#### Pool Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `chance` | double | Yes | Probability of this pool activating (0.0 to 1.0) |
| `entries` | array | Yes | Weighted list of possible drops |

#### Entry Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `itemId` | string | No | Item to drop. Omit for an "empty" entry (nothing drops) |
| `weight` | int | Yes | Selection weight. Higher = more likely |
| `min` | int | Yes | Minimum drop quantity |
| `max` | int | Yes | Maximum drop quantity (inclusive) |

## Pools and Weights

Each drop table has one or more **pools**. Every pool is rolled independently.

**Pool chance** determines whether the pool activates:
- `1.0` = always activates (100%)
- `0.25` = activates 25% of the time
- `0.05` = activates 5% of the time (rare)

Within an activated pool, entries are selected by **weighted random**. For example, with entries weighing 40, 15, and 45 (total: 100):
- 40% chance for the first entry
- 15% chance for the second entry
- 45% chance for the third entry (empty = nothing drops)

**Empty entries** (no `itemId`) act as "nothing drops" outcomes.

## Examples

### Adding Drops to a New NPC

A Trork Warrior that has a 30% chance to drop arcane dust and a 10% chance to drop spirit essence:

```json
{
  "dropListId": "Drop_Trork_Warrior",
  "pools": [
    {
      "chance": 0.30,
      "entries": [
        { "itemId": "Arcane_Dust", "weight": 60, "min": 1, "max": 2 },
        { "itemId": "Arcane_Shard", "weight": 20, "min": 1, "max": 1 },
        { "weight": 20 }
      ]
    },
    {
      "chance": 0.10,
      "entries": [
        { "itemId": "Spirit_Essence", "weight": 100, "min": 1, "max": 1 }
      ]
    }
  ]
}
```

### Overriding a Default Drop Table

To change the Spectre Void custom drops (native drops are still preserved):

```json
{
  "dropListId": "Drop_Spectre_Void",
  "pools": [
    {
      "chance": 0.80,
      "entries": [
        { "itemId": "Arcane_Crystal", "weight": 50, "min": 1, "max": 2 },
        { "itemId": "Golem_Core", "weight": 10, "min": 1, "max": 1 },
        { "weight": 40 }
      ]
    }
  ]
}
```

## Finding Drop List IDs

The `dropListId` must match a native `ItemDropList` asset ID. These follow the pattern `Drop_<NpcName>`.

| NPC | Drop List ID |
|---|---|
| Void Larva | `Drop_Larva_Void` |
| Void Crawler | `Drop_Crawler_Void` |
| Void Eye | `Drop_Eye_Void` |
| Void Spawn | `Drop_Spawn_Void` |
| Void Spectre | `Drop_Spectre_Void` |
| Spirit Root | `Drop_Spirit_Root` |
| Spirit Thunder | `Drop_Spirit_Thunder` |
| Spirit Frost | `Drop_Spirit_Frost` |
| Crystal Golem Earth | `Drop_Golem_Crystal_Earth` |
| Crystal Golem Thunder | `Drop_Golem_Crystal_Thunder` |
| Crystal Golem Frost | `Drop_Golem_Crystal_Frost` |
| Crystal Golem Sand | `Drop_Golem_Crystal_Sand` |
| Crystal Golem Flame | `Drop_Golem_Crystal_Flame` |
| Firesteel Golem | `Drop_Golem_Firesteel` |

## Reloading

Drop tables are reloaded with `/sb reload`. Changes take effect immediately.
