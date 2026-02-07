# Permissions

## Player Permissions

| Permission | Description |
|------------|-------------|
| `plots.claim` | Claim plots (required for `/plot claim` and `/plot auto`) |
| `plots.unclaim` | Unclaim plots |
| `plots.home` | Teleport to own plot |
| `plots.visit` | Visit other players' plots |
| `plots.trust` | Manage trusted players (trust/untrust) |
| `plots.ban` | Ban players from plot |
| `plots.transfer` | Transfer plot ownership |
| `plots.flag` | Change plot flags |
| `plots.info` | View plot information |
| `plots.list` | List owned plots |
| `plots.reset` | Reset plot to default state |
| `plots.merge` | Merge adjacent plots |
| `plots.unmerge` | Unmerge plots |

## Admin Permissions

| Permission | Description |
|------------|-------------|
| `plots.admin` | All admin commands (setup, delete, reload, tp) |
| `plots.admin.bypass` | Bypass plot protection (build anywhere) |

## Limit Permissions

Override the maximum plots per player setting.

| Permission | Description |
|------------|-------------|
| `plots.limit.unlimited` | Unlimited plots |
| `plots.limit.<number>` | Specific plot limit |

### Examples

```
plots.limit.5      # Player can own 5 plots
plots.limit.10     # Player can own 10 plots
plots.limit.unlimited  # No limit
```
