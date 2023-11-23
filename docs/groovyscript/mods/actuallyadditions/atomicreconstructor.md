---
title: "Atomic Reconstructor"
description: "The Atomic Reconstructor is a block which uses energy to convert a block or item in front of it into other items."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/actuallyadditions/AtomicReconstructor.java"
---

# Atomic Reconstructor (Actually Additions)

## Description

The Atomic Reconstructor is a block which uses energy to convert a block or item in front of it into other items.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="6"
mods.aa.AtomicReconstructor
mods.aa.atomicreconstructor
mods.aa.atomicReconstructor
mods.aa.atomic_reconstructor
mods.actuallyadditions.AtomicReconstructor
mods.actuallyadditions.atomicreconstructor/*(1)!*/
mods.actuallyadditions.atomicReconstructor
mods.actuallyadditions.atomic_reconstructor
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Atomic Reconstructor also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.actuallyadditions.atomicreconstructor.recipeBuilder()"
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

    - `#!groovy int`. Sets the amount of power consumed by the recipe. Requires greater than 0.

        ```groovy
        energy(int)
        energyUse(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `de.ellpeck.actuallyadditions.api.recipe.LensConversionRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.actuallyadditions.atomicreconstructor.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:diamond'))
            .energyUse(1000)
            .register()

        mods.actuallyadditions.atomicreconstructor.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:diamond'))
            .energy(1000)
            .register()

        mods.actuallyadditions.atomicreconstructor.recipeBuilder()
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:clay') * 2)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given ore:

    ```groovy
    mods.actuallyadditions.atomicreconstructor.removeByInput(IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.actuallyadditions.atomicreconstructor.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.actuallyadditions.atomicreconstructor.removeAll()
    ```

???+ Example
    ```groovy
    mods.actuallyadditions.atomicreconstructor.removeByInput(item('minecraft:diamond'))
    mods.actuallyadditions.atomicreconstructor.removeByOutput(item('actuallyadditions:block_crystal'))
    mods.actuallyadditions.atomicreconstructor.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.actuallyadditions.atomicreconstructor.streamRecipes()
    ```
