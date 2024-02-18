---
title: "Freezer"
description: "The Freezer is used to turn certain items into frozen versions."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/aether_legacy/Freezer.java"
---

# Freezer (GroovyScript - The Aether)

## Description

The Freezer is used to turn certain items into frozen versions.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.aether_legacy.freezer/*(1)!*/
mods.aether_legacy.freezer
mods.aether.freezer
mods.aether.freezer
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds a Freezer recipe in the format `input`, `output`, `time`.:

    ```groovy
    mods.aether_legacy.freezer.add(ItemStack, ItemStack, int)
    ```


### Recipe Builder

Just like other recipe types, the Freezer also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.aether_legacy.freezer.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. groovyscript.wiki.aether_legacy.freezer.time.value. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        time(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.gildedgames.the_aether.api.freezables.AetherFreezable`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.aether_legacy.freezer.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:dirt'))
            .time(200)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.aether_legacy.freezer.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.aether_legacy.freezer.removeAll()
    ```

???+ Example
    ```groovy
    mods.aether_legacy.freezer.removeByOutput(item('minecraft:obsidian'))
    mods.aether_legacy.freezer.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.aether_legacy.freezer.streamRecipes()
    ```
