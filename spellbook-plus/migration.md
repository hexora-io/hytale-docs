# Migration from v1

Spellbook Plus v2 is a complete rewrite. **There is no direct upgrade path from v1 to v2.** You must perform a clean installation.

## Why Direct Migration Is Not Possible

v2 fundamentally changes how spells, configuration, and the API work:

- Spells are no longer hardcoded; they are JSON node-graph definitions
- The configuration structure is entirely different (7 sections vs old 3)
- All data models are now records instead of mutable classes
- The service layer has been redesigned (new interfaces, new access pattern)
- New systems (enchantments, passives, triggers) have no v1 equivalent
- ECS components have been added and changed

## Breaking Changes

| Area | v1 | v2 |
|------|----|----|
| **Spell System** | 8 hardcoded spells | Node-graph JSON files, unlimited custom spells |
| **Spell Definition** | Class-based `SpellDefinition` | Record-based `SpellDefinition` with graph, checksum, translations |
| **Node Types** | 8 basic types (damage, heal, projectile, effect, push, shield, teleport, conditional) | 22 types in 4 categories (Trigger, Effect, Action, Modifier) |
| **Configuration** | `execution`, `cooldown`, `instability`, `mana`, `hud`, `storage` sections | `casting`, `projectile`, `ui`, `staffGlow`, `damage`, `enchanting`, `passive` sections |
| **Service Access** | `ServiceRegistry.get(Class)` | `SpellbookPlugin.getInstance().getXxxService()` |
| **Cooldown API** | `ICooldownManager` with `canCast`, `applyCooldown` | `CooldownService` with `isOnCooldown`, `setCooldown`, `reduceCooldown` |
| **Mana API** | `IManaManager` with `hasMana`, `consumeMana` | Removed from public API (handled internally) |
| **Storage** | `ISpellStorage` interface | `FileSpellRepository` with `SpellDataLoader` |
| **Enchantments** | Not available | Full system: tiers, triggers, XP, Enchanting Table UI |
| **Passives** | Not available | Full system: tiers, triggers, intervals, conditions, Passives UI |
| **Commands** | 4 commands (staff, scroll, material, reload) | 9+ commands including enchant, enchantment, passive, passives, spell subcommands |
| **Data Format** | Flat spell definitions | Nested node-graph with connections |
| **File Structure** | `spellbook/spells/` | `spells/`, `enchantments/`, `passives/`, `languages/` |
| **Triggers** | 3 types (on_cast, on_hit, on_expire) | 9 types (+ on_kill, on_damage_taken, on_heal, on_interval, on_enter_combat, on_exit_combat) |
| **I18n** | Built-in English strings | Custom I18n system with external language files, per-spell translations |
| **Node Handler** | `SpellNodeHandler` abstract class | `NodeHandler` functional interface |

## Migration Steps

Since direct migration is not possible, follow these steps:

### 1. Back Up v1 Data

```
cp -r mods/Hexora_SpellbookPlus/ mods/Hexora_SpellbookPlus_v1_backup/
```

### 2. Clean Install v2

1. Remove the old v1 JAR file
2. Remove the `mods/Hexora_SpellbookPlus/` directory
3. Install the v2 JAR in `mods/`
4. Start the server to generate default files

### 3. Reconfigure

The v1 config keys do not exist in v2. You must configure v2 from scratch.

**v1 config.json:**
```json
{
  "execution": { "maxNodesPerExecution": 50, "maxExecutionDepth": 10 },
  "cooldown": { "globalCooldownMs": 500, "minimumCooldownMs": 100 },
  "instability": { "safeThreshold": 50, "warningThreshold": 75, "dangerThreshold": 100, "catastrophicThreshold": 150 },
  "mana": { "useNativeMana": false },
  "hud": { "manaBarEnabled": true, "showOnlyWithStaff": true },
  "storage": { "storagePath": "spellbook/spells" }
}
```

**v2 config.json:**
```json
{
  "casting": { "instabilityEnabled": true },
  "projectile": { "timeoutMs": 30000, "cleanupIntervalSeconds": 1.0 },
  "ui": { "hotbarMaxSlots": 9, "doubleClickThresholdMs": 400 },
  "staffGlow": { "enabled": true, "tickInterval": 0.25 },
  "damage": { "aoeBaseDamage": 50.0 },
  "enchanting": { "xpPerHit": 2, "xpPerKill": 5, "basicRollCost": 50, "advancedRollCost": 150, "masterRollCost": 300 },
  "passive": { "basicRollCost": 50, "advancedRollCost": 150, "masterRollCost": 300, "maxActivePassives": 3 }
}
```

### 4. Custom Spells

If you had customized v1 spells, you need to recreate them as v2 node-graph JSON files. See [Spells](spells.md) for the v2 format.

### 5. API Consumers

If you have other mods that depend on the Spellbook Plus API, they must be updated:

- Replace `ServiceRegistry.get()` calls with `SpellbookPlugin.getInstance()`
- Update to new service interfaces (`CooldownService`, `SpellService`)
- Use record-based models (`SpellDefinition`, `SpellNode`, `SpellGraph`)
- Register custom nodes with `NodeHandler` functional interface instead of extending `SpellNodeHandler`

## What's New in v2

Features that have no v1 equivalent:

- **Enchantment System** — Trigger-based effects on staffs with XP rolling
- **Passive System** — Persistent abilities with interval and trigger activation
- **9 Trigger Types** — Expanded from 3 to 9 event types
- **Enchanting Table UI** — Visual enchantment rolling interface
- **Passives UI** — Visual passive management interface
- **Per-Spell Translations** — Localization support per spell
- **Spell Info Commands** — `spell list`, `spell info`, `spell translations`
- **13 New Node Types** — status_effect, aoe, glow, particle, mana_restore, and 8 new triggers
