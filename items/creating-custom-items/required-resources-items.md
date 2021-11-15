---
description: Your item has to have a few json files before it can fully appear in-game.
---

# Required Resources

### Texture

Your `Item` must have a 16x16 texture in the `src/resources/assets/<mod-id>/textures/item/` folder.

The path for this example texture is:

`src/resources/assets/<mod-id>/textures/item/my_item.png`

![Blue Book, spooky eh? Credit: BlueCommander](<../../.gitbook/assets/image (8).png>)

### Item Model

Your `Item` must have a model for your texture to appear in-game.

For the `Item` that you made in [Creating Custom Items](./), the model file would look like this:

{% code title="/src/main/resources/assets/<mod-id>/models/item/my_item.json" %}
```javascript
{
  "parent": "item/generated",
  "textures": {
    "layer0": "<my-mod>:item/my_item"
  }
}
```
{% endcode %}

This is a basic item texture. [For more info on item model types, checkout the Minecraft wiki.](https://minecraft.fandom.com/wiki/Model#Item\_models)

### Crafting Recipe

This is optional. [A useful tool for generating crafting recipes can be found here.](https://crafting.thedestruc7i0n.ca)

{% code title="/src/main/resources/data/<mod-id>/recipes/my_item.json" %}
```javascript
{
    "type": "minecraft:crafting_shaped",
    "pattern": [
        "# #",
        " # ",
        "# #"
    ],
    "key": {
        "#": {
            "item": "minecraft:polished_andesite"
        }
    },
    "result": {
        "item": "my_mod:my_item",
        "count": 1
    }
}
```
{% endcode %}

![](<../../.gitbook/assets/image (1).png>)
