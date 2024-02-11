---
title: "Ball of Fur"
description: "A weighted itemstack output for using a Ball of Fur, dropped by a cat."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/actuallyadditions/BallOfFur.java"
---

# Ball of Fur (Actually Additions)

## Description

A weighted itemstack output for using a Ball of Fur, dropped by a cat.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.aa.ball_of_fur
mods.aa.balloffur
mods.aa.ballOfFur
mods.aa.BallOfFur
mods.actuallyadditions.ball_of_fur/*(1)!*/
mods.actuallyadditions.balloffur
mods.actuallyadditions.ballOfFur
mods.actuallyadditions.BallOfFur
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Ball of Fur also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.actuallyadditions.ball_of_fur.recipeBuilder()"
    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. Sets how likely this entry is to be rolled. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        weight(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `de.ellpeck.actuallyadditions.api.recipe.BallOfFurReturn`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.actuallyadditions.ball_of_fur.recipeBuilder()
            .output(item('minecraft:clay') * 32)
            .weight(15)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.actuallyadditions.ball_of_fur.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.actuallyadditions.ball_of_fur.removeAll()
    ```

???+ Example
    ```groovy
    mods.actuallyadditions.ball_of_fur.removeByOutput(item('minecraft:feather'))
    mods.actuallyadditions.ball_of_fur.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.actuallyadditions.ball_of_fur.streamRecipes()
    ```
