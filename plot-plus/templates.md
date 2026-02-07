# Templates

Templates define the settings and appearance of plot worlds.

## Built-in Templates

| Template | Description |
|----------|-------------|
| `classic` | Traditional flat plots (64x64, 7-block roads) |
| `bridge` | Larger plots with bridge infrastructure (50x50, 12-block roads) |

## Template Location

Templates are stored in the plugin data folder:

```
mods/Hexora_PlotPlus/templates/
├── classic/
│   └── template.yml
└── bridge/
    └── template.yml
```

## Template Structure

```yaml
plot:
  size: 64
  height: 64
  floor: Soil_Grass
  filling: Soil_Dirt
  fill_depth: 0
  bedrock: true

wall:
  block: Rock_Stone_Brick_Smooth_Half

road:
  width: 7
  block: Rock_Stone
  filling: Soil_Dirt

prefab:
  use_prefabs: false

world:
  environment: Env_Zone1

claiming:
  max_plots_per_player: 1

economy:
  enabled: false
  claim_cost: 0
  sell_price: 0

flags:
  pvp: false
  explosions: false
```

## Settings

### plot

| Setting | Description |
|---------|-------------|
| `size` | Plot size in blocks (creates size x size area) |
| `height` | Y-coordinate of the plot floor |
| `floor` | Block type for the floor surface |
| `filling` | Block type for sub-floor filling |
| `fill_depth` | Depth of filling below floor |
| `bedrock` | Add bedrock layer at bottom |

### wall

| Setting | Description |
|---------|-------------|
| `block` | Block type for plot border walls |

### road

| Setting | Description |
|---------|-------------|
| `width` | Road width between plots |
| `block` | Block type for road surface |
| `filling` | Block type for road sub-surface |

### prefab

| Setting | Description |
|---------|-------------|
| `use_prefabs` | Enable prefab-based generation |
| `intersection` | Path to intersection prefab |
| `sideroad` | Path to sideroad prefab |

> **Note:** Prefab-based templates only support 2-plot merges. Chain merging (L-shapes, 2x2 grids, etc.) is only available in classic templates (`use_prefabs: false`).

### world

| Setting | Description |
|---------|-------------|
| `environment` | World environment/biome |

### claiming

| Setting | Description |
|---------|-------------|
| `max_plots_per_player` | Maximum plots per player in this world |

### economy

| Setting | Description |
|---------|-------------|
| `enabled` | Enable economy integration for this world |
| `claim_cost` | Cost to claim a plot |
| `sell_price` | Refund amount when unclaiming a plot |

### flags

| Setting | Description |
|---------|-------------|
| `pvp` | Default PvP flag value |
| `explosions` | Default explosions flag value |

## Creating a Template

1. Create a new folder in `templates/`
2. Create `template.yml` with your settings
3. Use `/plot setup <world_name> --template=<template_name>`

## Example: Large Plots Template

Create `templates/large/template.yml`:

```yaml
plot:
  size: 128
  height: 64
  floor: Soil_Grass
  filling: Soil_Dirt
  fill_depth: 0
  bedrock: true

wall:
  block: Rock_Stone_Brick_Smooth_Half

road:
  width: 8
  block: Rock_Stone
  filling: Soil_Dirt

world:
  environment: Env_Zone1

claiming:
  max_plots_per_player: 1

flags:
  pvp: false
  explosions: false
```

Usage: `/plot setup bigplots --template=large`
