---
title: "Magnet"
description: "Add or remove items from the magnet blacklist"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/Magnet.java"
---

# Magnet (Botania)

## Description

Add or remove items from the magnet blacklist

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.botania.magnet/*(1)!*/
mods.botania.Magnet
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds the given Block, IBlockState, or IIngredient to the magnet blacklist:

    ```groovy
    mods.botania.magnet.addToBlacklist(Block, int)
    ```

- Adds the given Block, IBlockState, or IIngredient to the magnet blacklist:

    ```groovy
    mods.botania.magnet.addToBlacklist(IBlockState)
    ```

- Adds the given Block, IBlockState, or IIngredient to the magnet blacklist:

    ```groovy
    mods.botania.magnet.addToBlacklist(IIngredient)
    ```

???+ Example
    ```groovy
    mods.botania.magnet.addToBlacklist(item('minecraft:diamond'))
    ```

## Removing Entries

- Removes the given Block, IBlockState, or IIngredient from the magnet blacklist:

    ```groovy
    mods.botania.magnet.removeFromBlacklist(Block, int)
    ```

- Removes the given Block, IBlockState, or IIngredient from the magnet blacklist:

    ```groovy
    mods.botania.magnet.removeFromBlacklist(IBlockState)
    ```

- Removes the given Block, IBlockState, or IIngredient from the magnet blacklist:

    ```groovy
    mods.botania.magnet.removeFromBlacklist(IIngredient)
    ```


## Getting the value of entries

- Checks if the given Block, IBlockState, or IIngredient is prevented from being interacted with by the magnet:

    ```groovy
    mods.botania.magnet.isInBlacklist(Block, int)
    ```

- Checks if the given Block, IBlockState, or IIngredient is prevented from being interacted with by the magnet:

    ```groovy
    mods.botania.magnet.isInBlacklist(IBlockState)
    ```

- Checks if the given Block, IBlockState, or IIngredient is prevented from being interacted with by the magnet:

    ```groovy
    mods.botania.magnet.isInBlacklist(IIngredient)
    ```
