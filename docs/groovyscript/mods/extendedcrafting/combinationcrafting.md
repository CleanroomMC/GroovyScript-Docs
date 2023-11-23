---
title: "Combination Crafting"
description: "Converts one main item and any number of additional items into an output itemstack, with a configurable rf cost and consumption per tick amount."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/extendedcrafting/CombinationCrafting.java"
---

# Combination Crafting (Extended Crafting)

## Description

Converts one main item and any number of additional items into an output itemstack, with a configurable rf cost and consumption per tick amount.

!!! Info
    By default, there are no Combination recipes

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.extendedcrafting.CombinationCrafting
mods.extendedcrafting.combinationcrafting/*(1)!*/
mods.extendedcrafting.combinationCrafting
mods.extendedcrafting.combination_crafting
mods.extendedcrafting.Combination
mods.extendedcrafting.combination
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `cost`, `perTick`, `input`, `pedestals`:

    ```groovy
    mods.extendedcrafting.combinationcrafting.add(ItemStack, long, int, Ingredient, NonNullList<Ingredient>)
    ```

- Adds recipes in the format `output`, `cost`, `input`, `pedestals`:

    ```groovy
    mods.extendedcrafting.combinationcrafting.add(ItemStack, long, Ingredient, NonNullList<Ingredient>)
    ```


### Recipe Builder

Just like other recipe types, the Combination Crafting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.extendedcrafting.combinationcrafting.recipeBuilder()"
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

    - `#!groovy long`. Sets the amount of RF required to complete the craft. Requires greater than or equal to 0.

        ```groovy
        cost(long)
        totalCost(long)
        ```

    - `#!groovy int`. Sets the maximum amount of RF consumed per tick until the entire cost is paid. Requires greater than or equal to 0.

        ```groovy
        perTick(int)
        costPerTick(int)
        ```

    - `#!groovy NonNullList<IIngredient>`. Sets the required items on nearby pedestals. (Default `null`).

        ```groovy
        pedestals(IIngredient)
        pedestals(IIngredient...)
        pedestals(Collection<IIngredient>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.blakebr0.extendedcrafting.crafting.CombinationRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.extendedcrafting.combinationcrafting.recipeBuilder()
            .input(item('minecraft:pumpkin'))
            .pedestals(item('minecraft:pumpkin') * 8)
            .output(item('minecraft:diamond') * 2)
            .cost(100)
            .perTick(100)
            .register()

        mods.extendedcrafting.combinationcrafting.recipeBuilder()
            .input(item('minecraft:pumpkin'))
            .pedestals(item('minecraft:pumpkin'), item('minecraft:clay'), item('minecraft:clay'), item('minecraft:pumpkin'))
            .output(item('minecraft:gold_ingot') * 2)
            .cost(10000)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.extendedcrafting.combinationcrafting.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.extendedcrafting.combinationcrafting.removeByInput(IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.extendedcrafting.combinationcrafting.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.extendedcrafting.combinationcrafting.removeAll()
    ```

???+ Example
    ```groovy
    mods.extendedcrafting.combinationcrafting.removeByInput(item('minecraft:pumpkin'))
    mods.extendedcrafting.combinationcrafting.removeByOutput(item('minecraft:gold_ingot'))
    mods.extendedcrafting.combinationcrafting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.extendedcrafting.combinationcrafting.streamRecipes()
    ```
