# Changelog

All notable changes to this project will be documented in this file.

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
