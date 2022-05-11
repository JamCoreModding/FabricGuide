---
description: >-
  A quick run-through of Minecraft behind the scenes. This is not a complete
  picture, but it gives a start for those who are unfamiliar with how Minecraft
  operates in-code.
---

# How does minecraft work?

## Registries

When you type `/give @s minecraft:grass` have you ever wondered where Minecraft gets the actual block from? The answer is a registry. Registries are large maps of content accessed by `Identifier` objects. Almost all pieces of content are stored in registries such as `Registry.BLOCK` or `Registry.ITEM`.

![Registries in a nutshell](<.gitbook/assets/image (5).png>)

Minecraft initialises all the registries during the loading screen, and mod-loaders such as Fabric run your mod's initializers afterwards. This is when you would typically register all the blocks, items and entities from your mod into Minecraft's registry lists.

#### What's an identifier?

Identifiers are how Minecraft tracks and identifies content and resources. They consist of two parts: The **namespace** and the **path**. The namespace is typically the ID of the mod, and in the case of vanilla content: '`minecraft`'. The path is the name of the content (in the case of content), and the file path relative to the namespace (in the case of resources).

\
Identifiers are typically expressed visually as `namespace:path` which you can see in console commands that specify a piece of content (`minecraft:dirt` ).

## What is a Block?

Blocks in Minecraft are '[Singleton](https://www.geeksforgeeks.org/singleton-class-java/)' classes, only one instance of a block exists at any time. This singular instance is the one you send to the registry in the mod. You can picture it as the singular instance managing all blocks that identify as belonging to said block.\
\
So how does a block store state then? There are clearly blocks that have state like slabs, doors and stairs. This is what the aptly named `BlockState` class is for. `BlockState`s, aside from containing a reference to the singleton Block, are primarily a map of `Property`objects. Properties themselves are just single values labelled with a name, and hey can be Booleans, Integers, Enums, etc.

\
An example of an existing property is the`SLAB_TYPE`property, it's used in slabs to determine the state of the slab block: top slab, bottom slab or _double_ slab.\
An example of a `BlockState` would be:\
`minecraft:quartz_slab`\
`-type: bottom`\
`-waterlogged: false`

![How the singleton operates](<.gitbook/assets/image (7).png>)

`BlockState`s are the ''real'' terrain data stored in chunks. Minecraft stores large lists of them as integers in special structures known as chunk sections (typically a 16x16x16 region of blocks), which are in turn stored as a list in a more familiar world chunk.

![A chunk section (Empty chunk sections are not stored)](<.gitbook/assets/image (2).png>)

\
`BlockState`s come with a downside however; internally all possible states of a specific block are stored. Since adding more properties exponentially increases the amount of `BlockState`s, a more robust solution is needed to store advanced blocks such as chests, crafting tables, furnaces and etc, which contain more complex data.

### The Block Entity

{% hint style="info" %}
TL;DR: Block Entities allow custom rendering and advanced states but need to be applied carefully to avoid lag.
{% endhint %}

The block entity is a special object that allows blocks (or more accurately, coordinates in the world) to have more advanced states and behaviours. Block Entities are also the only way a block can update itself every tick, as opposed to relying on random ticks like plants or neighbour update triggers like observers and fences. Any block that needs to store 'complex' data such as items or even just tracking progress bar would require a block entity. Block entities also allow more complex rendering mechanisms such as the floating book you see on the enchantment table.

However, being more expensive, block entities should be used sparingly for blocks that truly need it to avoid lag in servers. For example: you may think the crafting table uses a block entity, but since it does not retain a state (everything resets as soon as you leave the table), it does not use a block entity, and instead is simply a normal block that spawns a crafting screen on use.

Block Entities are stored in a separate map structure in a chunk, separate from chunk sections. They are accessed via a coordinate key and are somewhat inexpensive to retrieve.

### Block Models

_"Ok but what even decides what model Minecraft shows for any block? "_

You may have noticed if you've defined a blockstate json file you needed to specify the model [Identifier](how-does-minecraft-work.md#whats-an-identifier), this is where normal blocks get their models from. Typically the models are vanilla presets (e.g. `block/cubeall`), custom models made in a external application (such as BlockBench), or code-[generated](https://fabricmc.net/wiki/tutorial:custom\_model) (used for connected textures).\
`BlockEntityRenderer` objects directly use `ModelPart` objects in order to render models\
as opposed to json files. Model parts are processed versions of `TexturedModelData` objects, which are cuboids **manually defined** in code. `ModelPart` objects are typically fetched via an `EntityModelLayer` instance, which are essentially identifiers specifically for `TexturedModelData`Objects, allowing model parts to be accessed globally by renderers. This manual method of creating a `TexturedModelData` object is extremely error-prone even for simple models (the creeper was born from a mistake using this). As such, services such as BlockBench allow you to generate code files for `TexturedModelData` objects from models created on their application.



![Simplified view of the process](<.gitbook/assets/image (10).png>)

![A more detailed view of the process](<.gitbook/assets/image (11).png>)
