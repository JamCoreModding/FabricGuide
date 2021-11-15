---
description: >-
  This tutorial will show you some ways many professional Fabric Mod Developers
  register, and store their blocks.
---

# Creating a Class to store your Blocks.

### Introduction

Your ModInitializer may get a bit messy and big if you create and store your block variables in it.

Many known developers usually store their blocks in a separate class.

### Creating the Class

Lets create the class and move our custom block variable over.

```java
public class MyModBlocks {
    public static final Block MY_BLOCK = new Block(FabricBlockSettings.of(Material.STONE).strength(3, 10));
}
```

This seems a bit clunky. Your registry stuff is still in your ModInitializer!

This is where `static {}` comes in.

### Using `static {}` to register your blocks.

You can use `static {}` to assign your variables. =`static {}` is ran when the class is first referenced.\
Lets add it.

```java
public class MyModBlocks {
    public static final Block MY_BLOCK;
    
    static {
        MY_BLOCK = new Block(FabricBlockSettings.of(Material.STONE).strength(3, 10));
    }
}
```

However, your registry stuff is still in ModInitializer, lets create a utility method to allow us to register and create blocks at the same time.

Remove your registry stuff from your ModInitializer before continuing.

This should suffice.

```java
public class MyModBlocks {
    public static final Block MY_BLOCK;
    
    static {
        MY_BLOCK = new Block(FabricBlockSettings.of(Material.STONE).strength(3, 10));
    }
    
    
    private static Block register(String id, Block block) {
            return Registry.register(Registry.BLOCK, new Identifier("<mod-id>", id), block);
    }
}
```

Now lets update our `static {}` to use the `new register(String id, Block block)` method.

```java
static {
        MY_BLOCK = register("my_block", new Block(FabricBlockSettings.of(Material.STONE).strength(3, 10)));
}
```

You are now assigning your variable and registering it at the same time. Pretty cool huh 👌

However, when you run the game. Your blocks aren't showing up. This is because your blocks class isn't being referenced anywhere. We'll need to initialize the class.

### Creating an `Initializer()` method.

The initializer method doesn't need to contain any code. It just needs to exist because whenever you use init() for the first time you are essentially loading the class

```java
public static void init() { }
```

You can now use this in your ModInitializer:

```java
public void onInitalize() {
    // ...
    MyModBlocks.init()
}
```
