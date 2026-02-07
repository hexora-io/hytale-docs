# Commands

All commands use the `/plot` prefix.

## Player Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/plot claim` | `plots.claim` | Claim the plot you are standing on |
| `/plot auto` | `plots.claim` | Find and claim the next available plot |
| `/plot unclaim` | `plots.unclaim` | Unclaim your plot |
| `/plot home [--number=N]` | `plots.home` | Teleport to your plot (use --number for multiple plots) |
| `/plot visit <player> [--number=N]` | `plots.visit` | Visit another player's plot (use --number for multiple plots) |
| `/plot trust <player>` | `plots.trust` | Add a trusted player to your plot |
| `/plot untrust <player>` | `plots.trust` | Remove a trusted player from your plot |
| `/plot ban <player>` | `plots.ban` | Ban a player from your plot |
| `/plot transfer <player>` | `plots.transfer` | Transfer plot ownership to another player |
| `/plot flag <flag> <value>` | `plots.flag` | Set a plot flag |
| `/plot info` | `plots.info` | View plot information |
| `/plot list` | `plots.list` | List your plots |
| `/plot reset` | `plots.reset` | Reset your plot to default state |
| `/plot merge <direction>` | `plots.merge` | Merge with adjacent plot (north/south/east/west) * |
| `/plot unmerge` | `plots.unmerge` | Unmerge all merged plots * |
| `/plot confirm` | - | Confirm a pending action (reset, transfer) |

> \* **Plot Merging:**
> - **Classic template:** Full chain merge support - create L-shapes, 2x2, 3x1, or any configuration
> - **Prefab-based templates:** Limited to 2-plot merges only (no chain merging)

## Admin Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/plot setup <world_name>` | `plots.admin` | Create a new plot world (default template: classic) |
| `/plot setup <world_name> --template=<name>` | `plots.admin` | Create a plot world with specific template |
| `/plot delete <world_name>` | `plots.admin` | Delete a plot world |
| `/plot reload` | `plots.admin` | Reload the plugin configuration and translations |
| `/plot tp <world_name>` | `plots.admin` | Teleport to a plot world |
| `/plot admin listmerged` | `plots.admin` | List all merged plot groups |

## Examples

### Claiming a Plot

```
/plot claim
```

### Auto Claim

```
/plot auto
```

### Trusting a Player

```
/plot trust Steve
```

### Removing Trust

```
/plot untrust Steve
```

### Banning a Player

```
/plot ban Griefer
```

### Teleporting to Multiple Plots

If you own multiple plots, use `--number` to specify which one:

```
/plot home --number=2
```

### Visiting a Specific Plot

Visit a player's second plot:

```
/plot visit Steve --number=2
```

### Setting a Flag

```
/plot flag pvp true
```

### Merging Plots

Merge with the plot to the north:
```
/plot merge north
```

Merge with the plot to the east:
```
/plot merge east
```

### Unmerging Plots

```
/plot unmerge
```

### Creating a Plot World

Default template (classic):
```
/plot setup creative
```

With specific template:
```
/plot setup creative --template=bridge
```

### Teleporting to a Plot World

```
/plot tp creative
```

### Deleting a Plot World

```
/plot delete creative
```
