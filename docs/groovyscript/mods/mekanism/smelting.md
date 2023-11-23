---
title: "Smelting"
description: "Converts an input itemstack into an output itemstack in a recipe exclusive to the Smelter. Overrides the default furnace recipe, if applicable."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/Smelting.java"
---

# Smelting (Mekanism)

## Description

Converts an input itemstack into an output itemstack in a recipe exclusive to the Smelter. Overrides the default furnace recipe, if applicable.

!!! Danger ""
    Recipes exclusive to the Mekanism Smelter may not be displayed in JEI

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.Smelting
mods.mekanism.smelting/*(1)!*/
mods.mekanism.Smelter
mods.mekanism.smelter
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `ingredient`, `output`:

    ```groovy
    mods.mekanism.smelting.add(IIngredient, ItemStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.smelting.add(item('minecraft:diamond_block'), item('minecraft:clay'))
    ```

### Recipe Builder

Just like other recipe types, the Smelting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.smelting.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

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

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.SmeltingRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.smelting.recipeBuilder()
            .input(item('minecraft:clay_ball'))
            .output(item('minecraft:clay'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.smelting.removeByInput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.smelting.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.smelting.removeByInput(item('minecraft:clay'))
    mods.mekanism.smelting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.smelting.streamRecipes()
    ```
