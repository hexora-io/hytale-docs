# Commands

All commands use `/spellbook` or the alias `/sb`. Each command has its own permission node. Use `spellbook.*` to grant access to all commands. See [Permissions](permissions.md) for the full list.

## Command List

| Command | Description |
|---------|-------------|
| `/sb staff` | Give a spell staff |
| `/sb scroll` | Give a spell scroll |
| `/sb material` | Give crafting materials |
| `/sb reload` | Reload configuration and spell data |
| `/sb enchant` | Open the Enchanting Table UI |
| `/sb enchantment` | Manage enchantments |
| `/sb passive` | Manage passives |
| `/sb passives` | Open the Passives UI |
| `/sb spell` | Spell information commands |

## /sb staff

Gives a spell staff to the player.

```
/sb staff [--spell <type>] [--quality <tier>]
```

### Quality Tiers

| Tier | Damage | Mana Cost | Cooldown |
|------|--------|-----------|----------|
| `common` | +0% | +0% | +0% |
| `uncommon` | +10% | -5% | +0% |
| `rare` | +20% | -10% | -10% |
| `epic` | +35% | -15% | -20% |
| `legendary` | +50% | -25% | -30% |

### Examples

```
/sb staff
/sb staff --spell fireball
/sb staff --spell blink --quality legendary
```

## /sb scroll

Gives a spell scroll to learn a spell.

```
/sb scroll --spell <type>
```

### Examples

```
/sb scroll --spell fireball
/sb scroll --spell healing_light
```

Use the scroll to permanently learn the spell.

## /sb material

Gives crafting materials.

```
/sb material --material <name>
```

### Materials

| Material | Description |
|----------|-------------|
| `arcane_dust` | Common arcane dust from void creatures |
| `arcane_shard` | Uncommon crystallized arcane fragment |
| `arcane_crystal` | Rare fully formed arcane crystal |
| `spirit_essence` | Elemental energy from spirits |
| `ember_heart` | Smoldering core from flame golem |
| `golem_core` | Power source from crystal golems |
| `spell_scroll_blank` | Blank scroll for inscribing |
| `arcane_workbench` | Crafting station block |

### Examples

```
/sb material --material arcane_dust
/sb material --material arcane_workbench
```

## /sb reload

Reloads configuration, spell data, enchantments, and passives without restarting the server.

```
/sb reload
```

## /sb enchant

Opens the Enchanting Table UI for the player. Allows rolling for random enchantments using enchanting XP.

```
/sb enchant
```

## /sb enchantment

Manages enchantments on the player's staff.

```
/sb enchantment <action> <id>
```

### Actions

| Action | Description |
|--------|-------------|
| `add` / `apply` | Apply an enchantment to the player's staff |
| `remove` | Remove an enchantment from the player's staff |
| `list` | List active enchantments on the player's staff |
| `available` | List all registered enchantments |

### Examples

```
/sb enchantment add fire_burst
/sb enchantment remove fire_burst
/sb enchantment list
/sb enchantment available
```

## /sb passive

Manages passive abilities for the player.

```
/sb passive <action> <id>
```

### Actions

| Action | Description |
|--------|-------------|
| `add` / `activate` | Activate a passive |
| `remove` / `deactivate` | Deactivate a passive |
| `list` | List active passives with cooldown info |
| `available` | List all registered passives |
| `all` | Activate all available passives |
| `passives` | Open the Passives UI |

### Examples

```
/sb passive add mana_regen
/sb passive remove mana_regen
/sb passive list
/sb passive available
/sb passive all
```

## /sb passives

Opens the Passives UI for the player.

```
/sb passives
```

## /sb spell

Spell information subcommands.

### /sb spell list

Lists all registered spells with their ID, name, and category.

```
/sb spell list
```

### /sb spell info

Shows detailed information about a specific spell, including node graph, cooldown, mana cost, and instability level.

```
/sb spell info <id>
```

**Example:**

```
/sb spell info fireball
```

Output includes: spell ID, name, category, cooldown, mana cost, instability level, node count, and the full graph node listing.

### /sb spell translations

Lists available translations for a spell.

```
/sb spell translations <id>
```
