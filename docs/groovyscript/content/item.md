# Creating items

## The simplest way

```groovy
content.createItem(String name).register()
```

Simple right?
Let's break it up:

- `content` is a global variable.
- `createItem(String name)` creates an item and returns it. The name is the registry name and must only consist of lower
  case letters and `_`.
- `register()` registers the item. Without this the item will not appear in game.

## Registering an item

The example above creates a simple item for you, but you can also create items yourself (to create custom behaviour).
Use the following methods to register custom items.

```groovy
content.registerItem(String name, Item item)
```

## Texture

Minecraft's items need a texture (or multiple) and a model file which describes how the textures are rendered. If groovy
can't find a model file it will generate a default file
at `.minecraft/groovy/assets/[pack id]/models/item/[item name].json`.
It will point to a texture you will need to place
at `.minecraft/groovy/assets/[pack id]/textures/items/[item name].png`.

## Translating the items name

By default, the items name will show up as `item.[pack id].[item name].name`. To change that you need add an entry to
the lang file. GroovyScript generates a default lang file at `.minecraft/groovy/assets/[pack id]/lang/en_us.lang`.

!!! example

    First create an item

    ```groovy
    content.createItem('heart_of_the_universe')
    ```

    Let's assume that the pack id is `nomifactory` so that the item id will be `nomifactory:heart_of_the_universe`.
    Insert this line into the lang file.

    ```mclang
    item.nomifactory.heart_of_the_universe.name=Heart of the universe
    ```

    (`item.nomifactory.heart_of_the_universe.name` is the default generated translation key. You can change to anything you want.) <br>
    Finally, put a texture at `.minecraft/groovy/assets/nomifactory/textures/items/heart_of_the_universe.png`
