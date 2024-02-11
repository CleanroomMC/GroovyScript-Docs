---
title: "Compressor"
description: "Converts any number of a single item into an output itemstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/avaritia/Compressor.java"
---

# Compressor (Avaritia)

## Description

Converts any number of a single item into an output itemstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.avaritia.compressor/*(1)!*/
mods.avaritia.Compressor
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `cost`:

    ```groovy
    mods.avaritia.compressor.add(ItemStack, IIngredient, int)
    ```

???+ Example
    ```groovy
    mods.avaritia.compressor.add(item('minecraft:nether_star'), item('minecraft:clay_ball'), 100)
    ```

### Recipe Builder

Just like other recipe types, the Compressor also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.avaritia.compressor.recipeBuilder()"
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

    - `#!groovy int`. Sets the amount of items required to convert. (Default `300`).

        ```groovy
        input(IIngredient)
        inputCount(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `morph.avaritia.recipe.compressor.ICompressorRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.avaritia.compressor.recipeBuilder()
            .input(item('minecraft:clay_ball') * 100)
            .output(item('minecraft:nether_star'))
            .inputCount(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.avaritia.compressor.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.avaritia.compressor.removeAll()
    ```

???+ Example
    ```groovy
    mods.avaritia.compressor.removeByOutput(item('avaritia:singularity', 0))
    mods.avaritia.compressor.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.avaritia.compressor.streamRecipes()
    ```
