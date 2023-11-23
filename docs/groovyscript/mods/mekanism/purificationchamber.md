---
title: "Purification Chamber"
description: "Converts an input itemstack and gasstack into an output itemstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/PurificationChamber.java"
---

# Purification Chamber (Mekanism)

## Description

Converts an input itemstack and gasstack into an output itemstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.PurificationChamber
mods.mekanism.purificationchamber/*(1)!*/
mods.mekanism.purificationChamber
mods.mekanism.purification_chamber
mods.mekanism.Purifier
mods.mekanism.purifier
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `ingredient`, `gasInput`, `output`:

    ```groovy
    mods.mekanism.purificationchamber.add(IIngredient, GasStack, ItemStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.purificationchamber.add(item('minecraft:diamond'), gas('oxygen'), item('minecraft:nether_star'))
    ```

### Recipe Builder

Just like other recipe types, the Purification Chamber also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.purificationchamber.recipeBuilder()"
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

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.PurificationRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.purificationchamber.recipeBuilder()
            .input(item('minecraft:diamond'))
            .gasInput(gas('deuterium'))
            .output(item('minecraft:nether_star'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.purificationchamber.removeByInput(IIngredient, GasStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.purificationchamber.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.purificationchamber.removeByInput(item('mekanism:oreblock:0'), gas('oxygen'))
    mods.mekanism.purificationchamber.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.purificationchamber.streamRecipes()
    ```