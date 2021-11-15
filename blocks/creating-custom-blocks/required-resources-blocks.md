---
description: Your block has to have a few json files before it can fully appear in-game.
---

# Required Resources

### Texture

Well, that's a bit obvious! Your block texture should be 16px by 16px and be in the `/src/main/resources/assets/<mod-id>/textures/block/` folder.

The path for this example texture is: `src/main/resources/assets/<mod-id>/textures/block/my_block.png`

![Swirly Dirt! Who doesn't like swirly dirt? Credit: Ara - Artstation](<../../.gitbook/assets/image (3).png>)

### Block Model

To apply the texture to your block - you need a model.

For the Custom Block that you made in [Creating Custom Blocks](./), the model file would look like this:

{% code title="/src/main/resources/assets/<mod-id>/models/block/my_block.json" %}
```javascript
{
  "parent": "block/cube_all",
  "textures": {
    "all": "<mod-id>:block/my_block"
  }
}
```
{% endcode %}

This would assign the `my_block.png` texture to all sides of the block. For a more in-depth information on block models, [checkout the Minecraft wiki.](https://minecraft.fandom.com/wiki/Model#Block\_models)

### Item Model

Your block will need an Item model. Luckily its pretty easy.

For the BlockItem that you made in [Creating Custom Blocks](./), the model file would look like this:

{% code title="/src/main/resources/assets/<mod-id>/models/item/my_block.json" %}
```javascript
{
    "parent": "<mod-id>:block/my_block"
}
```
{% endcode %}

This means that the Item model will be the same as the block model.

### Block State

The [BlockState ](../../how-does-minecraft-work.md#what-is-a-block-exactly)can be used if you want to show different textures whenever your block has certain NBT tags applied to it.

For the Custom Block that you made in [Creating Custom Blocks](./), the BlockState file would look like this.

{% code title="/src/main/resources/assets/<mod-id>/blockstates/my_block.json" %}
```javascript
{
  "variants": {
    "": { "model": "<mod-id>:block/my_block" }
  }
}
```
{% endcode %}

Basically, since your block doesn't have any NBT data related to it, `""` can be used.

### Loot Table

This is technically optional, but its recommended if you want your block to drop itself when broken in survival.

Loot Tables are stored in `/src/main/resources/data/<mod-id/loot_tables/`&#x20;

For the Custom Block that you made in [Creating Custom Blocks](./), the loot table file would look like this.

{% code title="/src/main/resources/data/<mod-id>/loot_tables/my_block.json" %}
```javascript
{
  "type": "minecraft:block",
  "pools": [
    {
      "rolls": 1,
      "entries": [
        {
          "type": "minecraft:item",
          "name": "<mod-id>:my_block"
        }
      ],
      "conditions": [
        {
          "condition": "minecraft:survives_explosion"
        }
      ]
    }
  ]
}
```
{% endcode %}

This will mean your block will drop when mined, and will survive explosions. You can remove the `minecraft:survives_explosion` condition if you want your block to not drop itself when broken via an explosion.



