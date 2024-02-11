---
title: "Blood Altar"
description: "Converts an input item into an output itemstack, draining life essence from the altar at a base rate and requiring at least a specific tier."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/bloodmagic/BloodAltar.java"
---

# Blood Altar (Blood Magic: Alchemical Wizardry)

## Description

Converts an input item into an output itemstack, draining life essence from the altar at a base rate and requiring at least a specific tier.

???+ Note
    The Blood Altar consumes Life Essence from its internal tank to convert the input item into the output item. Each tier requires a larger multiblock, which may contain Runes that modify the Blood Altar's functionality.

!!! Danger ""
    Tier 6 must be enabled in the config to use a Blood Altar of that tier.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.bm.blood_altar
mods.bm.bloodaltar
mods.bm.bloodAltar
mods.bm.BloodAltar
mods.bloodmagic.blood_altar/*(1)!*/
mods.bloodmagic.bloodaltar
mods.bloodmagic.bloodAltar
mods.bloodmagic.BloodAltar
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `output`, `minimumTier`, `syphon`, `consumeRate`, `drainRate`:

    ```groovy
    mods.bloodmagic.blood_altar.add(Ingredient, ItemStack, int, int, int, int)
    ```


### Recipe Builder

Just like other recipe types, the Blood Altar also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.bloodmagic.blood_altar.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. Sets how much Life Essence in total is required. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        syphon(int)
        ```

    - `#!groovy int`. Sets how much Life Essence the recipe looses per tick when the recipe cannot consume Life Essence. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        drainRate(int)
        ```

    - `#!groovy int`. Sets how much Life Essence the Blood Altar can consume per tick for this recipe. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        consumeRate(int)
        ```

    - `#!groovy int`. Sets the minimum tier required from the altar. Requires greater than or equal to 0 and less than AltarTier.MAXTIERS. (Default `0`).

        ```groovy
        tier(int)
        minimumTier(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `WayofTime.bloodmagic.api.impl.recipe.RecipeBloodAltar`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.bloodmagic.blood_altar.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:gold_ingot'))
            .minimumTier(0)
            .drainRate(5)
            .syphon(10)
            .consumeRate(5)
            .register()

        mods.bloodmagic.blood_altar.recipeBuilder()
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:diamond'))
            .tier(3)
            .drainRate(100)
            .syphon(50000)
            .consumeRate(500)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.bloodmagic.blood_altar.removeByInput(IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.bloodmagic.blood_altar.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.bloodmagic.blood_altar.removeAll()
    ```

???+ Example
    ```groovy
    mods.bloodmagic.blood_altar.removeByInput(item('minecraft:ender_pearl'))
    mods.bloodmagic.blood_altar.removeByOutput(item('bloodmagic:slate:4'))
    mods.bloodmagic.blood_altar.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.bloodmagic.blood_altar.streamRecipes()
    ```
