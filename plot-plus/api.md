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
    String memberName = event.getMemberName(); // nullable
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
    String oldValue = event.getOldValue(); // null if new flag
    String newValue = event.getNewValue(); // null if flag removed
});
```

#### PlotAliasChangeEvent

Fired when a plot alias is set or removed.

```java
getEventRegistry().registerGlobal(PlotAliasChangeEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    String oldAlias = event.getOldAlias(); // null if first time
    String newAlias = event.getNewAlias(); // null if removed
});
```

#### PlotDescriptionChangeEvent

Fired when a plot description is set or removed.

```java
getEventRegistry().registerGlobal(PlotDescriptionChangeEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    String oldDescription = event.getOldDescription(); // null if first time
    String newDescription = event.getNewDescription(); // null if removed
});
```

#### PlotHomeChangeEvent

Fired when a plot home location is set or removed.

```java
getEventRegistry().registerGlobal(PlotHomeChangeEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    boolean removed = event.isRemoved();
    Double oldX = event.getOldHomeX(); // null if no previous home
    Double oldY = event.getOldHomeY();
    Double oldZ = event.getOldHomeZ();
    Double newX = event.getNewHomeX(); // null if removed
    Double newY = event.getNewHomeY();
    Double newZ = event.getNewHomeZ();
});
```

#### PlotClearEvent

Fired before a plot is cleared (blocks reset to template).

```java
getEventRegistry().registerGlobal(PlotClearEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    boolean isMerged = event.isMerged();
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

Fired before a sale listing is cancelled.

```java
getEventRegistry().registerGlobal(PlotSaleRemovedEvent.class, event -> {
    Player player = event.getPlayer();
    Plot plot = event.getPlot();
    double price = event.getPrice();
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

## Upcoming API

The following actions are planned for the public `PlotAPI` in an upcoming release:

- `claimPlot` / `unclaimPlot`
- `transferPlot`
- `addMember` / `removeMember`
- `setFlag`
- `mergePlots` / `unmergePlots`

Stay tuned for updates.

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
