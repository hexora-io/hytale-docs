# Flags

Flags allow plot owners to customize their plot behavior.

## Available Flags

| Flag | Type | Default | Admin Only | Description |
|------|------|---------|------------|-------------|
| `pvp` | boolean | false | No | Allow PvP combat on the plot |
| `explosions` | boolean | false | No | Allow explosion damage on the plot |
| `server_plot` | boolean | false | Yes | Mark plot as server-owned (shows "Server" as owner) |

## Usage

### Set a Flag

```
/plot flag set <flag> <value>
```

### Remove a Flag

```
/plot flag remove <flag>
```

## Examples

### Enable PvP

```
/plot flag set pvp true
```

### Disable PvP

```
/plot flag set pvp false
```

### Remove PvP Flag (resets to default)

```
/plot flag remove pvp
```

### Enable Explosions

```
/plot flag set explosions true
```

### Mark as Server Plot (admin only)

```
/plot flag set server_plot true
```

## Flag Behavior

### PvP Flag

When `pvp` is set to `false` (default):
- Players cannot damage other players on the plot
- This includes all damage types (melee, projectiles, etc.)

When `pvp` is set to `true`:
- Players can damage each other on the plot

### Explosions Flag

When `explosions` is set to `false` (default):
- Explosions do not damage blocks on the plot
- Explosions do not damage entities on the plot

When `explosions` is set to `true`:
- Explosions behave normally

### Server Plot Flag

When `server_plot` is set to `true`:
- `/plot info` shows "Server" as the plot owner instead of the player name
- Useful for spawn plots, event areas, or other server-managed plots
- Requires `plots.admin` permission to set
