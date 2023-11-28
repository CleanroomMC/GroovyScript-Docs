---
title: "Mana Infusion"
description: "Toss an item into a mana pool with an optional catalyst blockstate below the pool."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/ManaInfusion.java"
---

# Mana Infusion (Botania)

## Description

Toss an item into a mana pool with an optional catalyst blockstate below the pool.

???+ Warning
    A mana cost greater than 10,000 cannot be converted in a Diluted Mana Pools and a mana cost greater than 1,000,000 cannot be converted in a normal Mana Pool. Both the Fabulous Mana Pool and The Everlasting Guilty Pool have the same capacity as a normal Mana Pool.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.ManaInfusion
mods.botania.manainfusion/*(1)!*/
mods.botania.manaInfusion
mods.botania.mana_infusion
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `mana`:

    ```groovy
    mods.botania.manainfusion.add(ItemStack, IIngredient, int)
    ```


### Recipe Builder

Just like other recipe types, the Mana Infusion also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.botania.manainfusion.recipeBuilder()"
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

    - `#!groovy int`. Sets the mana cost of converting the item. Requires greater than or equal to 1. (Default `100`).

        ```groovy
        mana(int)
        ```

    - `#!groovy IBlockState`. Sets the IBlockState required below the mana pool.

        ```groovy
        catalyst(IBlockState)
        useAlchemy()
        useConjuration()
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `vazkii.botania.api.recipe.RecipeManaInfusion`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.botania.manainfusion.recipeBuilder()
            .input(ore('ingotGold'))
            .output(item('botania:manaresource', 1))
            .mana(500)
            .catalyst(blockstate('minecraft:stone'))
            .register()
        ```



## Removing Recipes

- Removes all recipes with the given IBlockState catalyst:

    ```groovy
    mods.botania.manainfusion.removeByCatalyst(IBlockState)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.manainfusion.removeByInput(IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.manainfusion.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.manainfusion.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.manainfusion.removeByCatalyst(blockstate('botania:alchemycatalyst'))
    mods.botania.manainfusion.removeByInput(item('minecraft:ender_pearl'))
    mods.botania.manainfusion.removeByOutput(item('botania:managlass'))
    mods.botania.manainfusion.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.manainfusion.streamRecipes()
    ```
