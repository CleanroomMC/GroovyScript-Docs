---
title: "Coke Oven"
description: "Converts an input itemstack into an output itemstack over time, producing a given amount of creosote oil."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/CokeOven.java"
---

# Coke Oven (Immersive Engineering)

## Description

Converts an input itemstack into an output itemstack over time, producing a given amount of creosote oil.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="6"
mods.ie.CokeOven
mods.ie.cokeoven
mods.ie.cokeOven
mods.ie.coke_oven
mods.immersiveengineering.CokeOven
mods.immersiveengineering.cokeoven/*(1)!*/
mods.immersiveengineering.cokeOven
mods.immersiveengineering.coke_oven
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `time`, `creosoteOutput`:

    ```groovy
    mods.immersiveengineering.cokeoven.add(ItemStack, IIngredient, int, int)
    ```


### Recipe Builder

Just like other recipe types, the Coke Oven also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.cokeoven.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. Sets the time in ticks the recipe takes to process. Requires greater than or equal to 0.

        ```groovy
        time(int)
        ```

    - `#!groovy int`. Sets the amount of Creosote Oil output. Requires greater than or equal to 0.

        ```groovy
        creosote(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.CokeOvenRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.cokeoven.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay'))
            .time(100)
            .creosote(50)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.cokeoven.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.cokeoven.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.cokeoven.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.cokeoven.removeByInput(item('minecraft:log'))
    mods.immersiveengineering.cokeoven.removeByOutput(item('immersiveengineering:material:6'))
    mods.immersiveengineering.cokeoven.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.cokeoven.streamRecipes()
    ```
