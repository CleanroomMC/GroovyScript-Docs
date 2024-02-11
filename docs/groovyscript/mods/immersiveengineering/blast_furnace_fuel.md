---
title: "Blast Furnace Fuel"
description: "Allows an item to be used in the Blast Furnace as a fuel for the given number of ticks."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/BlastFurnaceFuel.java"
---

# Blast Furnace Fuel (Immersive Engineering)

## Description

Allows an item to be used in the Blast Furnace as a fuel for the given number of ticks.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.ie.blast_furnace_fuel
mods.ie.blastfurnacefuel
mods.ie.blastFurnaceFuel
mods.ie.BlastFurnaceFuel
mods.immersiveengineering.blast_furnace_fuel/*(1)!*/
mods.immersiveengineering.blastfurnacefuel
mods.immersiveengineering.blastFurnaceFuel
mods.immersiveengineering.BlastFurnaceFuel
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `time`:

    ```groovy
    mods.immersiveengineering.blast_furnace_fuel.add(IIngredient, int)
    ```


### Recipe Builder

Just like other recipe types, the Blast Furnace Fuel also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.blast_furnace_fuel.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy int`. Sets the time in ticks the recipe takes to process. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        time(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.BlastFurnaceRecipe$BlastFurnaceFuel`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.blast_furnace_fuel.recipeBuilder()
            .input(item('minecraft:clay'))
            .time(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.blast_furnace_fuel.removeByInput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.blast_furnace_fuel.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.blast_furnace_fuel.removeByInput(item('immersiveengineering:material:6'))
    mods.immersiveengineering.blast_furnace_fuel.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.blast_furnace_fuel.streamRecipes()
    ```
