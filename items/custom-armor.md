---
description: This tutorial will show you how to create a custom armor material and set.
---

# Custom Armor

## The Armor Material

All armors in Minecraft have an armor material. This material contains infomation on durability, strength and other effects.

Lets begin by creating a class that implements `ArmorMaterial`&#x20;

This may look complicated - so we've commented as much as we could to break it down for you.

```java
public class MyArmorMaterial implements ArmorMaterial {

	// The base durability values of the armor. 
	// {helmet, chestplate, leggings, boots}
	private static final int[] BASE_DURABILITY = new int[] {13, 15, 16, 11};
	
	// The protection amount. Is increased by the Protection enchantments.
	// {helmet, chestplate, leggings, boots}
	// Leather uses {1, 2, 3, 1} whilst Diamond/Netherite uses {3, 6, 8, 3}
	private static final int[] PROTECTION_VALUES = new int[] {1, 3, 2, 1};
 
	@Override
	// Method to get the max durability of a certain slot.
	public int getDurability(EquipmentSlot slot) {
		// If slot is leggings, slot.getEntitySlotId() would be 2.
		// BASE_DURABILITY[2] = 16
		
		// X is the amount the durability should be multiplied. 
		// You may use PROTECTION_VALUES instead of a fixed number.
		float X = 1.0F;
		return BASE_DURABILITY[slot.getEntitySlotId()] * X;
	}
 
	@Override
	// Method to get the protection amount for a certain slot.
	public int getProtectionAmount(EquipmentSlot slot) {
		// If slot is helmet, slot.getEntitySlotId() would be 0.
		// PROTECTION_VALUES[0] = 1
		return PROTECTION_VALUES[slot.getEntitySlotId()];
	}
 
 	// Method to get the enchantability of the armor.
	@Override
	public int getEnchantability() {
		float X = 15F;
		// X is the chance of getting high level enchantments.
		return X;
	}
 
	@Override
	// Method to get the sound that plays when you equip the armor.
	public SoundEvent getEquipSound() {
		// Currently, it's set to the Iron equip sound. You may change this.
		return SoundEvents.ITEM_ARMOR_EQUIP_IRON;
	}
 
	@Override
	// Method to get the ingredient collection that the armor can be repaired with.
	public Ingredient getRepairIngredient() {
		// We've set it to Rotten Flesh and Diamonds, because why not.
		return Ingredient.ofItems(Items.ROTTEN_FLESH, Items.DIAMOND);
	}
 
	@Override
	// Self explanatory.
	public String getName() {
		// Name must be all lowercase.
		return "name";
	}
 
	@Override
	// Method to get the toughness of the armor.
	public float getToughness() {
		// For reference, Netherite is 4.5F and Leather is 0.5F
		return 1.0F;
	}
 
	@Override
	// Method to get the knockback resistance multiplier.
	public float getKnockbackResistance() {
		// Usually, this is 0.0F, although Netherite has a multiplier of 1.2F
		return 0.0F;
	}
}
```

## The Armor Items

Using the lovely, organized class you made in [Creating a Class to store your Items](creating-a-class-to-store-your-items.md), lets create some ArmorItems that uses `MyArmorMaterial`&#x20;

```java
public class MyModItems {
    // ...
    public static final Item MY_HELMET;
    public static final Item MY_CHESTPLATE;
    public static final Item MY_LEGGINGS;
    public static final Item MY_BOOTS;
    
    static {
        // ...
        MyArmorMaterial material = new MyArmorMaterial();
        
        MY_HELMET = register("my_helmet", new ArmorItem(material, EquipmentSlot.HEAD, new Item.Settings().group(ItemGroup.MISC)));
        MY_CHESTPLATE = register("my_chestplate", new ArmorItem(material, EquipmentSlot.CHEST, new Item.Settings().group(ItemGroup.MISC)));
        MY_LEGGINGS = register("my_chestplate", new ArmorItem(material, EquipmentSlot.LEGS, new Item.Settings().group(ItemGroup.MISC)));
        MY_BOOTS = register("my_boots", new ArmorItem(material, EquipmentSlot.FEET, new Item.Settings().group(ItemGroup.MISC)));
    }
    
    // ...
}
```

### Item Textures/Models

Your Armor Items must have normal item textures and models.&#x20;

See [Required Resources](creating-custom-items/required-resources-items.md) for more infomation on Item textures and models.

## Body Armor Textures

To give your armor textures when worn, you must create armor textures and place them in `src/main/resources/assets/minecraft/textures/models/armor/myarmor_layer_1.png`

#### Example - Iron Armor

[NovaSkin](https://minecraft.novaskin.me) is a great way to visualize your armor textures. Although heavily outdated with items and blocks, its armor layer editor is still working and compatible with the latest Minecraft version.

`layer_1.png `- Helmet, Chestplate, Boots - [NovaSkin Link](https://minecraft.novaskin.me/resourcepacks#default/assets/minecraft/textures/models/armor/iron\_layer\_1.png)

`layer_2.png `- Leggings - [NovaSkin Link](https://minecraft.novaskin.me/resourcepacks#default/assets/minecraft/textures/models/armor/iron\_layer\_2.png)

## Advanced - Adding Status Effects

This section gets into mixins, if you haven't already followed the mixins guide. [I suggest you do so here before continuing.](../mixin/untitled.md)
