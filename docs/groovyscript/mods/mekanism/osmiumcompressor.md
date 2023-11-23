---
title: "Osmium Compressor"
description: "Converts an input itemstack and 200 of a gasstack into an output itemstack. By default, will use Liquid Osmium as the gasstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/OsmiumCompressor.java"
---

# Osmium Compressor (Mekanism)

## Description

Converts an input itemstack and 200 of a gasstack into an output itemstack. By default, will use Liquid Osmium as the gasstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.OsmiumCompressor
mods.mekanism.osmiumcompressor/*(1)!*/
mods.mekanism.osmiumCompressor
mods.mekanism.osmium_compressor
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `ingredient`, `gasInput`, `output`:

    ```groovy
    mods.mekanism.osmiumcompressor.add(IIngredient, GasStack, ItemStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.osmiumcompressor.add(item('minecraft:diamond'), gas('hydrogen'), item('minecraft:nether_star'))
    ```

### Recipe Builder

Just like other recipe types, the Osmium Compressor also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.osmiumcompressor.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy GasStackList`. Sets the gas inputs of the recipe. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        gasInput(GasStack)
        gasInput(GasStack...)
        gasInput(Collection<GasStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.OsmiumCompressorRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.osmiumcompressor.recipeBuilder()
            .input(item('minecraft:diamond'))
            .gasInput(gas('hydrogen'))/*(1)!*/
            .output(item('minecraft:nether_star'))
            .register()
        ```

        1. Always uses 200 gas



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.osmiumcompressor.removeByInput(IIngredient, GasStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.osmiumcompressor.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.osmiumcompressor.removeByInput(ore('dustRefinedObsidian'), gas('liquidosmium'))
    mods.mekanism.osmiumcompressor.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.osmiumcompressor.streamRecipes()
    ```
