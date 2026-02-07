# Configuration

The main configuration file is `config.json` in the mod data folder:

```
mods/Hexora_SpellbookPlus/config.json
```

## Full Configuration

```json
{
  "casting": {
    "instabilityEnabled": true
  },
  "projectile": {
    "timeoutMs": 30000,
    "cleanupIntervalSeconds": 1.0
  },
  "ui": {
    "hotbarMaxSlots": 9,
    "doubleClickThresholdMs": 400
  },
  "staffGlow": {
    "enabled": true,
    "tickInterval": 0.25
  },
  "damage": {
    "aoeBaseDamage": 50.0
  },
  "enchanting": {
    "xpPerHit": 2,
    "xpPerKill": 5,
    "basicRollCost": 50,
    "advancedRollCost": 150,
    "masterRollCost": 300
  },
  "passive": {
    "basicRollCost": 50,
    "advancedRollCost": 150,
    "masterRollCost": 300,
    "maxActivePassives": 3
  }
}
```

## Casting Settings

### instabilityEnabled

Enable or disable the instability system. When disabled, spells never fizzle or backfire regardless of complexity.

| Value | Description |
|-------|-------------|
| `true` | Instability system active (default) |
| `false` | Instability checks disabled |

## Projectile Settings

### timeoutMs

Maximum lifetime for spell projectiles in milliseconds. Projectiles are destroyed after this duration.

| Value | Range |
|-------|-------|
| Default | `30000` |
| Min | `1000` |

### cleanupIntervalSeconds

How often the projectile cleanup system runs, in seconds.

| Value | Range |
|-------|-------|
| Default | `1.0` |
| Min | `0.1` |

## UI Settings

### hotbarMaxSlots

Maximum number of spells in the spell hotbar.

| Value | Range |
|-------|-------|
| Default | `9` |
| Min | `1` |
| Max | `36` |

### doubleClickThresholdMs

Time window for detecting double-click interactions in milliseconds.

| Value | Range |
|-------|-------|
| Default | `400` |
| Min | `100` |

## Staff Glow Settings

### enabled

Enable or disable the staff glow particle effect.

| Value | Description |
|-------|-------------|
| `true` | Staff glow active (default) |
| `false` | Staff glow disabled |

### tickInterval

How often the staff glow system updates, in seconds.

| Value | Range |
|-------|-------|
| Default | `0.25` |
| Min | `0.05` |

## Damage Settings

### aoeBaseDamage

Base damage value for area-of-effect spell calculations.

| Value | Range |
|-------|-------|
| Default | `50.0` |
| Min | `1.0` |

## Enchanting Settings

### xpPerHit

Enchanting XP earned per spell projectile hit. Only applies to staff spell projectiles — melee hits do not award XP. Not awarded if the hit kills the target (kill XP is awarded instead). Set to `0` to disable hit XP entirely.

| Value | Range |
|-------|-------|
| Default | `2` |
| Min | `0` |

### xpPerKill

Enchanting XP earned per kill with a staff spell (projectile, AOE, or direct spell damage). Melee kills do not award XP.

| Value | Range |
|-------|-------|
| Default | `5` |
| Min | `1` |

### basicRollCost

XP cost to roll a Common tier enchantment.

| Value | Range |
|-------|-------|
| Default | `50` |
| Min | `1` |

### advancedRollCost

XP cost to roll an Rare tier enchantment.

| Value | Range |
|-------|-------|
| Default | `150` |
| Min | `1` |

### masterRollCost

XP cost to roll a Epic tier enchantment.

| Value | Range |
|-------|-------|
| Default | `300` |
| Min | `1` |

## Passive Settings

### basicRollCost

XP cost to roll a Common tier passive.

| Value | Range |
|-------|-------|
| Default | `50` |
| Min | `1` |

### advancedRollCost

XP cost to roll an Rare tier passive.

| Value | Range |
|-------|-------|
| Default | `150` |
| Min | `1` |

### masterRollCost

XP cost to roll a Epic tier passive.

| Value | Range |
|-------|-------|
| Default | `300` |
| Min | `1` |

### maxActivePassives

Maximum number of passives a player can have active simultaneously.

| Value | Range |
|-------|-------|
| Default | `3` |
| Min | `1` |

## Reloading Configuration

Use `/sb reload` to reload the configuration without restarting the server.
