# API

PlotPlus provides an API for developers to integrate with plots.

## Events

All events can be cancelled using `setCancelled(true)`.

### Registering Event Listeners

Use `EventRegistry.register()` or `EventRegistry.registerGlobal()`:

```java
public class MyMod extends JavaPlugin {

    @Override
    public void onEnable() {
        getEventRegistry().registerGlobal(PlotClaimEvent.class, this::onPlotClaim);
        getEventRegistry().registerGlobal(PlotEnterEvent.class, this::onPlotEnter);
    }

    private void onPlotClaim(PlotClaimEvent event) {
        Player player = event.getPlayer();
        Plot plot = event.getPlot();

        // Cancel the claim
        event.setCancelled(true);
    }

    private void onPlotEnter(PlotEnterEvent event) {
        Player player = event.getPlayer();
        Plot toPlot = event.getToPlot();
    }
}
```

### Event Priority

```java
getEventRegistry().registerGlobal(EventPriority.EARLY, PlotClaimEvent.class, this::onPlotClaim);
```

Priorities: `FIRST`, `EARLY`, `NORMAL`, `LATE`, `LAST`

### Available Events

#### PlotClaimEvent

Fired when a player claims a plot.

```java
getEventRegistry().registerGlobal(PlotClaimEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
});
```

#### PlotUnclaimEvent

Fired when a player unclaims a plot.

```java
getEventRegistry().registerGlobal(PlotUnclaimEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
});
```

#### PlotTransferEvent

Fired when plot ownership is transferred.

```java
getEventRegistry().registerGlobal(PlotTransferEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    UUID previousOwnerUuid = event.getPreviousOwnerUuid();
    String previousOwnerName = event.getPreviousOwnerName();
    UUID newOwnerUuid = event.getNewOwnerUuid();
    String newOwnerName = event.getNewOwnerName();
});
```

#### PlotMemberAddEvent

Fired when a member is added (trusted or banned).

```java
getEventRegistry().registerGlobal(PlotMemberAddEvent.class, event -> {
    Player executor = event.getPlayer();
    Plot plot = event.getPlot();
    UUID memberUuid = event.getMemberUuid();
    String memberName = event.getMemberName();
    PlotRole role = event.getRole(); // TRUSTED or DENIED
    boolean isBan = event.isBan();
});
```

#### PlotMemberRemoveEvent

Fired when a member is removed.

```java
getEventRegistry().registerGlobal(PlotMemberRemoveEvent.class, event -> {
    Player executor = event.getPlayer();
    Plot plot = event.getPlot();
    UUID memberUuid = event.getMemberUuid();
    PlotRole previousRole = event.getPreviousRole();
    boolean wasUnban = event.wasUnban();
});
```

#### PlotFlagChangeEvent

Fired when a plot flag is changed.

```java
getEventRegistry().registerGlobal(PlotFlagChangeEvent.class, event -> {
    Player executor = event.getPlayer();
    Plot plot = event.getPlot();
    String flagName = event.getFlagName();
    String oldValue = event.getOldValue();
    String newValue = event.getNewValue();
});
```

#### PlotEnterEvent

Fired when a player enters a plot.

```java
getEventRegistry().registerGlobal(PlotEnterEvent.class, event -> {
    Player player = event.getPlayer();
    Plot toPlot = event.getToPlot();
    Plot fromPlot = event.getFromPlot(); // nullable
});
```

#### PlotLeaveEvent

Fired when a player leaves a plot.

```java
getEventRegistry().registerGlobal(PlotLeaveEvent.class, event -> {
    Player player = event.getPlayer();
    Plot fromPlot = event.getFromPlot();
    Plot toPlot = event.getToPlot(); // nullable
});
```

#### PlotBlockBreakEvent

Fired before a block is broken in a plot.

```java
getEventRegistry().registerGlobal(PlotBlockBreakEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    Vector3i position = event.getBlockPosition();
    boolean allowed = event.isAllowed();
    event.setAllowed(false); // Prevent break
});
```

#### PlotBlockPlaceEvent

Fired before a block is placed in a plot.

```java
getEventRegistry().registerGlobal(PlotBlockPlaceEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    Vector3i position = event.getBlockPosition();
    boolean allowed = event.isAllowed();
    event.setAllowed(false); // Prevent place
});
```

#### PlotInteractEvent

Fired before interaction in a plot.

```java
getEventRegistry().registerGlobal(PlotInteractEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    Vector3i position = event.getBlockPosition();
    boolean allowed = event.isAllowed();
    event.setAllowed(false); // Prevent interaction
});
```

#### PlotWorldCreateEvent

Fired when a plot world is created.

```java
getEventRegistry().registerGlobal(PlotWorldCreateEvent.class, event -> {
    PlotWorld plotWorld = event.getPlotWorld();
});
```

#### PlotWorldDeleteEvent

Fired when a plot world is deleted.

```java
getEventRegistry().registerGlobal(PlotWorldDeleteEvent.class, event -> {
    PlotWorld plotWorld = event.getPlotWorld();
});
```

#### PlotMergeEvent

Fired when plots are merged.

```java
getEventRegistry().registerGlobal(PlotMergeEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    Plot targetPlot = event.getTargetPlot();
    MergeDirection direction = event.getDirection();
});
```

#### PlotUnmergeEvent

Fired when plots are unmerged.

```java
getEventRegistry().registerGlobal(PlotUnmergeEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    List<Plot> mergedPlots = event.getMergedPlots();
});
```

## PlotAPI

High-level public API:

```java
// Get plot at ID
Optional<Plot> plot = PlotAPI.getPlot(plotId);

// Get plot at location
Optional<Plot> plot = PlotAPI.getPlotAt(worldName, x, z);

// Get player's plots
List<Plot> plots = PlotAPI.getPlayerPlots(playerUuid);

// Check if world is a plot world
boolean isPlotWorld = PlotAPI.isPlotWorld(worldName);

// Get plot world
Optional<PlotWorld> world = PlotAPI.getPlotWorld(worldName);

// Check build permission
boolean canBuild = PlotAPI.canBuild(player, worldName, x, y, z);
```

## Services

Access PlotPlus services through the ServiceRegistry.

### PlotService

```java
PlotService plotService = ServiceRegistry.get(PlotService.class);

// Get plot at ID
Optional<Plot> plot = plotService.getPlot(plotId);

// Get player's plots
List<Plot> plots = plotService.getPlayerPlots(playerUuid);

// Get plot count
int count = plotService.getPlayerPlotCount(playerUuid, worldName);

// Get player plot limit
int limit = plotService.getPlayerPlotLimit(player, plotWorld);

// Find next available plot
PlotId nextPlot = plotService.findNextAvailablePlot(plotWorld);

// Claim a plot
ClaimResult result = plotService.claimPlot(player, plotId);

// Unclaim a plot
UnclaimResult result = plotService.unclaimPlot(player, plotId);

// Transfer ownership
TransferResult result = plotService.transferPlot(executor, plot, targetPlayer);

// Add member
boolean success = plotService.addMember(executor, plot, memberUuid, memberName, PlotRole.TRUSTED);

// Remove member
boolean success = plotService.removeMember(executor, plot, memberUuid);

// Set flag
boolean success = plotService.setFlag(executor, plot, flagName, flagValue);

// Merge plots
MergeResult result = plotService.mergePlots(player, plotId, MergeDirection.NORTH);

// Unmerge plots
UnmergeResult result = plotService.unmergePlots(player, plotId);

// Get merged plots
List<Plot> merged = plotService.getMergedPlots(mergeId);
```

### Result Enums

```java
// ClaimResult
ClaimResult.SUCCESS
ClaimResult.ALREADY_CLAIMED
ClaimResult.MAX_PLOTS_REACHED
ClaimResult.WORLD_NOT_SETUP
ClaimResult.INSUFFICIENT_FUNDS

// UnclaimResult
UnclaimResult.SUCCESS
UnclaimResult.NOT_CLAIMED
UnclaimResult.NOT_OWNER
UnclaimResult.CANCELLED

// TransferResult
TransferResult.SUCCESS
TransferResult.NOT_CLAIMED
TransferResult.NOT_OWNER
TransferResult.ALREADY_OWNER
TransferResult.TARGET_MAX_PLOTS
TransferResult.CANCELLED

// MergeResult
MergeResult.SUCCESS
MergeResult.NOT_CLAIMED
MergeResult.NOT_OWNER
MergeResult.TARGET_NOT_CLAIMED
MergeResult.TARGET_NOT_OWNER
MergeResult.NOT_ADJACENT
MergeResult.ALREADY_MERGED
MergeResult.WORLD_NOT_SETUP
MergeResult.CANCELLED

// UnmergeResult
UnmergeResult.SUCCESS
UnmergeResult.NOT_MERGED
UnmergeResult.NOT_OWNER
UnmergeResult.CANCELLED
```

### PlotWorldService

```java
PlotWorldService worldService = ServiceRegistry.get(PlotWorldService.class);

// Check if world is a plot world
boolean isPlotWorld = worldService.isPlotWorld(worldName);

// Get plot world
Optional<PlotWorld> plotWorld = worldService.getPlotWorld(worldName);

// Get all plot worlds
List<PlotWorld> worlds = worldService.getAllPlotWorlds();

// Create plot world
PlotWorld created = worldService.createPlotWorld(plotWorld);

// Delete plot world
boolean deleted = worldService.deletePlotWorld(worldName);

// Reload from database
worldService.reload();
```

### PlotCache

```java
PlotCache cache = ServiceRegistry.get(PlotCache.class);

// Get plot at ID
Optional<Plot> plot = cache.getPlot(PlotId.of(worldName, plotX, plotZ));

// Cache a plot
cache.cachePlot(plot);

// Invalidate cache
cache.invalidate(plotId);
cache.invalidateAll();

// Reload plot from database
Plot reloaded = cache.reloadPlot(plotId);
```

### ProtectionManager

```java
ProtectionManager protection = ServiceRegistry.get(ProtectionManager.class);

// Get plot at location
Optional<Plot> plot = protection.getPlotAt(worldName, x, z);
Optional<Plot> plot = protection.getPlotAt(worldName, new Vector3i(x, y, z));

// Check if player can build
boolean canBuild = protection.canBuild(player, worldName, new Vector3i(x, y, z));
boolean canBuild = protection.canBuild(playerUuid, worldName, position, hasBypass);

// Check if player can break
boolean canBreak = protection.canBreak(player, worldName, new Vector3i(x, y, z));

// Check if player can interact
boolean canInteract = protection.canInteract(player, worldName, new Vector3i(x, y, z));

// Check if world is a plot world
boolean isPlotWorld = protection.isPlotWorld(worldName);
```

## Plot Roles

```java
public enum PlotRole {
    OWNER(3),    // Plot owner
    TRUSTED(2),  // Trusted player (can build)
    VISITOR(1),  // Default visitor
    DENIED(0);   // Banned player

    int getLevel();                      // Returns the permission level
    boolean hasAtLeast(PlotRole other);  // Check if this role has at least the given role's level
}
```

## Economy Integration

PlotPlus supports custom economy providers.

```java
public class MyEconomyProvider implements EconomyProvider {

    @Override
    public String getName() {
        return "MyEconomy";
    }

    @Override
    public boolean hasBalance(UUID player, double amount) {
        // Check if player has enough money
    }

    @Override
    public boolean withdraw(UUID player, double amount) {
        // Withdraw money from player
    }

    @Override
    public boolean deposit(UUID player, double amount) {
        // Deposit money to player
    }

    @Override
    public double getBalance(UUID player) {
        // Get player balance
    }
}

// Register provider
EconomyRegistry.register(new MyEconomyProvider());

// Unregister provider
EconomyRegistry.unregister();

// Get provider
Optional<EconomyProvider> provider = EconomyRegistry.getProvider();

// Check if economy is available
boolean hasEconomy = EconomyRegistry.hasEconomy();
```
