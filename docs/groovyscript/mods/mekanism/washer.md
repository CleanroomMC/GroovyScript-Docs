---
title: "Washer"
description: "Converts an input gasstack into an output gasstack at the cost of 5mb of water."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/Washer.java"
---

# Washer (Mekanism)

## Description

Converts an input gasstack into an output gasstack at the cost of 5mb of water.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.mekanism.washer/*(1)!*/
mods.mekanism.Washer
mods.mekanism.chemical_washer
mods.mekanism.chemicalwasher
mods.mekanism.chemicalWasher
mods.mekanism.ChemicalWasher
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `output`:

    ```groovy
    mods.mekanism.washer.add(GasStack, GasStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.washer.add(gas('water'), gas('hydrogen'))
    ```

### Recipe Builder

Just like other recipe types, the Washer also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.washer.recipeBuilder()"
    - `#!groovy GasStackList`. Sets the gas inputs of the recipe. Requires exactly 1.

        ```groovy
        gasInput(GasStack)
        gasInput(GasStack...)
        gasInput(Collection<GasStack>)
        ```

    - `#!groovy GasStackList`. Sets the gas outputs of the recipe. Requires exactly 1.

        ```groovy
        gasOutput(GasStack)
        gasOutput(GasStack...)
        gasOutput(Collection<GasStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.WasherRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.washer.recipeBuilder()
            .gasInput(gas('water') * 10)
            .gasOutput(gas('hydrogen') * 20)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.washer.removeByInput(GasStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.washer.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.washer.removeByInput(gas('iron'))
    mods.mekanism.washer.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.washer.streamRecipes()
    ```
