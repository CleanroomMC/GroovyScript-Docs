---
title: "Fermenter"
description: "Converts an input itemstack into an output fluidstack with an optional output itemstack, consuming power."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/Fermenter.java"
---

# Fermenter (Immersive Engineering)

## Description

Converts an input itemstack into an output fluidstack with an optional output itemstack, consuming power.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="4"
mods.ie.Fermenter
mods.ie.fermenter
mods.immersiveengineering.Fermenter
mods.immersiveengineering.fermenter/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `fluidOutput`, `itemOutput`, `input`, `energy`:

    ```groovy
    mods.immersiveengineering.fermenter.add(FluidStack, ItemStack, IIngredient, int)
    ```


### Recipe Builder

Just like other recipe types, the Fermenter also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.fermenter.recipeBuilder()"
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

    - `#!groovy FluidStackList`. Sets the fluid outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        fluidOutput(FluidStack)
        fluidOutput(FluidStack...)
        fluidOutput(Collection<FluidStack>)
        ```

    - `#!groovy int`. Sets the amount of power consumed to complete the recipe.

        ```groovy
        energy(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.FermenterRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.fermenter.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay'))
            .fluidOutput(fluid('water'))
            .energy(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.fermenter.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.fermenter.removeByOutput(FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.fermenter.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.fermenter.removeByInput(item('minecraft:reeds'))
    mods.immersiveengineering.fermenter.removeByOutput(fluid('ethanol'))
    mods.immersiveengineering.fermenter.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.fermenter.streamRecipes()
    ```
