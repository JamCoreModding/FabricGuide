---
description: This tutorial will show creating custom blocks
---

# Creating Custom Blocks

Make sure you have the [required resources](required-resources-blocks.md) before you start.

### Variable Creation

Adding a block is very simple. First, we need to create a new variable of our block:

```java
public static final Block MY_BLOCK = new Block(FabricBlockSettings().of(Material.STONE));
```

This creates a simple block, where the material is stone. There are many kinds of materials like stone, metal, air, amethyst, cake. They are in the `Material` class.

### Block Properties

There are also some other methods in `FabricBlockSettings` like setting the strength (hardness and resistance).

```java
public static final Block MY_BLOCK = new Block(FabricBlockSettings.of(Material.STONE).strength(3, 10));
```

### Registering The Block

Now, in your `ModInitializer`, you can register the block.

```java
Registry.register(Registry.BLOCK, new Identifier("<mod id>", "my_block"), MY_BLOCK);
```

### Adding a BlockItem

Most blocks have an item form too (i.e. in the inventory), so we will register their item form too. Registering the block item is similar to registering an item from the item tutorial.

```java
Registry.register(Registry.ITEM, new Identifier("<mod id>", "my_block"), new BlockItem(MY_BLOCK, new FabricItemSettings().group(ItemGroup.BUILDING_BLOCKS)))
```

**You must add the required json for your block to appear in-game. Else it will appear invincible and glitched.**
