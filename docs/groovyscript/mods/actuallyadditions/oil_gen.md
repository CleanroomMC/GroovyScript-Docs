---
title: "Oil Gen"
description: "Turns a fluid into power at a rate."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/actuallyadditions/OilGen.java"
---

# Oil Gen (Actually Additions)

## Description

Turns a fluid into power at a rate.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.aa.oil_gen
mods.aa.oilgen
mods.aa.oilGen
mods.aa.OilGen
mods.actuallyadditions.oil_gen/*(1)!*/
mods.actuallyadditions.oilgen
mods.actuallyadditions.oilGen
mods.actuallyadditions.OilGen
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Oil Gen also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.actuallyadditions.oil_gen.recipeBuilder()"
    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 1.

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy int`. Sets how long the fluid burns for. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        time(int)
        ```

    - `#!groovy int`. Sets how much power is generated per tick while fluid is being consumed. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        amount(int)
        fluidInput(FluidStack)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `de.ellpeck.actuallyadditions.api.recipe.OilGenRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.actuallyadditions.oil_gen.recipeBuilder()
            .fluidInput(fluid('water'))
            .amount(1000)
            .time(50)
            .register()

        mods.actuallyadditions.oil_gen.recipeBuilder()
            .fluidInput(fluid('lava') * 50)
            .time(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.actuallyadditions.oil_gen.removeByInput(Fluid)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.actuallyadditions.oil_gen.removeByInput(FluidStack)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.actuallyadditions.oil_gen.removeByInput(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.actuallyadditions.oil_gen.removeAll()
    ```

???+ Example
    ```groovy
    mods.actuallyadditions.oil_gen.removeByInput(fluid('canolaoil').getFluid())
    mods.actuallyadditions.oil_gen.removeByInput(fluid('canolaoil'))
    mods.actuallyadditions.oil_gen.removeByInput('refinedcanolaoil')
    mods.actuallyadditions.oil_gen.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.actuallyadditions.oil_gen.streamRecipes()
    ```
