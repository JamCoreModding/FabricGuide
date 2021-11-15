---
description: >-
  This is a list of all Fabric API events, their descriptions and their
  parameters. It is up-to-date as of 12/09/2021 (Fabric API version
  0.40.1+1.17). Deprecated events were not included.
---

# List of Fabric API Events

| Class Name                                           |          Event Name         |                                          Description                                          |
| ---------------------------------------------------- | :-------------------------: | :-------------------------------------------------------------------------------------------: |
| `EntitySleepEvents`                                  |       `ALLOW_SLEEPING`      |            Called to check whether a player can start to sleep in a bed-like block.           |
| `EntitySleepEvents`                                  |       `START_SLEEPING`      |                             Called when an entity starts to sleep                             |
| `EntitySleepEvents`                                  |       `STOP_SLEEPING`       |                                 Called when an entity wakes up                                |
| `EntitySleepEvents`                                  |         `ALLOW_BED`         |               Called to check whether a block is valid for sleeping (i.e. a bed)              |
| `EntitySleepEvents`                                  |      `ALLOW_SLEEP_TIME`     |             Called to check whether the current time of day is valid for sleeping             |
| `EntitySleepEvents`                                  |   `ALLOW_NEARBY_MONSTERS`   |              Called to check whether a player can sleep when monsters are nearby              |
| `EntitySleepEvents`                                  |   `ALLOW_RESETTINGS_TIME`   | Called to check whether a sleeping player counts into skipping the day and resetting the time |
| `EntitySleepEvents`                                  | `MODIFY_SLEEPING_DIRECTION` |                Called to provide the entity's sleep direction if it is missing                |
| `EntitySleepEvents`                                  |    `ALLOW_SETTING_SPAWN`    |               Called to check whether the players spawn can be set when sleeping              |
| `ServerEntityCombatEvents`                           | `AFTER_KILLED_OTHER_ENTITY` |           Called after an entity is directly responsible for killing another entity           |
| `ServerEntityWorldChangeEvents`                      | `AFTER_ENTITY_CHANGE_WORLD` |                   Called after an entity has been moved to a different world                  |
| `ServerEntityWorldChangeEvents`                      | `AFTER_PLAYER_CHANGE_WORLD` |                   Called after a player has been moved to a different world                   |
| `ServerPlayerEvents`                                 |         `COPY_FROM`         |                 Called when data from an old player is copied to a new player                 |
| `ServerPlayerEvents`                                 |       `AFTER_RESPAWN`       |                            Called after a player has been respawned                           |
| `ServerPlayerEvents`                                 |        `ALLOW_DEATH`        |                            Called when a player takes fatal damage                            |
| `ClientPickBlockApplyCallback`                       |           `EVENT`           |     Called during the block-picking process to modify or nullify the returned `ItemStack`     |
| `ClientPickBlockGatherCallback`                      |           `EVENT`           |    Called at the beginning of the block-picking process to find any applicable `ItemStack`    |
| `AttackBlockCallback`                                |           `EVENT`           |                        Called when a player attacks/left clicks a block                       |
| `AttackEntityCallback`                               |           `EVENT`           |                       Called when a player attacks/left clicks an entity                      |
| `PlayerBlockBreakEvents`                             |           `BEFORE`          |                                Called before a block is broken                                |
| `PlayerBlockBreakEvents`                             |           `AFTER`           |                                 Called after a block is broken                                |
| `PlayerBlockBreakEvents`                             |         `CANCELLED`         |                             Called when a block break is cancelled                            |
| `UseBlockCallback`                                   |           `EVENT`           |                         Called when a player uses/right clicks a block                        |
| `UseEntityCallback`                                  |           `EVENT`           |                        Called when a player uses/right clicks an entity                       |
| `UseItemCallback`                                    |           `EVENT`           |                      Called when a player uses/right clicks with an item                      |
| `ItemTooltipCallback`                                |           `EVENT`           |                   Called after the game has appended all base tooltip lines                   |
| `ClientBlockEntityEvents`                            |     `BLOCK_ENTITY_LOAD`     |                   Called when a `BlockEntity` is loaded into a `ClientWorld`                  |
| `ClientBlockEntityEvents`                            |    `BLOCK_ENTITY_UNLOAD`    |            Called when a `BlockEntity` is about to be unloaded from a `ClientWorld`           |
| `ClientChunkEvents`                                  |         `CHUNK_LOAD`        |                       Called when a chunk is loaded into a `ClientWorld`                      |
| `ClientChunkEvents`                                  |        `CHUNK_UNLOAD`       |                Called when a chunk is about to be unloaded from a `ClientWorld`               |
| `ClientEntityEvents`                                 |        `ENTITY_LOAD`        |                     Called when an `Entity`is loaded into a `ClientWorld`                     |
| `ClientEntityEvents`                                 |       `ENTITY_UNLOAD`       |                    Called when an `Entity` is unloaded from a `ClientWorld`                   |
| `ClientLifecycleEvents`                              |       `CLIENT_STARTED`      |                                Called when Minecraft is started                               |
| `ClientLifecycleEvents`                              |      `CLIENT_STOPPING`      |                         Called when Minecraft's client begins to stop                         |
| `ClientTickEvents`                                   |     `START_CLIENT_TICK`     |                             Called at the start of the client tick                            |
| `ClientTickEvents`                                   |      `END_CLIENT_TICK`      |                              Called at the end of the client tick                             |
| `ClientTickEvents`                                   |      `START_WORLD_TICK`     |                         Called at the start of a `ClientWorld`'s tick                         |
| `ClientTickEvents`                                   |       `END_WORLD_TICK`      |                          Called at the end of a `ClientWorld`'s tick                          |
| `ServerBlockEntityEvents`                            |     `BLOCK_ENTITY_LOAD`     |                   Called when a `BlockEntity` is loaded into a `ServerWorld`                  |
| `ServerBlockEntityEvents`                            |    `BLOCK_ENTITY_UNLOAD`    |            Called when a `BlockEntity` is about to be unloaded from a `ClientWorld`           |
| `ServerChunkEvents`                                  |         `CHUNK_LOAD`        |                       Called when a chunk is loaded into a `ServerWorld`                      |
| `ServerChunkEvents`                                  |        `CHUNK_UNLOAD`       |                Called when a chunk is about to be unloaded from a `ServerWorld`               |
| `ServerEntityEvents`                                 |        `ENTITY_LOAD`        |                     Called when an `Entity`is loaded into a `ServerWorld`                     |
| `ServerEntityEvents`                                 |       `ENTITY_UNLOAD`       |                    Called when an `Entity` is unloaded from a `ServerWorld`                   |
| `ServerLifecycleEvents`                              |      `SERVER_STARTING`      |                           Called when a Minecraft server is starting                          |
| `ServerLifecycleEvents`                              |       `SERVER_STARTED`      |               Called when a Minecraft server is about to tick for the first time              |
| `ServerLifecycleEvents`                              |      `SERVER_STOPPING`      |                    Called when a Minecraft server has started shutting down                   |
| `ServerLifecycleEvents`                              |       `SERVER_STOPPED`      |                           Called when a Minecraft server has stopped                          |
| `ServerLifecycleEvents`                              |   `START_DATA_PACK_RELOAD`  |                      Called before a Minecraft server reloads data packs                      |
| `ServerLifecycleEvents`                              |    `END_DATA_PACK_RELOAD`   |                    Called after a Minecraft server has reloaded data packs                    |
| `ServerTickEvents`                                   |     `START_SERVER_TICK`     |                             Called at the start of the server tick                            |
| `ServerTickEvents`                                   |      `END_SERVER_TICK`      |                              Called at the end of the server tick                             |
| `ServerTickEvents`                                   |      `START_WORLD_TICK`     |                         Called at the start of a `ServerWorld`'s tick                         |
| `ServerTickEvents`                                   |       `END_WORLD_TICK`      |                          Called at the end of a `ServerWorld`'s tick                          |
| `ServerWorldEvents`                                  |            `LOAD`           |                   Called just after a world is loaded by a Minecraft server                   |
| `ServerWorldEvents`                                  |           `UNLOAD`          |                    Called before a world is unloaded by a Minecraft server                    |
| `LootTableLoadingCallback`                           |           `EVENT`           |                               Called when loot tables are loaded                              |
| `C2SPlayChannelEvents`                               |          `REGISTER`         |      Called when an update is received regarding the server's ability to receive packets      |
| `C2SPlayChannelEvents`                               |         `UNREGISTER`        |               Called to indicate the server's lack of ability to receive packets              |
| `ClientLoginConnectionEvents`                        |            `INIT`           |                       Called when a connection enters the `LOGIN` state                       |
| `ClientLoginConnectionEvents`                        |        `QUERY_START`        |                   Called when the client has started receiving login queries                  |
| `ClientLoginConnectionEvents`                        |         `DISCONNECT`        |                Called when the client's login process ends due to disconnection               |
| `ClientPlayConnectionEvents`                         |            `INIT`           |                        Called when a connection enters the `PLAY` state                       |
| `ClientPlayConnectionEvents`                         |            `JOIN`           |              Called when the client play network handler is ready to send packets             |
| `ClientPlayConnectionEvents`                         |         `DISCONNECT`        |                    Called when the client play network handler disconnects                    |
| `EntityTrackingEvents`                               |       `START_TRACKING`      |                       Called before the player starts tracking an entity                      |
| `EntityTrackingEvents`                               |       `STOP_TRACKING`       |                     Called after the player has stopped tracking an entity                    |
| `S2CPlayChannelEvents`                               |          `REGISTER`         |      Called when an update is received regarding the clients's ability to receive packets     |
| `S2CPlayChannelEvents`                               |         `UNREGISTER`        |               Called to indicate the client's lack of ability to receive packets              |
| `ServerLoginConnectionEvents`                        |            `INIT`           |                       Called when a connection enters the `LOGIN` state                       |
| `ServerLoginConnectionEvents`                        |        `QUERY_START`        |           Called when the queries from the server login network handler have started          |
| `ServerLoginConnectionEvents`                        |         `DISCONNECT`        |                    Called when the server play network handler disconnects                    |
| `ServerPlayConnectionEvents`                         |            `INIT`           |                        Called when a connection enters the `PLAY` state                       |
| `ServerPlayConnectionEvents`                         |            `JOIN`           |              Called when the sever play network handler is ready to send packets              |
| `ServerPlayConnectionEvents`                         |         `DISCONNECT`        |                    Called when the server play network handler disconnects                    |
| `DynamicRegistrySetupCallback`                       |           `EVENT`           |                     Called when a new `DynamicRegistryManager` is created                     |
| `HudRenderCallback`                                  |           `EVENT`           |         Called after rendering the whole HUD, so mods can add their own elements to it        |
| `InvalidateRenderStateCallback`                      |           `EVENT`           |                             Called when the world renderer reloads                            |
| `LivingEntityFeatureRenderer`-`RegistrationCallback` |           `EVENT`           |               Called when a feature renderer is registered for a `LivingEntity`               |
| `ScreenEvents`                                       |        `BEFORE_INIT`        |                             Called before a screen is initialised                             |
| `ScreenEvents`                                       |         `AFTER_INIT`        |                              Called after a screen is initialised                             |
