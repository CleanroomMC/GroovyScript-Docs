---
title: "Squeezer"
description: "Converts an input itemstack into either an output itemstack, fluidstack, or both, using energy."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/Squeezer.java"
---

# Squeezer (Immersive Engineering)

## Description

Converts an input itemstack into either an output itemstack, fluidstack, or both, using energy.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="4"
mods.ie.Squeezer
mods.ie.squeezer
mods.immersiveengineering.Squeezer
mods.immersiveengineering.squeezer/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `fluidOutput`, `itemOutput`, `input`, `energy`:

    ```groovy
    mods.immersiveengineering.squeezer.add(FluidStack, ItemStack, IIngredient, int)
    ```


### Recipe Builder

Just like other recipe types, the Squeezer also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.squeezer.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 0 and less than or equal to 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid outputs of the recipe. Requires greater than or equal to 0 and less than or equal to 1. (Default `null`).

        ```groovy
        fluidOutput(FluidStack)
        fluidOutput(FluidStack...)
        fluidOutput(Collection<FluidStack>)
        ```

    - `#!groovy int`. Sets the amount of power consumed to complete the recipe.

        ```groovy
        energy(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.squeezer.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay'))
            .fluidOutput(fluid('lava'))
            .energy(100)
            .register()

        mods.immersiveengineering.squeezer.recipeBuilder()
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:clay'))
            .energy(100)
            .register()

        mods.immersiveengineering.squeezer.recipeBuilder()
            .input(item('minecraft:clay'))
            .fluidOutput(fluid('water'))
            .energy(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.squeezer.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.squeezer.removeByOutput(FluidStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.squeezer.removeByOutput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.squeezer.removeByOutput(FluidStack, ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.squeezer.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.squeezer.removeByInput(item('minecraft:wheat_seeds'))
    mods.immersiveengineering.squeezer.removeByOutput(fluid('plantoil'))
    mods.immersiveengineering.squeezer.removeByOutput(item('immersiveengineering:material:18'))
    mods.immersiveengineering.squeezer.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.squeezer.streamRecipes()
    ```
