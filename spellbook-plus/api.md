# API

Spellbook Plus v2 provides a developer API for integrating with the spell system. The API uses record-based models and service interfaces accessed via `SpellbookPlugin.getInstance()`.

## Plugin Instance

Access the main plugin and all services:

```java
SpellbookPlugin plugin = SpellbookPlugin.getInstance();

// Core services
CooldownService cooldowns = plugin.getCooldownService();
SpellService spells = plugin.getSpellService();
NodeRegistry nodes = plugin.getNodeRegistry();
SpellbookEventBus eventBus = plugin.getEventBus();
DamageService damage = plugin.getDamageService();

// Enchantment & Passive services
EnchantmentRegistry enchantments = plugin.getEnchantmentRegistry();
EnchantmentService enchantmentService = plugin.getEnchantmentService();
PassiveRegistry passives = plugin.getPassiveRegistry();
PassiveService passiveService = plugin.getPassiveService();
```

## SpellService

Manage spell definitions and player spell knowledge.

```java
public interface SpellService {
    Optional<SpellDefinition> getSpell(String spellId);
    List<SpellDefinition> getAllSpells();
    List<SpellDefinition> getSpellsByCategory(SpellCategory category);
    List<SpellDefinition> getPlayerSpells(UUID playerId);
    boolean hasSpell(UUID playerId, String spellId);
    void grantSpell(UUID playerId, String spellId);
    void revokeSpell(UUID playerId, String spellId);
    void registerSpell(SpellDefinition spell);
    void unregisterSpell(String spellId);
    void reloadSpells();
    int getSpellCount();
}
```

## CooldownService

Manage spell cooldowns per player.

```java
public interface CooldownService {
    boolean isOnCooldown(UUID playerId, String spellId);
    long getRemainingCooldown(UUID playerId, String spellId);
    float getCooldownPercent(UUID playerId, String spellId);
    void setCooldown(UUID playerId, String spellId, long durationMs);
    void reduceCooldown(UUID playerId, String spellId, long reductionMs);
    void clearCooldown(UUID playerId, String spellId);
    void clearAllCooldowns(UUID playerId);
    Map<String, Long> getAllCooldowns(UUID playerId);
    void tick(long deltaMs);
    void removePlayer(UUID playerId);
}
```

## DamageService

Calculate spell damage and track hits.

```java
public interface DamageService {
    float calculateDamage(ProjectileDataComponent projectileData, float nativeDamage, UUID targetId);
    boolean isDuplicateHit(ProjectileDataComponent projectileData, UUID targetId);
    void markHit(ProjectileDataComponent projectileData, UUID targetId);
}
```

## NodeRegistry

Register and look up node handlers. Used by the spell execution engine.

```java
public final class NodeRegistry {
    void register(String nodeType, NodeHandler handler);
    Optional<NodeHandler> get(String nodeType);
    boolean has(String nodeType);
    boolean isAllowed(String nodeType);
    void unregister(String nodeType);
    int size();
    Set<String> getRegisteredTypes();
}
```

## SpellbookEventBus

Publish/subscribe event system for spell-related events.

```java
public final class SpellbookEventBus {
    <T extends SpellbookEvent> void subscribe(Class<T> eventType, Consumer<T> listener);
    <T extends SpellbookEvent> void unsubscribe(Class<T> eventType, Consumer<T> listener);
    <T extends SpellbookEvent> void publish(T event);
    void clear();
}
```

## Data Models

### SpellDefinition (Record)

```java
public record SpellDefinition(
    String id,
    String name,
    SpellMetadata metadata,
    SpellGraph graph,
    Map<String, SpellTranslation> translations,
    Optional<String> checksum
) {
    int getBaseCooldown();
    int getBaseManaCost();
    SpellCategory getCategory();
    int getInstabilityLevel();
    int getNodeCount();
    String getLocalizedName(String locale);
    String getLocalizedDescription(String locale);
    boolean verifyChecksum();
}
```

### SpellMetadata (Record)

```java
public record SpellMetadata(
    int baseCooldown,
    int baseManaCost,
    SpellCategory category,
    int instabilityLevel,
    Optional<String> description,
    Optional<String> icon
)
```

### SpellGraph (Record)

```java
public record SpellGraph(List<SpellNode> nodes) {
    Optional<SpellNode> getNode(String id);
    List<SpellNode> getNodesByType(String type);
    Optional<SpellNode> getEntryNode();
    List<SpellNode> getConnectedNodes(SpellNode node);
    int getTotalManaCost();
    int getTotalInstability();
}
```

### SpellNode (Record)

```java
public record SpellNode(
    String id,
    String type,
    Map<String, Object> parameters,
    List<String> connections
) {
    int getInt(String key, int defaultValue);
    float getFloat(String key, float defaultValue);
    String getString(String key, String defaultValue);
    boolean getBoolean(String key, boolean defaultValue);
}
```

### EnchantmentDefinition (Record)

```java
public record EnchantmentDefinition(
    String id,
    String name,
    TriggerType trigger,
    int maxStacks,
    float cooldown,
    EnchantmentTier tier,
    int rollWeight,
    Optional<String> description,
    SpellGraph graph
)
```

### PassiveDefinition (Record)

```java
public record PassiveDefinition(
    String id,
    String name,
    TriggerType trigger,
    float interval,
    float cooldown,
    PassiveTier tier,
    int rollWeight,
    Optional<String> condition,
    Optional<String> description,
    SpellGraph graph
) {
    boolean isIntervalBased();
}
```

## Creating Custom Node Handlers

Implement the `NodeHandler` functional interface:

```java
@FunctionalInterface
public interface NodeHandler {
    NodeResult handle(NodeContext context);
}
```

Register in `NodeRegistry`:

```java
SpellbookPlugin plugin = SpellbookPlugin.getInstance();
NodeRegistry registry = plugin.getNodeRegistry();

registry.register("my_custom_node", context -> {
    int value = context.getNode().getInt("value", 10);

    // Your custom logic here

    return NodeResult.success();
});
```

## Enums

### SpellCategory

```
PROJECTILE, DAMAGE, HEAL, UTILITY, DEFENSE, BUFF, DEBUFF
```

### TriggerType

```
ON_CAST, ON_HIT, ON_KILL, ON_DAMAGE_TAKEN, ON_HEAL, ON_EXPIRE, ON_INTERVAL, ON_ENTER_COMBAT, ON_EXIT_COMBAT
```

### EnchantmentTier

```
COMMON, RARE, EPIC
```

### PassiveTier

```
COMMON, RARE, EPIC
```

### NodeType

```
ON_CAST, ON_HIT, ON_KILL, ON_DAMAGE_TAKEN, ON_HEAL, ON_EXPIRE, ON_INTERVAL, ON_ENTER_COMBAT, ON_EXIT_COMBAT,
DAMAGE, HEAL, EFFECT, STATUS_EFFECT, AOE, GLOW, PROJECTILE, TELEPORT, SHIELD, PUSH, PARTICLE, MANA_RESTORE, CONDITIONAL
```

## ECS Components

The mod uses Hytale's ECS system with these components:

| Component | Purpose |
|-----------|---------|
| `SpellCasterComponent` | Player spell state and hotbar |
| `ProjectileDataComponent` | Projectile metadata (damage, caster, spell ID) |
| `ShieldComponent` | Active damage shield tracking |
| `PlayerPassiveComponent` | Active passive abilities |
| `StaffEnchantmentComponent` | Staff enchantment slots |
| `PlayerEnchantingComponent` | Enchanting XP and progress |

## Example: Check Cooldown and Cast

```java
SpellbookPlugin plugin = SpellbookPlugin.getInstance();
CooldownService cooldowns = plugin.getCooldownService();
SpellService spells = plugin.getSpellService();

UUID playerId = player.getUUID();
String spellId = "fireball";

if (cooldowns.isOnCooldown(playerId, spellId)) {
    long remaining = cooldowns.getRemainingCooldown(playerId, spellId);
    // Handle cooldown...
    return;
}

Optional<SpellDefinition> spell = spells.getSpell(spellId);
if (spell.isEmpty()) {
    // Spell not found...
    return;
}

// Apply cooldown
cooldowns.setCooldown(playerId, spellId, spell.get().getBaseCooldown() * 1000L);
```

## Event Types

| Event | Trigger | Key Fields |
|-------|---------|------------|
| `SpellCastEvent` | Spell cast | `playerId`, `spellId` |
| `ProjectileHitEvent` | Spell projectile hits target | `casterId`, `hitEntityId`, `damage`, `spellId` |
| `EntityKillEvent` | Entity killed by spell | `casterId`, `killedEntityId`, `spellId` |
| `DamageTakenEvent` | Entity takes damage | `casterId`, `sourceId`, `amount` |
| `HealEvent` | Entity healed | `casterId`, `healedId`, `amount` |

## Example: Subscribe to Events

```java
SpellbookEventBus eventBus = SpellbookPlugin.getInstance().getEventBus();

eventBus.subscribe(SpellCastEvent.class, event -> {
    System.out.println("Player " + event.playerId() + " cast " + event.spellId());
});

eventBus.subscribe(EntityKillEvent.class, event -> {
    System.out.println("Player " + event.casterId() + " killed " + event.killedEntityId() + " with " + event.spellId());
});
```
