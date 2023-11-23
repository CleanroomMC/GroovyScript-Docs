---
title: "Electrolytic Separator"
description: "Converts an input fluid into two output gasstacks at the cost of power."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/ElectrolyticSeparator.java"
---

# Electrolytic Separator (Mekanism)

## Description

Converts an input fluid into two output gasstacks at the cost of power.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.ElectrolyticSeparator
mods.mekanism.electrolyticseparator/*(1)!*/
mods.mekanism.electrolyticSeparator
mods.mekanism.electrolytic_separator
mods.mekanism.Separator
mods.mekanism.separator
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `leftOutput`, `rightOutput`, `energy`:

    ```groovy
    mods.mekanism.electrolyticseparator.add(FluidStack, GasStack, GasStack, double)
    ```

???+ Example
    ```groovy
    mods.mekanism.electrolyticseparator.add(fluid('lava') * 10, gas('cleanGold') * 5, gas('cleanCopper') * 3, 3000)
    ```

### Recipe Builder

Just like other recipe types, the Electrolytic Separator also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.electrolyticseparator.recipeBuilder()"
    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy GasStackList`. Sets the gas outputs of the recipe. Requires exactly 2. (Default `null`).

        ```groovy
        gasOutput(GasStack)
        gasOutput(GasStack...)
        gasOutput(Collection<GasStack>)
        ```

    - `#!groovy double`. Sets the energy cost of the recipe. Requires greater than 0.

        ```groovy
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.electrolyticseparator.recipeBuilder()
            .fluidInput(fluid('lava') * 10)
            .gasOutput(gas('cleanGold') * 5, gas('cleanCopper') * 3)
            .energy(3000)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.electrolyticseparator.removeByInput(FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.electrolyticseparator.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.electrolyticseparator.removeByInput(fluid('water'))
    mods.mekanism.electrolyticseparator.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.electrolyticseparator.streamRecipes()
    ```
