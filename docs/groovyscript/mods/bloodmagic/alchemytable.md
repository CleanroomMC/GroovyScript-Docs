---
title: "Alchemy Table"
description: "Converts up to 6 input items into an output itemstack, with configurable time, minimum tier of Blood Orb required, and Life Essence drained from the Orb network."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/bloodmagic/AlchemyTable.java"
---

# Alchemy Table (Blood Magic: Alchemical Wizardry)

## Description

Converts up to 6 input items into an output itemstack, with configurable time, minimum tier of Blood Orb required, and Life Essence drained from the Orb network.

!!! Danger ""
    Tier 6 must be enabled in the config to use an Orb of that tier in the Alchemy Table.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="6"
mods.bm.AlchemyTable
mods.bm.alchemytable
mods.bm.alchemyTable
mods.bm.alchemy_table
mods.bloodmagic.AlchemyTable
mods.bloodmagic.alchemytable/*(1)!*/
mods.bloodmagic.alchemyTable
mods.bloodmagic.alchemy_table
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `output`, `syphon`, `ticks`, `minimumTier`:

    ```groovy
    mods.bloodmagic.alchemytable.add(NonNullList<Ingredient>, ItemStack, int, int, int)
    ```


### Recipe Builder

Just like other recipe types, the Alchemy Table also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.bloodmagic.alchemytable.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to 6. (Default `null`).

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

    - `#!groovy int`. Sets how long in ticks the recipe should take. Requires greater than 0.

        ```groovy
        time(int)
        ticks(int)
        ```

    - `#!groovy int`. Sets how much Life Essence is drained from the Blood Network. Requires greater than or equal to 0.

        ```groovy
        drain(int)
        syphon(int)
        ```

    - `#!groovy int`. Sets the minimum tier the Blood Orb inside the table must be. Requires greater than or equal to 0 and less than AltarTier.MAXTIERS.

        ```groovy
        tier(int)
        minimumTier(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `WayofTime.bloodmagic.api.impl.recipe.RecipeAlchemyTable`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.bloodmagic.alchemytable.recipeBuilder()
            .input(item('minecraft:diamond'), item('minecraft:diamond'))
            .output(item('minecraft:clay'))
            .ticks(100)
            .minimumTier(2)
            .syphon(500)
            .register()

        mods.bloodmagic.alchemytable.recipeBuilder()
            .input(item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('bloodmagic:slate'), item('bloodmagic:slate'))
            .output(item('minecraft:clay'))
            .time(2000)
            .tier(5)
            .drain(25000)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.bloodmagic.alchemytable.removeByInput(NonNullList<IIngredient>)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.bloodmagic.alchemytable.removeByInput(IIngredient...)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.bloodmagic.alchemytable.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.bloodmagic.alchemytable.removeAll()
    ```

???+ Example
    ```groovy
    mods.bloodmagic.alchemytable.removeByInput(item('minecraft:nether_wart'), item('minecraft:gunpowder'))
    mods.bloodmagic.alchemytable.removeByOutput(item('minecraft:sand'))
    mods.bloodmagic.alchemytable.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.bloodmagic.alchemytable.streamRecipes()
    ```
