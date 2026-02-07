# Configuration

The main configuration file is `config.json` in the plugin data folder:

```
mods/Hexora_PlotPlus/config.json
```

## Full Configuration

```json
{
  "database": {
    "type": "sqlite",
    "sqlite": {
      "file": "plots.db"
    },
    "mysql": {
      "host": "localhost",
      "port": 3306,
      "database": "plotplus",
      "username": "root",
      "password": ""
    }
  }
}
```

## Database Settings

### type

Database type to use.

| Value | Description |
|-------|-------------|
| `sqlite` | SQLite file database (default) |
| `mysql` | MySQL server database |

### sqlite.file

The SQLite database file name. Default: `plots.db`

### mysql.host

MySQL server hostname. Default: `localhost`

### mysql.port

MySQL server port. Default: `3306`

### mysql.database

MySQL database name. Default: `plotplus`

The database is created automatically if it doesn't exist.

### mysql.username

MySQL username. Default: `root`

### mysql.password

MySQL password. Default: empty

---

## Translations

Language files are stored in the `languages/` folder:

```
mods/Hexora_PlotPlus/languages/
```

### Supported Languages

| Code | Language |
|------|----------|
| `en-US` | English |
| `tr-TR` | Turkish |
| `de-DE` | German |
| `es-ES` | Spanish |
| `fr-FR` | French |
| `pt-BR` | Portuguese |
| `ru-RU` | Russian |
| `ja-JP` | Japanese |
| `ko-KR` | Korean |
| `zh-CN` | Chinese |

### Customizing Translations

1. Navigate to `mods/Hexora_PlotPlus/languages/`
2. Open the JSON file for your language (e.g., `en-US.json`)
3. Edit the messages as needed
4. Use `/plot reload` to apply changes

### i18n Auto-Merge

When PlotPlus updates and adds new translation keys, the **auto-merge system** automatically adds missing keys to your language files on startup. Your customizations are preserved — only new keys are added. You never need to manually update language files after a plugin update.

### Customizable Chat Prefix

Each language file includes a `"prefix"` key that controls the chat prefix (e.g., `[Plots]`). The prefix is **locale-aware** — each language can have its own prefix:

```json
{
  "prefix": "[Plots]"
}
```

Set `"prefix": ""` (empty string) to completely disable the prefix for a language.

### Example Translation File

```json
{
  "prefix": "[Plots]",
  "error": {
    "common": {
      "player_only": "This command can only be used by players.",
      "no_permission": "You don't have permission to do this."
    },
    "plot": {
      "not_claimed": "This plot is not claimed."
    }
  },
  "success": {
    "claim": {
      "claimed": "You have claimed this plot!"
    }
  }
}
```

### Placeholders

Translations support placeholders using `{placeholder}` format:

```json
"claimed_by_other": "This plot is owned by {owner}."
```

### Error ID Tracking

When an internal error occurs, players see a user-friendly message with a unique error ID (e.g., `a1b2c3d4`). Server admins can look up the full error details in the server logs using this ID.

### Migration from .lang Files

If you're upgrading from v1, your old `.lang` files are automatically moved to `languages/old/`. The auto-merge system handles all key changes automatically.

---

## Reloading Configuration

Use `/plot reload` to reload the configuration and translations without restarting the server.

Note: Database settings require a server restart to take effect.
