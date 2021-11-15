---
description: >-
  This tutorial will show you some ways many professional Fabric Mod Developers
  register, and store their items.
---

# Creating a Class to store your Items

### Introduction

Your ModInitializer may get a bit messy and big if you create and store your item variables in it.

Many known developers usually store their items in a separate class.

### Creating the Class

Lets create the class and move our custom item variable over.

```java
public class MyModItems {
    public static final Item MY_ITEM = new Item(new FabricItemSettings().group(ItemGroups.MISC));
}
```

This seems a bit clunky. Your registry stuff is still in your ModInitializer!

This is where `static {}` comes in.

### Using `static {}` to register your items.

You can use `static {}` to assign your variables. =`static {}` is ran when the class is first referenced.\
Lets add it.

```java
public class MyModItems {
    public static final Item MY_ITEM;
    
    static {
        MY_ITEM = new Item(new FabricItemSettings().group(ItemGroups.MISC));
    }
}
```

However, your registry stuff is still in ModInitializer, lets create a utility method to allow us to register and create blocks at the same time.

Remove your registry stuff from your ModInitializer before continuing.

This should suffice.

```java
public class MyModItems {
    public static final Item MY_ITEM;
    
    static {
        MY_ITEM = new Item(new FabricItemSettings().group(ItemGroups.MISC));
    }
    
    
    private static Item register(String id, Item item) {
            return Registry.register(Registry.ITEM, new Identifier("<mod-id>", id), item);
    }
}
```

Now lets update our `static {}` to use the `new register(String id, Item item)` method.

```java
static {
        MY_ITEM = register("my_item", new Item(new FabricItemSettings().group(ItemGroups.MISC)));
}
```

You are now assigning your variable and registering it at the same time. Pretty cool huh 👌

However, when you run the game. Your blocks aren't showing up. This is because your items class isn't being referenced anywhere. We'll need to initialize the class.

### Creating an `Initializer()` method.

The initializer method doesn't need to contain any code. It just needs to exist because whenever you use init() for the first time you are essentially loading the class

```java
public static void init() { }
```

You can now use this in your ModInitializer:

```java
public void onInitalize() {
    // ...
    MyModItems.init()
}
```

