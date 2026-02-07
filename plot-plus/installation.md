# Installation

## Fresh Install

1. Download `PlotPlus-x.x.x.jar` from [CurseForge](https://curseforge.com)
2. Place the JAR file in your server's `mods` folder
3. Start the server
4. Edit `config.json` (optional)
5. Create a plot world with `/plot setup <world_name>` or `/plot setup <world_name> --template=<name>`

## Upgrading from v1

If you are upgrading from PlotPlus v1, see the [Migration Guide](migration.md) for important changes. The key steps:

1. Back up your `mods/Hexora_PlotPlus/` folder
2. Replace the old JAR with the v2 JAR
3. Start the server (database and language files migrate automatically)
4. **Update your permissions** — several permissions were renamed in v2

## File Structure

The plugin creates files in the mod data folder:

```
mods/Hexora_PlotPlus/
├── config.json          # Main configuration
├── plots.db             # SQLite database (default)
├── languages/           # Translation files (auto-extracted)
│   ├── en-US.json
│   ├── tr-TR.json
│   ├── de-DE.json
│   └── ...
└── templates/           # Plot templates
    ├── classic/
    │   └── template.yml
    └── bridge/
        └── template.yml
```

## Customizing Translations

Language files are automatically extracted to `languages/` on first run. You can edit these files to customize messages.

When the plugin updates and adds new translation keys, the **i18n auto-merge system** automatically adds missing keys to your files while preserving your customizations. You never need to manually update language files after a plugin update.

## Database Selection

### SQLite (Default)

No additional configuration required. Suitable for small to medium servers.

### MySQL

Recommended for large servers. In `config.json`:

```json
{
  "database": {
    "type": "mysql",
    "mysql": {
      "host": "localhost",
      "port": 3306,
      "database": "plotplus",
      "username": "root",
      "password": "password"
    }
  }
}
```

The database is created automatically.

## First Plot World

After installation:

```
/plot setup plots
```

This creates a world named `plots` using the default `classic` template.

Or with a specific template:

```
/plot setup plots --template=bridge
```
