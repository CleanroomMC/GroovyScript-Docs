---
title: "Lightwell"
description: "Converts an input item into fluid, with a chance at breaking every time fluid is produced. The amount of fluid produced per interval can be increased via starlight."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/Lightwell.java"
---

# Lightwell (Astral Sorcery)

## Description

Converts an input item into fluid, with a chance at breaking every time fluid is produced. The amount of fluid produced per interval can be increased via starlight.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="8"
mods.astral.Lightwell
mods.astral.lightwell
mods.astral_sorcery.Lightwell
mods.astral_sorcery.lightwell
mods.as.Lightwell
mods.as.lightwell
mods.astralsorcery.Lightwell
mods.astralsorcery.lightwell/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `catalyst`, `output`, `productionMultiplier`, `shatterMultiplier`:

    ```groovy
    mods.astralsorcery.lightwell.add(ItemStack, Fluid, float, float)
    ```

- Adds recipes in the format `catalyst`, `output`, `productionMultiplier`, `shatterMultiplier`, `color`:

    ```groovy
    mods.astralsorcery.lightwell.add(ItemStack, Fluid, float, float, Color)
    ```


### Recipe Builder

Just like other recipe types, the Lightwell also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.astralsorcery.lightwell.recipeBuilder()"
    - `#!groovy Color`. Sets the color of the produced particles. (Default `null`).

        ```groovy
        catalystColor(int)
        catalystColor(Color)
        catalystColor(int, int, int)
        catalystColor(int, int, int, int)
        ```

    - `#!groovy Fluid`. Sets the output fluid. Requires not null. (Default `null`).

        ```groovy
        output(FluidStack)
        ```

    - `#!groovy ItemStack`. Sets the input item. Requires not null. (Default `null`).

        ```groovy
        catalyst(ItemStack)
        ```

    - `#!groovy float`. Sets how likely the catalyst is to shatter when producing fluid, with higher being less likely but never 0. Requires greater than or equal to 0.

        ```groovy
        shatterMultiplier(float)
        ```

    - `#!groovy float`. Sets the base amount of fluid produced per tick. Requires greater than or equal to 0.

        ```groovy
        productionMultiplier(float)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `hellfirepvp.astralsorcery.common.base.WellLiquefaction$LiquefactionEntry`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.lightwell.recipeBuilder()
            .catalyst(item('minecraft:stone'))
            .output(fluid('astralsorcery.liquidstarlight'))
            .productionMultiplier(1.0F)
            .shatterMultiplier(15.0F)
            .catalystColor(16725260)
            .register()

        mods.astralsorcery.lightwell.recipeBuilder()
            .catalyst(item('minecraft:obsidian'))
            .output(fluid('astralsorcery.liquidstarlight'))
            .productionMultiplier(1.0F)
            .shatterMultiplier(15.0F)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given catalyst:

    ```groovy
    mods.astralsorcery.lightwell.removeByCatalyst(ItemStack)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.lightwell.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.astralsorcery.lightwell.removeByOutput(FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.lightwell.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.lightwell.removeByCatalyst(item('minecraft:ice'))
    mods.astralsorcery.lightwell.removeByInput(item('minecraft:packed_ice'))
    mods.astralsorcery.lightwell.removeByOutput(fluid('lava'))
    mods.astralsorcery.lightwell.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.lightwell.streamRecipes()
    ```
