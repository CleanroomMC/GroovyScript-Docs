---
title: "Blast Furnace"
description: "Converts an input itemstack into an output itemstack and an optional 'slag' itemstack, taking time and consuming fuel (based on Blast Furnace Fuels)."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/BlastFurnace.java"
---

# Blast Furnace (Immersive Engineering)

## Description

Converts an input itemstack into an output itemstack and an optional 'slag' itemstack, taking time and consuming fuel (based on Blast Furnace Fuels).

## Identifier

Refer to this via any of the following:

```groovy hl_lines="6"
mods.ie.BlastFurnace
mods.ie.blastfurnace
mods.ie.blastFurnace
mods.ie.blast_furnace
mods.immersiveengineering.BlastFurnace
mods.immersiveengineering.blastfurnace/*(1)!*/
mods.immersiveengineering.blastFurnace
mods.immersiveengineering.blast_furnace
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `time`, `slag`:

    ```groovy
    mods.immersiveengineering.blastfurnace.add(ItemStack, IIngredient, int, ItemStack)
    ```


### Recipe Builder

Just like other recipe types, the Blast Furnace also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.blastfurnace.recipeBuilder()"
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

    - `#!groovy ItemStack`. Sets the item output as slag.

        ```groovy
        slag(ItemStack)
        ```

    - `#!groovy int`. Sets the time in ticks the recipe takes to process. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        time(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.BlastFurnaceRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.blastfurnace.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay'))
            .time(100)
            .slag(item('minecraft:gold_nugget'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.blastfurnace.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.blastfurnace.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.blastfurnace.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.blastfurnace.removeByInput(item('minecraft:iron_block'))
    mods.immersiveengineering.blastfurnace.removeByOutput(item('immersiveengineering:metal:8'))
    mods.immersiveengineering.blastfurnace.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.blastfurnace.streamRecipes()
    ```
