---
title: "Injection Chamber"
description: "Converts an input itemstack and 200 of a gasstack into an output itemstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/InjectionChamber.java"
---

# Injection Chamber (Mekanism)

## Description

Converts an input itemstack and 200 of a gasstack into an output itemstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.InjectionChamber
mods.mekanism.injectionchamber/*(1)!*/
mods.mekanism.injectionChamber
mods.mekanism.injection_chamber
mods.mekanism.Injector
mods.mekanism.injector
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `ingredient`, `gasInput`, `output`:

    ```groovy
    mods.mekanism.injectionchamber.add(IIngredient, GasStack, ItemStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.injectionchamber.add(item('minecraft:diamond'), gas('water'), item('minecraft:nether_star'))
    ```

### Recipe Builder

Just like other recipe types, the Injection Chamber also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.injectionchamber.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

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

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.InjectionRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.injectionchamber.recipeBuilder()
            .input(item('minecraft:diamond'))
            .gasInput(gas('water'))/*(1)!*/
            .output(item('minecraft:nether_star'))
            .register()
        ```

        1. Always uses 200 gas



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.injectionchamber.removeByInput(IIngredient, GasStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.injectionchamber.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.injectionchamber.removeByInput(item('minecraft:hardened_clay'), gas('water'))
    mods.mekanism.injectionchamber.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.injectionchamber.streamRecipes()
    ```
