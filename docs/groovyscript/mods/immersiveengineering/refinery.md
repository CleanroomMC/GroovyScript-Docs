---
title: "Refinery"
description: "Converts 2 input fluidstacks into an output fluidstack, consuming power."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/Refinery.java"
---

# Refinery (Immersive Engineering)

## Description

Converts 2 input fluidstacks into an output fluidstack, consuming power.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="4"
mods.ie.Refinery
mods.ie.refinery
mods.immersiveengineering.Refinery
mods.immersiveengineering.refinery/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input0`, `input1`, `energy`:

    ```groovy
    mods.immersiveengineering.refinery.add(FluidStack, FluidStack, FluidStack, int)
    ```


### Recipe Builder

Just like other recipe types, the Refinery also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.refinery.recipeBuilder()"
    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 2. (Default `null`).

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
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

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.refinery.recipeBuilder()
            .fluidInput(fluid('water'), fluid('water'))
            .fluidOutput(fluid('lava'))
            .energy(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.refinery.removeByInput(FluidStack, FluidStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.refinery.removeByOutput(FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.refinery.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.refinery.removeByInput(fluid('plantoil'), fluid('ethanol'))
    mods.immersiveengineering.refinery.removeByOutput(fluid('biodiesel'))
    mods.immersiveengineering.refinery.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.refinery.streamRecipes()
    ```
