# Installation

## Requirements

- Hytale Server (Latest version)
- Java 25 or higher

## Optional Dependencies

| Mod | Purpose |
|-----|---------|
| [Hytalor](https://www.curseforge.com/hytale/mods/hytalor) | Native mana integration |
| [MultipleHUD](https://www.curseforge.com/hytale/mods/multiplehud) | HUD compatibility |

## Steps

1. Download `SpellbookPlus-x.x.x.jar` from [CurseForge](https://curseforge.com)
2. Place the JAR file in your server's `mods` folder
3. Start the server
4. Edit `config.json` (optional)
5. Use `/sb staff` to get your first spell staff

## File Structure

The mod creates files in the mod data folder:

```
mods/Hexora_SpellbookPlus/
├── config.json              # Main configuration
├── spells/                  # Custom spell overrides (JSON files)
├── enchantments/            # Custom enchantment overrides (JSON files)
├── passives/                # Custom passive overrides (JSON files)
├── drops/                   # Custom drop table overrides (JSON files)
└── languages/               # Translation files
    ├── en-US.json
    ├── tr-TR.json
    ├── de-DE.json
    ├── es-ES.json
    ├── fr-FR.json
    ├── ru-RU.json
    ├── ja-JP.json
    ├── ko-KR.json
    ├── pt-BR.json
    └── zh-CN.json
```

### Defaults and Overrides

All defaults (8 spells, 5 enchantments, 3 passives, 14 drop tables) are built into the plugin code. The folders above are empty on first launch — no default JSON files are written to disk.

To customize a default or add new content, place a JSON file in the corresponding folder. Files with matching IDs override the built-in defaults. Run `/sb reload` to apply changes.

### Spells Directory

Place spell JSON files in `spells/` to override defaults or add new spells. All spells use the node-graph format.

### Enchantments Directory

Place enchantment JSON files in `enchantments/` to override defaults or add new enchantments. Each file defines a single enchantment with its trigger, tier, and node graph.

### Passives Directory

Place passive JSON files in `passives/` to override defaults or add new passives. Each file defines a single passive with its trigger, interval, conditions, and node graph.

### Drops Directory

Place drop table JSON files in `drops/` to override defaults or add new drop tables. See [Drop Tables](drops.md) for the JSON format.

## Migration from v1

> **Warning:** There is no direct upgrade path from Spellbook Plus v1 to v2.
> v2 is a complete rewrite with different spell data formats, configuration structure, and API.
> See the [Migration Guide](migration.md) for details.

If you are upgrading from v1:

1. **Back up** your existing `mods/Hexora_SpellbookPlus/` directory
2. **Remove** the old JAR and data directory entirely
3. **Install** the v2 JAR as a fresh installation
4. Reconfigure settings in the new `config.json`

## First Spell Staff

After installation:

```
/sb staff --spell fireball --quality common
```

This gives you a common fireball staff to start casting spells.
