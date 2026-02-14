# Permissions

## Player Permissions

| Permission | Command | Description |
|------------|---------|-------------|
| `plots.claim` | `/plot claim` | Claim plots |
| `plots.auto` | `/plot auto` | Auto-claim next available plot |
| `plots.delete` | `/plot delete` | Delete/unclaim owned plots |
| `plots.home` | `/plot home` | Teleport to own plot |
| `plots.visit` | `/plot visit` | Visit other players' plots |
| `plots.middle` | `/plot middle` | Teleport to plot center |
| `plots.sethome` | `/plot sethome` | Set custom home location |
| `plots.trust` | `/plot trust` | Add trusted players (build anytime) |
| `plots.add` | `/plot add` | Add members (build when owner online) |
| `plots.remove` | `/plot remove` | Remove players from plot |
| `plots.deny` | `/plot deny` | Deny players from entering plot |
| `plots.kick` | `/plot kick` | Kick players from plot |
| `plots.alias` | `/plot alias` | Set or remove plot alias |
| `plots.description` | `/plot desc` | Set or remove plot description |
| `plots.flag` | `/plot flag` | Change plot flags |
| `plots.merge` | `/plot merge` | Merge adjacent plots |
| `plots.unlink` | `/plot unlink` | Unmerge plots |
| `plots.clear` | `/plot clear` | Reset plot terrain |
| `plots.info` | `/plot info` | View plot information |
| `plots.list` | `/plot list` | List owned plots |
| `plots.confirm` | `/plot confirm` | Confirm pending actions |
| `plots.sell` | `/plot sell` | List plots for sale |
| `plots.buy` | `/plot buy` | Purchase plots from marketplace |
| `plots.setowner` | `/plot setowner` | Transfer own plot to another player |

## Admin Permissions

### General

| Permission | Description |
|------------|-------------|
| `plots.admin` | Grants all admin commands and overrides ownership checks |
| `plots.admin.bypass` | Bypass all plot protection (build, break, interact anywhere) |

### Granular Admin Permissions

Grant specific admin abilities instead of full `plots.admin`:

| Permission | Description |
|------------|-------------|
| `plots.admin.command.setup` | Create plot worlds |
| `plots.admin.command.deleteworld` | Delete plot worlds |
| `plots.admin.command.reload` | Reload plugin configuration |
| `plots.admin.command.worldtp` | Teleport to plot worlds |
| `plots.admin.command.setowner` | Transfer ownership of any plot (bypass ownership check) |
| `plots.admin.command.trust` | Trust players on any plot |
| `plots.admin.command.add` | Add members to any plot |
| `plots.admin.command.remove` | Remove players from any plot |
| `plots.admin.command.deny` | Deny players on any plot |
| `plots.admin.command.kick` | Kick players from any plot |
| `plots.admin.command.clear` | Clear any plot |
| `plots.admin.command.merge` | Merge any plots |
| `plots.admin.command.unlink` | Unlink any plots |
| `plots.admin.command.flag` | Set flags on any plot |
| `plots.admin.command.sethome` | Set home on any plot |
| `plots.admin.command.desc` | Set description on any plot |
| `plots.admin.command.delete` | Delete any plot |
| `plots.admin.command.alias` | Set alias on any plot |
| `plots.admin.command.regenroads` | Regenerate roads in plot worlds |

### Bypass Permissions

| Permission | Description |
|------------|-------------|
| `plots.admin.bypass` | Bypass all plot protection |
| `plots.admin.sell.bypass` | Sell or cancel sale on any plot |
| `plots.admin.kick.bypass` | Cannot be kicked from any plot |

## Limit Permissions

Override the maximum plots per player defined in the template.

| Permission | Description |
|------------|-------------|
| `plots.limit.unlimited` | Unlimited plots |
| `plots.limit.<number>` | Specific plot limit |

### Examples

```
plots.limit.5          # Player can own 5 plots
plots.limit.10         # Player can own 10 plots
plots.limit.unlimited  # No limit
```

## Changes from v1

Several permissions were renamed in v2. See the [Migration Guide](migration.md) for the full mapping.

| Old (v1) | New (v2) |
|----------|----------|
| `plots.unmerge` | `plots.unlink` |
| `plots.unclaim` | `plots.delete` |
| `plots.ban` | `plots.deny` |
| `plots.reset` | `plots.clear` |
| `plots.claim` (for auto) | `plots.auto` |
| `plots.transfer` | `plots.setowner` |
| `plots.set.home` | `plots.sethome` |
| `plots.set.desc` | `plots.description` |
| `plots.alias.set` | `plots.alias` |
| `plots.command.sell` | `plots.sell` |
| `plots.command.buy` | `plots.buy` |
| `plots.admin.alias.set` | `plots.admin.command.alias` |
