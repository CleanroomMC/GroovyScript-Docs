---
title: "Carving"
description: "Sets a group of items any item can be converted between freely, in world and in a GUI"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/chisel/Carving.java"
---

# Carving (Chisel)

## Description

Sets a group of items any item can be converted between freely, in world and in a GUI

???+ Warning
    This compat is not fully documented. Some or all of its features are not present on the wiki. View the source code to gain an accurate understanding of the compat.

!!! Danger
    You cannot addVariation/removeVariation to chisel groups based on the oredict, you have to modify the oredict directly.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.chisel.carving/*(1)!*/
mods.chisel.Carving
```

1. This identifier will be used as the default for examples on this page

## Editing Values

- Sets the sound of the Chisel Group:

    ```groovy
    mods.chisel.carving.setSound(ICarvingGroup, SoundEvent)
    ```

- Sets the sound of the Chisel Group:

    ```groovy
    mods.chisel.carving.setSound(String, SoundEvent)
    ```

???+ Example
    ```groovy
    mods.chisel.carving.setSound('demo', sound('minecraft:block.glass.break'))
    ```

## Adding Entries

- Adds a new Chisel Group with the given name:

    ```groovy
    mods.chisel.carving.addGroup(String)
    ```

- Adds a new Item Variation to the Chisel Group:

    ```groovy
    mods.chisel.carving.addVariation(String, ItemStack)
    ```

???+ Example
    ```groovy
    mods.chisel.carving.addGroup('demo')
    mods.chisel.carving.addVariation('demo', item('minecraft:diamond_block'))
    mods.chisel.carving.addVariation('demo', item('chisel:antiblock:3'))
    mods.chisel.carving.addVariation('demo', item('minecraft:sea_lantern'))
    ```

## Removing Entries

- Removes all Chisel Groups and Variations within each Chisel Group:

    ```groovy
    mods.chisel.carving.removeAll()
    ```

- Removes a Chisel Group and all Item Variations with that Chisel Group:

    ```groovy
    mods.chisel.carving.removeGroup(String)
    ```

- Removes an Item Variation from the given Chisel Group:

    ```groovy
    mods.chisel.carving.removeVariation(String, ItemStack)
    ```

???+ Example
    ```groovy
    mods.chisel.carving.removeAll()
    mods.chisel.carving.removeGroup('blockDiamond')
    mods.chisel.carving.removeVariation('antiblock', item('chisel:antiblock:3'))
    mods.chisel.carving.removeVariation('antiblock', item('chisel:antiblock:15'))
    ```
