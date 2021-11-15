---
description: This tutorial will show creating custom items.
---

# Creating Custom Items

### Variable Creation

Creating a Custom Item is simple. First Initialize a Item variable.

```java
public static final Item MY_ITEM = new Item(
    new FabricItemSettings() // Item Settings
        .group(ItemGroup.MISC) // Set the item's group to Miscellaneous
        .fireproof() // Make it fireproof like netherite tools.
);
```

Your Item will appear in the group "Miscellaneous" and be fireproof.

### Custom Item Group

To assign your `Item` to a custom `ItemGroup` (creative inventory tab), you must use the `FabricItemGroupBuilder`&#x20;

```java
public static final ItemGroup MY_ITEM_GROUP = FabricItemGroupBuilder.build(
		new Identifier("<mod-id>", "my_item_group"), // The Identifier of the ItemGroup
		() -> new ItemStack(Blocks.DIAMOND_BLOCK)); // What item/block should be used for the icon.
```

You can add your `Item` to the `ItemGroup` by using it in the `.group()` method of `FabricItemSettings`:

```java
new FabricItemSettings().group(MY_ITEM_GROUP)
```

### Item Properties

Using `FabricItemSettings` you can specify the following:

{% tabs %}
{% tab title="Food Component" %}
The `.food(FoodComponent component)` allows you to make your item edible.

Food Components can be made using the `FoodComponent.Builder()`

|                      Method                     |                                                                                              Info                                                                                              |
| :---------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|              `.hunger(int hunger)`              |                                    <p>The <code>int hunger</code> variable is how </p><p>many hunger points the food </p><p>should replenish when eaten.</p>                                   |
| `.saturationModifier(float saturationModifier)` |         <p>The <code>float saturationModifier</code> is how much saturation should be multiplied by when eaten. </p><p>Golden Carrots have a <code>saturationModifier of 15</code></p>         |
|                    `.meat()`                    |                                                                       Specifies if the food should be considered as meat.                                                                      |
|                `.alwaysEdible()`                |                                               Specifies if the food can be eaten when the hunger points bar is full. Chorus Fruit is an example.                                               |
|                    `.snack()`                   |                                                             Specifies is the food is a snack. Cake, Cookies and Kelp are examples.                                                             |
|  `.statusEffect(StatusEffectInstance instance)` | Adds a status effect to the item. See [`StatusEffectInstance`](https://maven.fabricmc.net/docs/yarn-20w16a+build.9/net/minecraft/entity/effect/StatusEffectInstance.html) for more infomation. |
|                    `.build()`                   |                                                                                   Builds the `FoodComponent`                                                                                   |

**Example:**

```java
new FabricItemSettings()
        .food((new FoodComponent.Builder())
                .hunger(5) // Add 5 Hunger Points when ate.
                .saturationModifier(12) // Add 12 saturation.
                .meat() // Sorry vegans...
                .alwaysEdible() // Allow the player to always eat it.
                .build() // Build the FoodComponent
        );
```
{% endtab %}

{% tab title="Max Stack Count" %}
The Max Stack Count is how many items can be placed in one stack.&#x20;

The minimum is 1 and the maximum is 64 usually. Enderpearls, Snowballs and Signs have a max stack count of 16.

#### Example:

```java
new FabricItemSettings().maxCount(42); // Only allow a max stack of 42.
```
{% endtab %}

{% tab title="Max Damage" %}
Max Damage is usually the durability of the `Item`&#x20;

It usually only applied to tools.

#### Example:

```java
// Override the durability to 42
new FabricItemSettings().maxDamage(42); 

// Set the durability to 42 if the durability hasn't been already set.
new FabricItemSettings().maxDamageIfAbsent(42); 
```

It is recommended to use `maxDamageIfAbsent(int maxDamage)` whenever possible.
{% endtab %}

{% tab title="Recipe Remainder" %}
The Recipe Remainder is what `Item` should be returned whenever the `Item` is used in a recipe. Milk has a Recipe Remainder of a bucket.

#### Example

```java
// Whenever this Item is used in crafting, it will turn into a bucket afterwards.
new FabricItemSettings().recipeRemainder(Items.BUCKET);
```
{% endtab %}

{% tab title="Group" %}
The `ItemGroup` (creative inventory tab) to show your item in.

#### Example:

```java
// Add the item to the Miscellaneous creative tab.
new FabricItemSettings.group(ItemGroups.MISC);
```
{% endtab %}

{% tab title="Rarity" %}
The cosmetic rarity of the `Item`. This only changes the color of the item name.

By default, all Items have the `Rarity.COMMON` rarity.

[Checkout the Official Minecraft Wiki for a breakdown of all the Rarities.](https://minecraft.fandom.com/wiki/Rarity#Tiers)

#### Example:

```java
// Set the rarity of the Item to common (white).
new FabricItemSettings().rarity(Rarity.COMMON);

// Set the rarity of the Item to epic (purple).
new FabricItemSettings().rarity(Rarity.EPIC);
```
{% endtab %}

{% tab title="Fireproof" %}
Makes the `Item` fireproof - resistant to lava and fire. Netherite Tools and Armor are Fireproof.

#### Example:

```java
new FabricItemSettings().fireproof();
```
{% endtab %}
{% endtabs %}
