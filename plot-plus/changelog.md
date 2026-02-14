# Changelog

All notable changes to this project will be documented in this file.

---

## [2.0.0-beta.4] - 2026-02-14

### Breaking Changes

#### Permission Standardization
All command permissions now follow a consistent `plots.<command>` format:

| Old Permission | New Permission |
|----------------|----------------|
| `plots.set.home` | `plots.sethome` |
| `plots.set.desc` | `plots.description` |
| `plots.alias.set` | `plots.alias` |
| `plots.command.sell` | `plots.sell` |
| `plots.command.buy` | `plots.buy` |
| `plots.admin.command.setowner` | `plots.setowner` |
| `plots.admin.alias.set` | `plots.admin.command.alias` |

#### Admin Commands Grouped
All admin commands are now under `/plot admin`:
- `/plot setup` → `/plot admin setup`
- `/plot reload` → `/plot admin reload`
- `/plot worldtp` → `/plot admin worldtp`
- `/plot deleteworld` → `/plot admin deleteworld`
- `/plot regenroads` → `/plot admin regenroads`

#### `/plot setowner` is Now a Player Command
- Plot owners can transfer their own plots (permission: `plots.setowner`)
- Admins with `plots.admin.command.setowner` can transfer any plot

### New Features

#### `/plot regenroads` Admin Command
- Regenerate all roads, walls, and intersections in a plot world
- Useful after changing templates or prefab files
- Chunk-aware: regenerates roads in all generated areas
- Non-blocking: server stays fully responsive during regeneration
- Permission: `plots.admin.command.regenroads`

#### `server_plot` Flag
- Mark a plot as server-owned with `/plot flag set server_plot true`
- Server plots display "Server" as the owner in `/plot info`
- Admin-only flag (requires `plots.admin` permission)

#### Flag Subcommands
- Flags now use explicit subcommands: `/plot flag set <flag> <value>` and `/plot flag remove <flag>`

#### Corner Prefab Support
- Intersections surrounded by 3 closed sides now use a dedicated corner prefab
- Add `corner_prefab` to your template's `border.json` to customize corner intersections
- Supports automatic rotation based on the open side direction

#### `/p` Command Alias
- `/p` now works as a shortcut for `/plot`

### Improvements

#### Protection System Migration
- BuilderTools protection (selection, transform, paste, line tool) moved to patch-level Hyxin mixins via PlotPlus-Patches
- Crop harvest protection moved to patch-level mixins
- Fluid spread protection across plot boundaries via patch-level mixins

#### Prefab Walls Toggle
- Templates can control whether walls are placed between plots using `"walls"` in `border.json`
- Set `"walls": false` to disable wall generation entirely

#### Chain Merge Improvements
- Improved road removal logic when merging plots in chain configurations

#### Performance
- Improved protection check performance with lazy caching
- Merge/unmerge and worldgen performance optimizations

### Fixed
- `/plot setowner` crash when target player was on a different world thread
- Admin `/plot setowner` now bypasses target player's plot limit
- Fluid spread no longer crosses plot boundaries
- `{price}` placeholder not working in claim messages
- Setup command showing incorrect `/plot tp` instead of `/plot admin worldtp`

---

## [2.0.0-beta.3] - 2026-02-07

### New Features

#### Auto-Claim Teleport
- `/plot auto` now automatically teleports you to the claimed plot after a successful claim

### Improvements

#### Locale-Aware Message Prefix
- The chat prefix (e.g. `[Plots]`) now correctly respects **each language file's** `"prefix"` setting
- Setting `"prefix": ""` in a language file now fully disables the prefix in all messages

#### Better Error Messages
- Command errors now show a user-friendly message with a unique error ID instead of raw error text
- Server admins can use the error ID to find the full details in server logs
- Error messages are fully translated in all 10 supported languages

### Fixed
- Fixed MySQL database connection not working
- Fixed `{price}` placeholder not working in `/plot claim` and `/plot auto` messages
- Fixed potential server crash when async command execution encountered errors

---

## [2.0.0-beta.2] - 2026-01-30

### New Features

#### Customizable Chat Prefix
- Chat prefix `[Plots]` is now fully customizable via language files
- Set `"prefix": "YourPrefix"` in any language file to customize
- Set `"prefix": ""` (empty) to completely disable the prefix
- Each language can have its own prefix (e.g., Turkish uses `[Arsalar]`)

#### i18n Auto-Merge System
- Missing translation keys are now automatically added to user language files
- When new keys are added in updates, they merge into existing translations
- User customizations are preserved during merge
- Eliminates need to manually update language files after plugin updates

### Improvements
- Turkish translations updated with proper Turkish characters (ö, ü, ç)
- All language files restructured to new nested JSON format

---

## [2.0.0-beta.1] - 2026-01-30

### Breaking Changes

This is a major update with breaking changes. See the [Migration Guide](migration.md) for upgrade instructions.

#### Permission Changes
| Old Permission | New Permission |
|----------------|----------------|
| `plots.unmerge` | `plots.unlink` |
| `plots.unclaim` | `plots.delete` |
| `plots.ban` | `plots.deny` |
| `plots.reset` | `plots.clear` |
| `plots.claim` (for /plot auto) | `plots.auto` |
| `plots.transfer` | Removed (now `plots.admin.command.setowner`) |

#### Translation Key Changes
All translation keys have been restructured. The i18n auto-merge system handles this automatically.

### New Features

#### Plot Marketplace
- `/plot sell <price>` - List your plot for sale
- `/plot sell cancel` - Remove plot from sale
- `/plot buy` - Purchase the plot you're standing on
- Sale status shown in `/plot info`
- New permissions: `plots.sell`, `plots.buy`

#### New Commands
- `/plot kick <player|*>` - Kick players from your plot
- `/plot middle` - Teleport to plot center (works with merged plots)
- `/plot sethome` - Set custom home location for your plot
- `/plot alias <name>` - Give your plot a custom name
- `/plot desc <text>` - Set a description for your plot
- `/plot add <player>` - Add player as member (can build when owner is online)
- `/plot delete` - Delete your own plot (with refund if economy enabled)

#### Command Renames
Old names still work as aliases:
- `/plot reset` → `/plot clear`
- `/plot unmerge` → `/plot unlink`
- `/plot ban` → `/plot deny`
- `/plot untrust` → `/plot remove`
- `/plot transfer` → `/plot setowner` (now admin-only)

#### Granular Admin Permissions
18 specific admin permissions instead of all-or-nothing `plots.admin`. See [Permissions](permissions.md).

#### Membership System
- New role: **Member** (via `/plot add`) - Can build only when owner is online
- **Trusted** players (via `/plot trust`) - Can build anytime
- Members and trusted shown separately in `/plot info`

### Improvements
- Plot info now shows alias, description, and sale status
- Restructured translation files for better organization

---

## [1.7.3] - 2026-01-29

### Fixed
- Players can no longer steal flowers and plants from other plots using F key

### Changed
- Build optimizations and internal improvements

---

## [1.7.2] - 2026-01-29

### Fixed
- Workbenches accessing linked containers from other plots (security fix)

### Changed
- Workbench container access is now filtered based on plot permissions

---

## [1.7.1] - 2026-01-28

### Fixed
- Extra wall blocks appearing at intersections after unmerging 4 plots
- Unable to build on internal intersection area after merging 4 plots

### Changed
- Build optimizations and internal improvements

---

## [1.7.0] - 2026-01-28

### Added
- New JSON-based translation system with 10 languages
- Supported languages: English, Turkish, German, Spanish, French, Portuguese, Russian, Japanese, Korean, Chinese
- Automatic migration of old language files to `languages/old/` folder

### Fixed
- Server translations randomly disappearing when plugin is active
- Command help showing raw keys instead of translated text
- `/plot home` and `/plot visit` causing errors when teleporting between worlds
- `/plot delete` now properly deletes world files even when world is not loaded
- Inconsistent message formatting across commands

### Changed
- Language files now use JSON format and are stored in `languages/` folder
- Custom translations are fully editable by server admins

---

## [1.6.0] - 2026-01-28

### Added
- `/plot admin listmerged` command to view all merged plot groups
- Teleport failed error message for all languages

### Fixed
- Various stability improvements and crash fixes
- Improved error handling throughout the plugin

---

## [1.5.0] - 2026-01-28

### Added
- Chain merge support for classic templates (L-shapes, 2x2, 3x1 configurations)
- Confirmation system for dangerous commands
- `/plot reset` and `/plot transfer` now require confirmation
- Merged plots can now be reset together (resets all connected plots)

### Fixed
- Permission issues with merged plot roads and borders
- Notification spam when walking within merged areas
- `/plot unclaim` now properly restores roads when unmerging
- Command help displays correctly translated text

---

## [1.4.3] - 2026-01-28

### Added
- Customizable language files (extracted to `data/languages/` folder)
- Server admins can now edit translations

---

## [1.4.2] - 2026-01-28

### Added
- `/plot home <number>` - teleport to specific plot when you own multiple
- `/plot visit <player> <number>` - visit specific plot of another player
- Plot numbers shown in `/plot list` output

### Fixed
- `/plot reset` command now works correctly

---

## [1.4.1] - 2026-01-28

### Fixed
- Selection tool bypass with rotated selections

---

## [1.4.0] - 2026-01-27

### Added
- Selection tool protection (prevents moving/copying to unauthorized areas)
- Bedrock layer protection for selection tool

---

## [1.3.2] - 2026-01-27

### Fixed
- Bedrock layer protection based on template settings
- BuilderTools can no longer modify protected bedrock
- Merged road edges now accessible in bridge template

---

## [1.3.1] - 2026-01-27

### Changed
- Performance improvements for BuilderTools protection

---

## [1.3.0] - 2026-01-27

### Added
- Full BuilderTools integration
- Protection for all brush types, line tool, and paste operations
- Scripted brush protection (Boulder, Building, Cave, etc.)

---

## [1.2.0] - 2026-01-27

### Added
- Corridor prefab support for merged roads
- Better prefab positioning

### Fixed
- Intersection prefabs update correctly after merge/unmerge

---

## [1.1.0] - 2026-01-27

### Added
- Plot merge system - combine adjacent plots together
- `/plot merge <direction>` command (north/south/east/west)
- `/plot unmerge` command to separate merged plots

### Fixed
- Road and wall blocks now match template configuration
- Merged road edges are properly protected

---

## [1.0.2] - 2026-01-26

### Added
- Economy support in templates (claim_cost, sell_price)

### Fixed
- Refund message no longer shows when economy is disabled

---

## [1.0.1] - 2026-01-26

### Security
- Updated dependencies for security fixes

---

## [1.0.0] - 2026-01-25

### Added
- Initial release
- Plot world creation with templates (classic, bridge)
- Plot claiming and unclaiming
- Trust and ban system
- Plot flags (pvp, explosions)
- Plot transfer between players
- SQLite and MySQL database support
- Economy integration support

---
