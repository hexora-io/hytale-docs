# Migration from v1

PlotPlus v2 is a major update with new features and restructured internals. **Most things migrate automatically, but permissions are a breaking change and must be updated manually.**

## What Migrates Automatically

### Database

The database schema is upgraded automatically on first startup. PlotPlus v2 runs 9 transactional migrations that add new tables and columns (aliases, descriptions, custom homes, marketplace). No data is lost.

### Language Files

Language files remain in JSON format. The new **i18n auto-merge system** automatically adds missing translation keys to your existing files on every startup, so you never need to manually update language files after a plugin update. Your customizations are preserved.

> If you are upgrading from a version older than v1.7.0 that still used `.lang` files, those are automatically moved to `languages/old/` and replaced with JSON files.

### Commands

All renamed commands keep their old name as an alias:

| Old Command | New Command | Old Still Works? |
|-------------|-------------|:----------------:|
| `/plot reset` | `/plot clear` | Yes |
| `/plot unmerge` | `/plot unlink` | Yes |
| `/plot ban` | `/plot deny` | Yes |
| `/plot untrust` | `/plot remove` | Yes |
| `/plot unclaim` | `/plot delete` | Yes |

`/plot transfer` has been replaced by `/plot setowner`, which is now **admin-only**. Players no longer have a transfer command.

## Breaking Changes

| Area | v1 | v2 |
|------|----|----|
| **Permissions** | `plots.unmerge` | `plots.unlink` |
| **Permissions** | `plots.claim` (for `/plot auto`) | `plots.auto` |
| **Permissions** | `plots.unclaim` | `plots.delete` |
| **Permissions** | `plots.ban` | `plots.deny` |
| **Permissions** | `plots.trust` (for untrust) | `plots.remove` |
| **Permissions** | `plots.reset` | `plots.clear` |
| **Permissions** | `plots.transfer` | Removed (now admin-only: `plots.admin.command.setowner`) |
| **Admin Permissions** | `plots.admin` (all-in-one) | 18 granular permissions (see [Permissions](permissions.md)) |
| **Plot Roles** | OWNER, TRUSTED, VISITOR, DENIED | OWNER, TRUSTED, MEMBER, GUEST, DENIED |
| **Translation Keys** | `error.player_only` | Reorganized to `error.common.player_only` |
| **Admin Command** | `/plot tp <world>` | `/plot worldtp <world>` |
| **Admin Command** | `/plot delete <world>` | `/plot deleteworld <world>` |
| **Command Behavior** | `/plot auto` claims only | `/plot auto` claims and teleports |
| **Command Meaning** | `/plot delete` was admin (delete world) | `/plot delete` is now player (delete own plot) |

## Step-by-Step Migration

### 1. Back Up

```
cp -r mods/Hexora_PlotPlus/ mods/Hexora_PlotPlus_v1_backup/
```

### 2. Replace the JAR

1. Remove the old v1 JAR from `mods/`
2. Place the v2 JAR in `mods/`

### 3. Start the Server

Start the server. PlotPlus v2 will:

- Run database migrations automatically
- Auto-merge any missing translation keys into your existing language files

### 4. Update Permissions

This is the only manual step. Update your permission plugin configuration:

```yaml
# Old v1 permissions → New v2 permissions
plots.unmerge    → plots.unlink
plots.unclaim    → plots.delete
plots.ban        → plots.deny
plots.reset      → plots.clear
plots.transfer   → (remove — now admin-only)

# New permissions to grant players
plots.auto       # /plot auto (was included in plots.claim)
plots.add        # /plot add (new member role)
plots.remove     # /plot remove (replaces untrust functionality)
plots.kick       # /plot kick (new command)
plots.middle     # /plot middle (new command)
plots.set.home   # /plot sethome (new command)
plots.alias.set  # /plot alias (new command)
plots.set.desc   # /plot desc (new command)
plots.confirm    # /plot confirm
plots.command.sell  # /plot sell (new command)
plots.command.buy   # /plot buy (new command)
```

If you use `plots.admin`, the granular admin permissions are optional. `plots.admin` still grants full admin access. See [Permissions](permissions.md) for the full list.

### 5. Verify

1. Check server logs for migration success messages
2. Test `/plot info` on an existing plot — data should be intact
3. Test `/plot list` — all player plots should appear
4. Test claiming and building on plots

## What's New in v2

Features with no v1 equivalent:

- **Plot Marketplace** — `/plot sell` and `/plot buy` for player-to-player plot trading
- **Membership System** — Members (build when owner online) vs Trusted (build anytime)
- **Plot Aliases** — Name your plots with `/plot alias` and visit them by name
- **Plot Descriptions** — Add descriptions with `/plot desc`, shown in `/plot info`
- **Custom Homes** — Set a custom teleport point with `/plot sethome`
- **Kick** — `/plot kick` to remove players from your plot, including `*` to kick all non-trusted
- **Granular Admin Permissions** — 18 specific admin permissions instead of all-or-nothing
- **i18n Auto-Merge** — Language files update automatically, preserving your customizations
- **Locale-Aware Prefix** — Chat prefix respects each language file's `"prefix"` setting
- **Error ID Tracking** — User-friendly error messages with unique IDs for server admins to look up in logs
