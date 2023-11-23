---
title: "Sag Mill"
description: "Convert an input itemstack into up to 4 output itemstacks with chances, using energy. Output can be boosted by Grinding Balls based on set bonusType. Can be set to require at least SIMPLE, NORMAL, or ENHANCED tiers, or to IGNORE the tier. SIMPLE and IGNORE are effectively the same."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/enderio/SagMill.java"
---

# Sag Mill (Ender IO)

## Description

Convert an input itemstack into up to 4 output itemstacks with chances, using energy. Output can be boosted by Grinding Balls based on set bonusType. Can be set to require at least SIMPLE, NORMAL, or ENHANCED tiers, or to IGNORE the tier. SIMPLE and IGNORE are effectively the same.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.enderio.SagMill
mods.enderio.sagmill/*(1)!*/
mods.enderio.sagMill
mods.enderio.sag_mill
mods.enderio.Sag
mods.enderio.sag
mods.enderio.SAGMill
mods.eio.SagMill
mods.eio.sagmill
mods.eio.sagMill
mods.eio.sag_mill
mods.eio.Sag
mods.eio.sag
mods.eio.SAGMill
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Sag Mill also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.enderio.sagmill.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 1 and less than or equal to 4. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(ItemStack, float)
        output(Collection<ItemStack>)
        ```

    - `#!groovy RecipeLevel`. Sets the minimum required machine tier of the recipe.

        ```groovy
        tierAny()
        tierNormal()
        tierSimple()
        tierEnhanced()
        ```

    - `#!groovy int`. Sets the energy cost of the recipe. Requires greater than 0.

        ```groovy
        energy(int)
        ```

    - `#!groovy FloatList`. Sets the chance the given output of each output slot. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack, float)
        ```

    - `#!groovy RecipeBonusType`. Sets the type of bonus a Grinding Ball can apply.

        ```groovy
        bonusTypeNone()
        bonusTypeChance()
        bonusTypeMultiply()
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `crazypants.enderio.base.recipe.Recipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.enderio.sagmill.recipeBuilder()
            .input(item('minecraft:diamond_block'))
            .output(item('minecraft:diamond') * 4)
            .output(item('minecraft:clay_ball') * 2, 0.7)
            .output(item('minecraft:gold_ingot'), 0.1)
            .output(item('minecraft:gold_ingot'), 0.1)
            .bonusTypeMultiply()
            .energy(1000)
            .tierEnhanced()
            .register()

        mods.enderio.sagmill.recipeBuilder()
            .input(item('minecraft:clay_ball'))
            .output(item('minecraft:diamond') * 4)
            .output(item('minecraft:gold_ingot'), 0.1)
            .bonusTypeChance()
            .tierNormal()
            .register()

        mods.enderio.sagmill.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:gold_ingot'), 0.1)
            .bonusTypeNone()
            .tierSimple()
            .register()

        mods.enderio.sagmill.recipeBuilder()
            .input(item('minecraft:nether_star'))
            .output(item('minecraft:clay_ball') * 2, 0.7)
            .output(item('minecraft:gold_ingot'), 0.1)
            .tierAny()
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.enderio.sagmill.removeByInput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.enderio.sagmill.removeAll()
    ```

???+ Example
    ```groovy
    mods.enderio.sagmill.removeByInput(item('minecraft:wheat'))
    mods.enderio.sagmill.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.enderio.sagmill.streamRecipes()
    ```
