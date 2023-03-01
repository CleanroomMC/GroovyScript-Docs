# Creating items

## The simplest way

````groovy
content.createItem(String name).register()
````

Simple right?
Let's break it up:

- `content` is a global variable.
- `createItem(String name)` creates an item and returns it. The name is the registry name and must only consist of lower
  case letters and `_`.
- `register()` registers the item. Without this the item will not appear in game.

## Texture

Minecraft's items need a texture (or multiple) and a model file which describes how the textures are rendered. If groovy
can't find a model file it will generate a default file
at `.minecraft/groovy/assets/[pack id]/models/item/[item name].json`.
It will point to a texture you will need to place
at `.minecraft/groovy/assets/[pack id]/textures/items/[item name].png`.

## Translating the items name

By default, the items name will show up as `item.[pack id].[item name].name`. To change that you need add an entry to
the lang file. GroovyScript generates a default lang file at `.minecraft/groovy/assets/[pack id]/lang/en_us.lang`.

### Example
If your items id is `nomifactory:heart_of_the_universe`, then you need to insert
````mclang
item.nomifactory.heart_of_the_universe.name=Heart of the universe
````
into your lang file.
(`item.nomifactory.heart_of_the_universe.name` is the default generated translation key. You can change to anything you want.)
