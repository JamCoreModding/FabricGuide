---
description: >-
  This tutorial will show you how to listen to events added by Fabric API or
  other mods
---

# Listening to Fabric API Events

By listening for events, you can execute code whenever a certain action/event occurs. In this example, we'll show you how to damage a player when they try to sleep. You can find a full list of events on [this page](list-of-fabric-api-events.md)

To listen for when an entity attempts to sleep, we can use `EntitySleepEvents` like so:

{% code title="ModInitializer.java" %}
```java
@Override
public void onInitialize() {
    EntitySleepEvents.START_SLEEPING.register((entity, sleepingPos) -> {
        entity.damage(1.0f, DamageSource.GENERIC);
    });
}
```
{% endcode %}

`EntitySleepEvents.START_SLEEPING` is an `Event<...>` that is called when an entity starts to sleep. This specific event gives us the parameters `LivingEntity entity` and `BlockPos sleepingPos`

We then use these parameters inside a lambda expression to damage the entity.

If you launch the game and try to sleep, you should find you get damaged slightly.
