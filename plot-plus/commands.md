# Commands

All commands use the `/plot` prefix.

## Player Commands

### Claiming & Navigation

| Command | Aliases | Permission | Description |
|---------|---------|------------|-------------|
| `/plot claim [--coords=x,z]` | `c` | `plots.claim` | Claim the plot you are standing on (or at coordinates) |
| `/plot auto` | `a` | `plots.auto` | Find and claim the next available plot, then teleport to it |
| `/plot delete [--coords=x,z]` | `dispose`, `del`, `unclaim` | `plots.delete` | Delete your plot (refund if economy enabled) |
| `/plot home <number>` | `h` | `plots.home` | Teleport to your plot by number (default: 1) |
| `/plot visit <target> [--number=1]` | `v`, `teleport`, `goto`, `warp` | `plots.visit` | Visit a player's plot by name or alias |
| `/plot middle [--coords=x,z]` | `center`, `centre` | `plots.middle` | Teleport to the center of a plot |
| `/plot sethome <set\|remove\|reset> [--coords=x,z]` | `sh`, `seth` | `plots.sethome` | Set or remove a custom home location |

### Members & Access

| Command | Aliases | Permission | Description |
|---------|---------|------------|-------------|
| `/plot trust <player> [--coords=x,z]` | `t` | `plots.trust` | Add a player as **trusted** (can build anytime) |
| `/plot add <player> [--coords=x,z]` | - | `plots.add` | Add a player as **member** (can build when owner is online) |
| `/plot remove <player> [--coords=x,z]` | `r`, `untrust`, `ut`, `undeny`, `ud`, `unban` | `plots.remove` | Remove a player from members or denied list |
| `/plot deny <player> [--coords=x,z]` | `d`, `ban` | `plots.deny` | Deny a player from entering your plot |
| `/plot kick <player\|*> [--coords=x,z]` | `k` | `plots.kick` | Kick a player from your plot (`*` kicks all non-trusted) |

### Plot Settings

| Command | Aliases | Permission | Description |
|---------|---------|------------|-------------|
| `/plot alias <name> [--coords=x,z]` | `setalias`, `sa`, `name`, `rename`, `setname`, `seta`, `nameplot` | `plots.alias` | Set or remove an alias for your plot (3-16 chars) |
| `/plot desc <text> [--coords=x,z]` | `setdescription`, `setdesc`, `setd`, `description` | `plots.description` | Set or remove a description (max 256 chars) |
| `/plot flag set <flag> <value> [--coords=x,z]` | - | `plots.flag` | Set a plot flag |
| `/plot flag remove <flag> [--coords=x,z]` | - | `plots.flag` | Remove a plot flag |

### Merging

| Command | Aliases | Permission | Description |
|---------|---------|------------|-------------|
| `/plot merge <direction> [--coords=x,z]` | `m` | `plots.merge` | Merge with adjacent plot (north/south/east/west) |
| `/plot unlink [--coords=x,z]` | `u`, `unmerge` | `plots.unlink` | Unmerge a merged plot |

### Marketplace

| Command | Aliases | Permission | Description |
|---------|---------|------------|-------------|
| `/plot sell <price\|cancel>` | - | `plots.sell` | List your plot for sale or cancel a listing |
| `/plot buy` | - | `plots.buy` | Buy the plot you are standing on |

### Information & Utility

| Command | Aliases | Permission | Description |
|---------|---------|------------|-------------|
| `/plot info [--coords=x,z]` | `i` | `plots.info` | View detailed plot information |
| `/plot list` | `l`, `find`, `search` | `plots.list` | List all your owned plots |
| `/plot clear [--coords=x,z]` | `reset` | `plots.clear` | Reset plot terrain to default (requires confirmation) |
| `/plot confirm` | - | `plots.confirm` | Confirm a pending action |

> **Plot Merging:**
> - **Classic template:** Full chain merge support - create L-shapes, 2x2, 3x1, or any configuration
> - **Prefab-based templates:** Limited to 2-plot merges only (no chain merging)

## Admin Commands

All admin commands are grouped under `/plot admin`:

| Command | Aliases | Permission | Description |
|---------|---------|------------|-------------|
| `/plot admin setup <world> [--template=classic]` | `create` | `plots.admin.command.setup` | Create a new plot world (default template: classic) |
| `/plot admin deleteworld <world>` | `delworld`, `removeworld` | `plots.admin.command.deleteworld` | Delete a plot world and all its data |
| `/plot admin reload` | `rl` | `plots.admin.command.reload` | Reload configuration, templates, and translations |
| `/plot admin worldtp <world>` | `wtp` | `plots.admin.command.worldtp` | Teleport to a plot world spawn |
| `/plot admin regenroads` | `regenroad`, `rr` | `plots.admin.command.regenroads` | Regenerate all roads in current plot world |
| `/plot setowner <player> [--coords=x,z]` | `owner`, `so`, `seto` | `plots.setowner` | Transfer plot ownership (requires confirmation) |

> **Note:** `/plot setowner` is a player command — plot owners can transfer their own plots. Admins with `plots.admin.command.setowner` can transfer any plot. `plots.admin` grants access to all admin commands. See [Permissions](permissions.md) for the full list.

## Examples

### Claiming a Plot

```
/plot claim
/plot auto
```

### Managing Members

```
/plot trust Steve          # Steve can build anytime
/plot add Alex             # Alex can build when you're online
/plot remove Steve         # Remove Steve from members
/plot deny Griefer         # Ban Griefer from your plot
/plot kick Griefer         # Kick Griefer off your plot
/plot kick *               # Kick all non-trusted players
```

### Navigating Plots

```
/plot home 1               # Go to your first plot
/plot home 2               # Go to your second plot
/plot visit Steve           # Visit Steve's plot
/plot visit Steve --number=2  # Visit Steve's second plot
/plot visit myshop          # Visit a plot by alias
/plot middle                # Teleport to plot center
```

### Customizing Your Plot

```
/plot alias myshop          # Set an alias
/plot desc A cozy shop      # Set a description
/plot sethome set           # Set custom home at your location
/plot sethome remove        # Remove custom home
/plot flag set pvp true     # Enable PvP
/plot flag remove pvp      # Remove PvP flag
```

### Plot Marketplace

```
/plot sell 5000             # List for sale at 5000
/plot sell cancel           # Cancel sale listing
/plot buy                   # Buy the plot you're on
```

### Merging Plots

```
/plot merge north           # Merge with the plot to the north
/plot merge east            # Merge with the plot to the east
/plot unlink                # Unmerge all merged plots
```

### Admin Commands

```
/plot admin setup creative                    # Create world with classic template
/plot admin setup creative --template=bridge  # Create world with bridge template
/plot admin deleteworld creative              # Delete a plot world
/plot admin worldtp creative                  # Teleport to plot world
/plot admin reload                            # Reload config and translations
/plot admin regenroads                        # Regenerate all roads
/plot setowner Steve                          # Transfer plot ownership
```
