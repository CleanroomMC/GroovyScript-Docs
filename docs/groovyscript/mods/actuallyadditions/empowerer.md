---
title: "Empowerer"
description: "Turns 5 input items into an output item at the cost of power and time. Has a configurable color."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/actuallyadditions/Empowerer.java"
---

# Empowerer (Actually Additions)

## Description

Turns 5 input items into an output item at the cost of power and time. Has a configurable color.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="3"
mods.aa.empowerer
mods.aa.Empowerer
mods.actuallyadditions.empowerer/*(1)!*/
mods.actuallyadditions.Empowerer
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Empowerer also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.actuallyadditions.empowerer.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 4 and less than or equal to 5.

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

    - `#!groovy float`. Sets the red color. Requires greater than or equal to 0 and less than or equal to 1. (Default `0.0f`).

        ```groovy
        red(float)
        color(int)
        color(float...)
        particleColor(int)
        particleColor(float...)
        ```

    - `#!groovy float`. Sets the blue color. Requires greater than or equal to 0 and less than or equal to 1. (Default `0.0f`).

        ```groovy
        blue(float)
        color(int)
        color(float...)
        particleColor(int)
        particleColor(float...)
        ```

    - `#!groovy int`. Sets the amount of time the recipe takes to complete. Requires greater than 0. (Default `0`).

        ```groovy
        time(int)
        ```

    - `#!groovy float`. Sets the green color. Requires greater than or equal to 0 and less than or equal to 1. (Default `0.0f`).

        ```groovy
        green(float)
        color(int)
        color(float...)
        particleColor(int)
        particleColor(float...)
        ```

    - `#!groovy IIngredient`. Sets the center IIngredient if the input only has 4 entries.

        ```groovy
        mainInput(IIngredient)
        ```

    - `#!groovy int`. Sets the amount of energy each stand must consume to process the recipe. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        energy(int)
        energyPerStand(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `de.ellpeck.actuallyadditions.api.recipe.EmpowererRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.actuallyadditions.empowerer.recipeBuilder()
            .mainInput(item('minecraft:clay'))
            .input(item('minecraft:clay'),item('minecraft:clay'),item('minecraft:clay'),item('minecraft:clay'))
            .output(item('minecraft:diamond'))
            .time(50)
            .energy(1000)
            .red(0.5)
            .green(0.3)
            .blue(0.2)
            .register()

        mods.actuallyadditions.empowerer.recipeBuilder()
            .mainInput(item('minecraft:clay'))
            .input(item('minecraft:diamond'),item('minecraft:clay'),item('minecraft:clay'),item('minecraft:clay'))
            .output(item('minecraft:diamond') * 2)
            .time(50)
            .color(0.5, 0.3, 0.2)
            .register()

        mods.actuallyadditions.empowerer.recipeBuilder()
            .mainInput(item('minecraft:diamond'))
            .input(item('minecraft:diamond'),item('minecraft:gold_ingot'),item('minecraft:diamond'),item('minecraft:gold_ingot'))
            .output(item('minecraft:dirt') * 8)
            .time(50)
            .particleColor(0x00FF88)
            .register()

        mods.actuallyadditions.empowerer.recipeBuilder()
            .input(item('minecraft:gold_ingot'),item('minecraft:clay'),item('minecraft:clay'),item('minecraft:clay'),item('minecraft:clay'))
            .output(item('minecraft:diamond'))
            .time(50)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.actuallyadditions.empowerer.removeByInput(IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.actuallyadditions.empowerer.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.actuallyadditions.empowerer.removeAll()
    ```

???+ Example
    ```groovy
    mods.actuallyadditions.empowerer.removeByInput(item('actuallyadditions:item_crystal'))
    mods.actuallyadditions.empowerer.removeByOutput(item('actuallyadditions:item_misc:24'))
    mods.actuallyadditions.empowerer.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.actuallyadditions.empowerer.streamRecipes()
    ```
