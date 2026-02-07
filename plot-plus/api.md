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

Fired when a player unclaims/deletes a plot.

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

Fired when a member is added to a plot (trusted, member, or denied).

```java
getEventRegistry().registerGlobal(PlotMemberAddEvent.class, event -> {
    Player executor = event.getPlayer();
    Plot plot = event.getPlot();
    UUID memberUuid = event.getMemberUuid();
    String memberName = event.getMemberName();
    PlotRole role = event.getRole(); // TRUSTED, MEMBER, or DENIED
    boolean isBan = event.isBan();
});
```

#### PlotMemberRemoveEvent

Fired when a member is removed from a plot.

```java
getEventRegistry().registerGlobal(PlotMemberRemoveEvent.class, event -> {
    Player executor = event.getPlayer();
    Plot plot = event.getPlot();
    UUID memberUuid = event.getMemberUuid();
    PlotRole previousRole = event.getPreviousRole();
    boolean wasUnban = event.wasUnban();
});
```

#### PlotKickEvent

Fired when a player is kicked from a plot.

```java
getEventRegistry().registerGlobal(PlotKickEvent.class, event -> {
    Player kicker = event.getKicker();
    Plot plot = event.getPlot();
    PlayerRef target = event.getTargetRef();
    String reason = event.getReason();
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

#### PlotListedForSaleEvent

Fired when a plot is listed for sale on the marketplace.

```java
getEventRegistry().registerGlobal(PlotListedForSaleEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    double price = event.getPrice();
});
```

#### PlotPurchaseEvent

Fired when a plot is purchased from the marketplace.

```java
getEventRegistry().registerGlobal(PlotPurchaseEvent.class, event -> {
    Player buyer = event.getBuyer();
    Plot plot = event.getPlot();
    UUID sellerUuid = event.getSellerUuid();
    String sellerName = event.getSellerName();
    double price = event.getPrice();
});
```

#### PlotSaleRemovedEvent

Fired when a sale listing is cancelled.

```java
getEventRegistry().registerGlobal(PlotSaleRemovedEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
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
OperationResult<ClaimResult> result = plotService.claimPlot(player, plotId);

// Unclaim a plot
OperationResult<UnclaimResult> result = plotService.unclaimPlot(player, plotId);

// Transfer ownership
OperationResult<TransferResult> result = plotService.transferPlot(executor, plot, targetPlayer);

// Add member
boolean success = plotService.addMember(executor, plot, memberUuid, memberName, PlotRole.TRUSTED);

// Remove member
boolean success = plotService.removeMember(executor, plot, memberUuid);

// Set flag
boolean success = plotService.setFlag(executor, plot, flagName, flagValue);

// Merge plots
OperationResult<MergeResult> result = plotService.mergePlots(player, plotId, MergeDirection.NORTH);

// Unmerge plots
OperationResult<UnmergeResult> result = plotService.unmergePlots(player, plotId);

// Get merged plots
List<Plot> merged = plotService.getMergedPlots(mergeId);
```

### OperationResult

All service operations return `OperationResult<T>`, a generic wrapper that pairs a result status with an optional i18n message:

```java
public record OperationResult<T>(
    @Nonnull T status,
    @Nullable String messageKey,
    @Nonnull Map<String, String> placeholders
) {
    // Check if the operation succeeded
    public boolean isSuccess();

    // Send the translated message to a player
    public void sendMessageTo(@Nonnull PlayerRef playerRef);

    // Factory methods
    public static <T> OperationResult<T> success(@Nonnull T status);
    public static <T> OperationResult<T> success(@Nonnull T status, @Nonnull String messageKey);
    public static <T> OperationResult<T> failure(@Nonnull T status, @Nonnull String messageKey);
    public static <T> OperationResult<T> failure(@Nonnull T status, @Nonnull String messageKey,
                                                  @Nonnull Map<String, String> placeholders);

    // Add placeholders
    public OperationResult<T> withPlaceholder(@Nonnull String key, @Nonnull String value);
    public OperationResult<T> withPlaceholders(@Nonnull Map<String, String> additional);
}
```

### Result Enums

#### ClaimResult

| Value | Message Key | Description |
|-------|-------------|-------------|
| `SUCCESS` | `success.claim.claimed` | Plot claimed |
| `ALREADY_CLAIMED` | `error.plot.already_claimed` | Plot already owned |
| `MAX_PLOTS_REACHED` | `error.plot.max_plots_reached` | Player at plot limit |
| `WORLD_NOT_SETUP` | `error.world.not_setup` | World not configured |
| `INSUFFICIENT_FUNDS` | `error.plot.insufficient_funds` | Not enough currency |

#### UnclaimResult

| Value | Message Key | Description |
|-------|-------------|-------------|
| `SUCCESS` | `success.delete.unclaimed` | Plot unclaimed |
| `NOT_CLAIMED` | `error.plot.not_claimed` | Plot not claimed |
| `NOT_OWNER` | `error.plot.not_owner` | Player not owner |
| `CANCELLED` | - | Operation cancelled |

#### TransferResult

| Value | Message Key | Description |
|-------|-------------|-------------|
| `SUCCESS` | `success.transfer.transferred` | Transfer complete |
| `NOT_CLAIMED` | `error.plot.not_claimed` | Plot not claimed |
| `NOT_OWNER` | `error.plot.not_owner` | Player not owner |
| `ALREADY_OWNER` | `error.transfer.already_owner` | Target already owns plot |
| `TARGET_MAX_PLOTS` | `error.transfer.target_max_plots` | Target at plot limit |
| `CANCELLED` | - | Operation cancelled |

#### MergeResult

| Value | Message Key | Description |
|-------|-------------|-------------|
| `SUCCESS` | `success.merge.merged` | Merge complete |
| `NOT_CLAIMED` | `error.plot.not_claimed` | Source not claimed |
| `NOT_OWNER` | `error.plot.not_owner` | Not source owner |
| `TARGET_NOT_CLAIMED` | `error.merge.target_not_claimed` | Target not claimed |
| `TARGET_NOT_OWNER` | `error.merge.target_not_owned` | Not target owner |
| `NOT_ADJACENT` | `error.merge.not_adjacent` | Plots not adjacent |
| `ALREADY_MERGED` | `error.merge.already_merged` | Already merged |
| `CHAIN_MERGE_NOT_ALLOWED` | `error.merge.chain_not_allowed` | Chain merge not supported |
| `WORLD_NOT_SETUP` | `error.world.not_setup` | World not configured |
| `CANCELLED` | - | Operation cancelled |

#### UnmergeResult

| Value | Message Key | Description |
|-------|-------------|-------------|
| `SUCCESS` | `success.merge.unmerged` | Unmerge complete |
| `NOT_MERGED` | `error.merge.not_merged` | Plot not merged |
| `NOT_OWNER` | `error.plot.not_owner` | Not owner |
| `CANCELLED` | - | Operation cancelled |

#### BuyResult

| Value | Message Key | Description |
|-------|-------------|-------------|
| `SUCCESS` | `success.buy.purchased` | Purchase complete |
| `NOT_CLAIMED` | `error.plot.not_claimed` | Plot not claimed |
| `NOT_FOR_SALE` | `error.buy.not_for_sale` | Not listed for sale |
| `OWN_PLOT` | `error.buy.own_plot` | Cannot buy own plot |
| `INSUFFICIENT_FUNDS` | `error.buy.insufficient_funds` | Not enough currency |
| `ECONOMY_DISABLED` | `error.economy.disabled` | Economy not enabled |
| `MAX_PLOTS_REACHED` | `error.plot.max_plots_reached` | Buyer at plot limit |
| `TRANSACTION_FAILED` | `error.buy.transaction_failed` | Transaction failed |
| `EVENT_CANCELLED` | `error.common.cancelled` | Event cancelled |

#### SellResult

| Value | Message Key | Description |
|-------|-------------|-------------|
| `SUCCESS` | `success.sell.listed` | Listed for sale |
| `CANCELLED` | `success.sell.cancelled` | Listing cancelled |
| `NOT_CLAIMED` | `error.plot.not_claimed` | Plot not claimed |
| `NOT_OWNER` | `error.plot.not_owner` | Not owner |
| `ALREADY_FOR_SALE` | `error.sell.already_for_sale` | Already listed |
| `NOT_FOR_SALE` | `error.sell.not_for_sale` | Not listed |
| `INVALID_PRICE` | `error.sell.invalid_price` | Invalid price |
| `ECONOMY_DISABLED` | `error.economy.disabled` | Economy not enabled |

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
    OWNER(4),    // Plot owner
    TRUSTED(3),  // Trusted player (can build anytime)
    MEMBER(2),   // Member (can build when owner is online)
    GUEST(1),    // Default visitor
    DENIED(0);   // Denied player

    int getLevel();                      // Returns the permission level
    boolean hasAtLeast(PlotRole other);  // Check if this role has at least the given role's level
}
```

### Build Permission by Role

| Role | Can Build | Condition |
|------|-----------|-----------|
| OWNER | Yes | Always |
| TRUSTED | Yes | Always |
| MEMBER | Yes | Only when owner is online |
| GUEST | No | - |
| DENIED | No | Cannot enter plot |

## Economy Integration

PlotPlus supports custom economy providers for plot claiming costs, refunds, and the marketplace.

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
