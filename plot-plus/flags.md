# Flags

Flags allow plot owners to customize their plot behavior.

## Available Flags

| Flag | Type | Default | Description |
|------|------|---------|-------------|
| `pvp` | boolean | false | Allow PvP combat on the plot |
| `explosions` | boolean | false | Allow explosion damage on the plot |

## Usage

```
/plot flag <flag> <value>
```

## Examples

### Enable PvP

```
/plot flag pvp true
```

### Disable PvP

```
/plot flag pvp false
```

### Enable Explosions

```
/plot flag explosions true
```

### Disable Explosions

```
/plot flag explosions false
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
