---
title: "Treasure Chest"
description: "A weighted item, with a weight to obtain and a minimum and maximum amount. Obtained via right-clicking a Treasure Chest spawning randomly on the sea floor."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/actuallyadditions/TreasureChest.java"
---

# Treasure Chest (Actually Additions)

## Description

A weighted item, with a weight to obtain and a minimum and maximum amount. Obtained via right-clicking a Treasure Chest spawning randomly on the sea floor.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="6"
mods.aa.TreasureChest
mods.aa.treasurechest
mods.aa.treasureChest
mods.aa.treasure_chest
mods.actuallyadditions.TreasureChest
mods.actuallyadditions.treasurechest/*(1)!*/
mods.actuallyadditions.treasureChest
mods.actuallyadditions.treasure_chest
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Treasure Chest also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.actuallyadditions.treasurechest.recipeBuilder()"
    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. Sets the maximum stack size given when rolled. Requires greater than or equal to 0 and greater than or equal to min. (Default `0`).

        ```groovy
        max(int)
        ```

    - `#!groovy int`. Sets the minimum stack size given when rolled. Requires greater than or equal to 0 and less than or equal to max. (Default `0`).

        ```groovy
        min(int)
        ```

    - `#!groovy int`. Sets how likely this loot is to be rolled. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        weight(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `de.ellpeck.actuallyadditions.api.recipe.TreasureChestLoot`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.actuallyadditions.treasurechest.recipeBuilder()
            .output(item('minecraft:clay'))
            .weight(50)
            .min(16)
            .max(32)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.actuallyadditions.treasurechest.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.actuallyadditions.treasurechest.removeAll()
    ```

???+ Example
    ```groovy
    mods.actuallyadditions.treasurechest.removeByOutput(item('minecraft:iron_ingot'))
    mods.actuallyadditions.treasurechest.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.actuallyadditions.treasurechest.streamRecipes()
    ```
