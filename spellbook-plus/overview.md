# Overview

Spellbook Plus is a node-based spell programming system for Hytale servers. Design custom spells with JSON node graphs, enchant your staffs, and unlock passive abilities.

## v2.0

Spellbook Plus v2 is a complete rewrite. If you are upgrading from v1, see the [Migration Guide](migration.md).

## Core Systems

### Spells

All spells are defined as node graphs — directed pipelines of connected nodes that execute in sequence. There are no hardcoded spells; every spell (including the 8 built-in ones) is a JSON file you can edit or replace.

- 22 node types across 4 categories (Trigger, Effect, Action, Modifier)
- 7 spell categories (Projectile, Damage, Heal, Utility, Defense, Buff, Debuff)
- Visual **[Spell Editor](https://spellbook-editor.hexora.io/)** for creating spells with drag-and-drop
- Instability system with threshold-based penalties
- Checksum validation for spell integrity

### Enchantments

Trigger-based effects that attach to staffs and fire automatically during combat.

- 3 tiers: Common, Rare, Epic
- 9 trigger types
- Enchanting Table UI with XP-based rolling
- Node-graph powered

### Passives

Persistent effects that activate automatically based on triggers or intervals.

- 3 tiers: Common, Rare, Epic
- Interval and trigger based activation
- Optional conditions
- Configurable max active passives per player

### Triggers

A unified trigger system drives all three systems:

| Trigger | Description |
|---------|-------------|
| `on_cast` | Spell is cast |
| `on_hit` | Projectile hits a target |
| `on_kill` | Caster kills a target |
| `on_damage_taken` | Caster takes damage |
| `on_heal` | Caster is healed |
| `on_expire` | Spell effect expires |
| `on_interval` | Repeating timer |
| `on_enter_combat` | Entering combat |
| `on_exit_combat` | Leaving combat |

## Built-in Spells

| Spell | Category | Mana | Cooldown | Description |
|-------|----------|------|----------|-------------|
| Fireball | Projectile | 18 | 3s | Fire projectile with AoE explosion |
| Frost Bolt | Projectile | 15 | 4s | Ice projectile that slows |
| Arcane Bolt | Projectile | 12 | 2s | Quick arcane projectile |
| Lightning | Damage | 25 | 6s | High-speed lightning projectile |
| Healing Light | Heal | 20 | 5s | Self heal |
| Force Push | Utility | 15 | 4s | AoE knockback with minor damage |
| Mana Shield | Defense | 30 | 10s | Damage absorption barrier |
| Blink | Utility | 25 | 8s | Teleport 12 blocks forward |

## Quick Start

1. [Installation](installation.md)
2. [Commands](commands.md)
3. [Permissions](permissions.md)

## Documentation

- [Configuration](configuration.md)
- [Spells](spells.md)
- [Enchantments](enchantments.md)
- [Passives](passives.md)
- [Items](items.md)
- [Drop Tables](drops.md)
- [API](api.md)
- [Migration from v1](migration.md)
