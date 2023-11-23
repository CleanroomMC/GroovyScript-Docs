---
title: "Compression Crafting"
description: "Converts any number of a single item into an output itemstack, with a configurable rf cost, consumption per tick amount, catalyst, and if the catalyst is consumed."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/extendedcrafting/CompressionCrafting.java"
---

# Compression Crafting (Extended Crafting)

## Description

Converts any number of a single item into an output itemstack, with a configurable rf cost, consumption per tick amount, catalyst, and if the catalyst is consumed.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.extendedcrafting.CompressionCrafting
mods.extendedcrafting.compressioncrafting/*(1)!*/
mods.extendedcrafting.compressionCrafting
mods.extendedcrafting.compression_crafting
mods.extendedcrafting.Compression
mods.extendedcrafting.compression
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `inputCount`, `catalyst`, `consumeCatalyst`, `powerCost`, `powerRate`:

    ```groovy
    mods.extendedcrafting.compressioncrafting.add(ItemStack, IIngredient, int, IIngredient, boolean, int, int)
    ```

- Adds recipes in the format `output`, `input`, `inputCount`, `catalyst`, `consumeCatalyst`, `powerCost`:

    ```groovy
    mods.extendedcrafting.compressioncrafting.add(ItemStack, IIngredient, int, IIngredient, boolean, int)
    ```


### Recipe Builder

Just like other recipe types, the Compression Crafting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.extendedcrafting.compressioncrafting.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires not null. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy IIngredient`. Sets the catalyst item for the recipe. Requires not null.

        ```groovy
        catalyst(IIngredient)
        ```

    - `#!groovy int`. Sets the amount of RF required to complete the craft. Requires greater than or equal to 0.

        ```groovy
        powerCost(int)
        ```

    - `#!groovy int`. Sets the maximum amount of RF consumed per tick until the entire cost is paid. Requires greater than or equal to 0.

        ```groovy
        powerRate(int)
        ```

    - `#!groovy int`. Sets the quantity of input items required. Requires greater than or equal to 0.

        ```groovy
        inputCount(int)
        ```

    - `#!groovy boolean`. Sets if the catalyst item is consumed when the recipe completes.

        ```groovy
        consumeCatalyst(boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.blakebr0.extendedcrafting.crafting.CompressorRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.extendedcrafting.compressioncrafting.recipeBuilder()
            .input(item('minecraft:clay'))
            .inputCount(100)
            .output(item('minecraft:gold_ingot') * 7)
            .catalyst(item('minecraft:diamond'))
            .consumeCatalyst(true)
            .powerCost(10000)
            .powerRate(1000)
            .register()

        mods.extendedcrafting.compressioncrafting.recipeBuilder()
            .input(item('minecraft:clay') * 10)
            .output(item('minecraft:diamond') * 2)
            .powerCost(1000)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given catalyst:

    ```groovy
    mods.extendedcrafting.compressioncrafting.removeByCatalyst(IIngredient)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.extendedcrafting.compressioncrafting.removeByInput(IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.extendedcrafting.compressioncrafting.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.extendedcrafting.compressioncrafting.removeAll()
    ```

???+ Example
    ```groovy
    mods.extendedcrafting.compressioncrafting.removeByCatalyst(item('extendedcrafting:material:11'))
    mods.extendedcrafting.compressioncrafting.removeByInput(item('minecraft:gold_ingot'))
    mods.extendedcrafting.compressioncrafting.removeByOutput(item('extendedcrafting:singularity:6'))
    mods.extendedcrafting.compressioncrafting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.extendedcrafting.compressioncrafting.streamRecipes()
    ```
