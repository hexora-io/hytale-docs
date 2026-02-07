# Permissions

## Permission Nodes

| Permission | Description | Default |
|------------|-------------|---------|
| `spellbook.*` | Grants access to all commands (wildcard) | OP |
| `spellbook.command.staff` | `/sb staff` — Give spell staffs | OP |
| `spellbook.command.scroll` | `/sb scroll` — Give spell scrolls | OP |
| `spellbook.command.material` | `/sb material` — Give crafting materials | OP |
| `spellbook.command.reload` | `/sb reload` — Reload configuration | OP |
| `spellbook.command.enchant` | `/sb enchant` — Open Enchanting Table UI | OP |
| `spellbook.command.enchantment` | `/sb enchantment` — Manage enchantments | OP |
| `spellbook.command.passive` | `/sb passive` — Manage passives | OP |
| `spellbook.command.passives` | `/sb passives` — Open Passives UI | OP |
| `spellbook.command.spell` | `/sb spell` — Spell info commands | OP |

## How It Works

Spellbook Plus uses Hytale's native permission system with hierarchical wildcard support:

- `*` — Grants all permissions (OP group has this by default)
- `spellbook.*` — Grants all Spellbook Plus commands
- `spellbook.command.*` — Grants all Spellbook Plus commands
- `spellbook.command.staff` — Grants only the staff command

Permission denial is also supported with the `-` prefix:

- `-spellbook.command.reload` — Denies the reload command even if `spellbook.*` is granted

### Examples

Give a player access to only the enchanting UI:
```json
{
  "users": {
    "player-uuid": {
      "permissions": ["spellbook.command.enchant"]
    }
  }
}
```

Give a group full admin access to all Spellbook commands:
```json
{
  "groups": {
    "SpellbookAdmin": ["spellbook.*"]
  }
}
```

## Notes

- Regular players can cast spells without any special permissions
- Players need to learn spells via scrolls or be given staffs by admins
- Enchantments and passives can be managed by admins via commands, or by players through the UI
