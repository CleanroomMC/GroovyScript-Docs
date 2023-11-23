---
title: "Transmutation"
description: "When running the Transmutation, convert nearby blocks that match a set of conditions into either a block or items."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/Transmutation.java"
---

# Transmutation (Roots 3)

## Description

When running the Transmutation, convert nearby blocks that match a set of conditions into either a block or items.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.roots.Transmutation
mods.roots.transmutation/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Transmutation also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.transmutation.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe. (Default `null`).

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 0 and less than or equal to 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy BlockStatePredicate`. Sets the starting blockstate. Requires not null. (Default `null`).

        ```groovy
        start(IBlockState)
        start(BlockStatePredicate)
        ```

    - `#!groovy IBlockState`. Sets the output iblockstate. (Default `null`).

        ```groovy
        state(IBlockState)
        output(IBlockState)
        ```

    - `#!groovy WorldBlockStatePredicate`. Sets a condition for the input to be converted, typically indicating a specific block above or below.

        ```groovy
        condition(WorldBlockStatePredicate)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.recipe.TransmutationRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.transmutation.recipeBuilder()
            .name('clay_duping')
            .start(blockstate('minecraft:clay'))
            .output(item('minecraft:clay_ball') * 30)
            .condition(mods.roots.predicates.stateBuilder().blockstate(blockstate('minecraft:gold_block')).below().register())
            .register()

        mods.roots.transmutation.recipeBuilder()
            .start(mods.roots.predicates.stateBuilder().blockstate(blockstate('minecraft:yellow_flower:type=dandelion')).properties('type').register())
            .state(blockstate('minecraft:gold_block'))
            .condition(mods.roots.predicates.above(mods.roots.predicates.LEAVES))
            .register()

        mods.roots.transmutation.recipeBuilder()
            .start(blockstate('minecraft:diamond_block'))
            .state(blockstate('minecraft:gold_block'))
            .register()
        ```



## Removing Recipes

- Removes the Transmutation recipe for the given input IBlockState:

    ```groovy
    mods.roots.transmutation.removeByInput(IBlockState)
    ```

- Removes the Transmutation recipe with the given name:

    ```groovy
    mods.roots.transmutation.removeByName(ResourceLocation)
    ```

- Removes the Transmutation recipe for the given output itemstack:

    ```groovy
    mods.roots.transmutation.removeByOutput(ItemStack)
    ```

- Removes the Transmutation recipe for the given output IBlockState:

    ```groovy
    mods.roots.transmutation.removeByOutput(IBlockState)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.transmutation.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.transmutation.removeByName(resource('roots:redstone_block_to_glowstone'))
    mods.roots.transmutation.removeByOutput(item('minecraft:dye:3'))
    mods.roots.transmutation.removeByOutput(blockstate('minecraft:log:variant=jungle'))
    mods.roots.transmutation.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.transmutation.streamRecipes()
    ```
