---
title: "Sag Mill Grinding"
description: "Add a new Griding Ball for use in a Sag Mill with the given output multiplier, power multiplier, chance multiplier, and duration (in base power used)."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/enderio/SagMillGrinding.java"
---

# Sag Mill Grinding (Ender IO)

## Description

Add a new Griding Ball for use in a Sag Mill with the given output multiplier, power multiplier, chance multiplier, and duration (in base power used).

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.enderio.SagMillGrinding
mods.enderio.sagmillgrinding/*(1)!*/
mods.enderio.sagMillGrinding
mods.enderio.sag_mill_grinding
mods.enderio.Grinding
mods.enderio.grinding
mods.eio.SagMillGrinding
mods.eio.sagmillgrinding
mods.eio.sagMillGrinding
mods.eio.sag_mill_grinding
mods.eio.Grinding
mods.eio.grinding
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Sag Mill Grinding also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.enderio.sagmillgrinding.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy float`. Sets the power multiplier to recipes processed with the grinding ball. Requires greater than 0.

        ```groovy
        power(float)
        ```

    - `#!groovy float`. Sets the chance to double all outputs in recipes with an applicable bonusType. Requires greater than 0.

        ```groovy
        chance(float)
        ```

    - `#!groovy int`. Sets the amount of power used in recipes before the grinding ball is consumed. Requires greater than 0.

        ```groovy
        duration(int)
        ```

    - `#!groovy float`. Format error: Sets the chance to increase outputs up to 100% with an applicable bonusType. Requires greater than 0.

        ```groovy
        grinding(float)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `crazypants.enderio.base.recipe.sagmill.GrindingBall`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.enderio.sagmillgrinding.recipeBuilder()
            .input(item('minecraft:clay_ball'))
            .chance(6.66)
            .power(0.001)
            .grinding(3.33)
            .duration(10000)
            .register()
        ```



## Removing Recipes

- Removes the Grinding Ball item:

    ```groovy
    mods.enderio.sagmillgrinding.remove(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.enderio.sagmillgrinding.removeAll()
    ```

???+ Example
    ```groovy
    mods.enderio.sagmillgrinding.remove(item('minecraft:flint'))
    mods.enderio.sagmillgrinding.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.enderio.sagmillgrinding.streamRecipes()
    ```
