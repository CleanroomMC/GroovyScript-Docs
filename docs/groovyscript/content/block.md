# Creating blocks

## The simplest way

```groovy
content.createBlock(String name).register()
```

Simple right?
Let's break it up:

- `content` is a global variable.
- `createBlock(String name)` creates a block and an item version and returns it. The name is the registry name and must only consist of lower
  case letters and `_`.
- `register()` registers the block and the item. Without this the block will not appear in game.

## Registering a block

The example above creates a simple block for you, but you can also create blocks yourself (to create custom behaviour).
Use the following methods to register custom blocks.

```groovy
content.registerBlock(String name, Block block)
content.registerBlock(String name, Block block, ItemBlock block)
```

## Texture

Minecraft's blocks need a texture (or multiple), a model file which describes how the textures are rendered and a block state file which points each block state to a model file. If groovy
can't find a model file or a block state file it will generate default files
at `.minecraft/groovy/assets/[pack id]/models/block/[block name].json` and `.minecraft/groovy/assets/[pack id]/blockstates/[item name].json`.
It will point to a texture you will need to place
at `.minecraft/groovy/assets/[pack id]/textures/blocks/[block name].png`.

## Translating the items name

By default, the items name will show up as `tile.[pack id].[block name].name`. To change that you need add an entry to
the lang file. GroovyScript generates a default lang file at `.minecraft/groovy/assets/[pack id]/lang/en_us.lang`.

!!! example

    First create a block

    ```groovy
    content.createBlock('dust_block')
    ```

    Let's assume that the pack id is `nomifactory` so that the item and block id will be `nomifactory:dust_block`.
    Insert this line into the lang file.

    ```mclang
    tile.nomifactory.dust_block.name=Heart of the universe
    ```

    (`tile.nomifactory.dust_block.name` is the default generated translation key. You can change to anything you want.) <br>
    Finally, put a texture at `.minecraft/groovy/assets/nomifactory/textures/items/dust_block.png`
