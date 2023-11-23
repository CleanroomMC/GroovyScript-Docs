---
title: "Crystallizer"
description: "Converts an input gasstack into an output itemstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/Crystallizer.java"
---

# Crystallizer (Mekanism)

## Description

Converts an input gasstack into an output itemstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.Crystallizer
mods.mekanism.crystallizer/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `output`:

    ```groovy
    mods.mekanism.crystallizer.add(GasStack, ItemStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.crystallizer.add(gas('cleanGold'), item('minecraft:gold_ingot'))
    ```

### Recipe Builder

Just like other recipe types, the Crystallizer also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.crystallizer.recipeBuilder()"
    - `#!groovy GasStackList`. Sets the gas inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        gasInput(GasStack)
        gasInput(GasStack...)
        gasInput(Collection<GasStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.CrystallizerRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.crystallizer.recipeBuilder()
            .gasInput(gas('cleanGold'))
            .output(item('minecraft:gold_ingot'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.crystallizer.removeByInput(GasStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.crystallizer.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.crystallizer.removeByInput(gas('cleanGold'))
    mods.mekanism.crystallizer.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.crystallizer.streamRecipes()
    ```
