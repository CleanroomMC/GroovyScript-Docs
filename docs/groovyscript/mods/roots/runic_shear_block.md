---
title: "Runic Shear Block"
description: "Right clicking a Runic Shear on a block to convert it into a replacement block and drop items."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/RunicShearBlock.java"
---

# Runic Shear Block (Roots 3)

## Description

Right clicking a Runic Shear on a block to convert it into a replacement block and drop items.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.roots.runic_shear_block/*(1)!*/
mods.roots.runicshearblock
mods.roots.runicShearBlock
mods.roots.RunicShearBlock
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Runic Shear Block also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.runic_shear_block.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy BlockStatePredicate`. Sets the target input blockstate. Requires not null.

        ```groovy
        state(IBlockState)
        state(BlockStatePredicate)
        ```

    - `#!groovy ItemStack`. Sets the item representing the target input blockstate.

        ```groovy
        displayItem(ItemStack)
        ```

    - `#!groovy IBlockState`. Sets the blockstate replacing the input block. Requires not null.

        ```groovy
        replacementState(IBlockState)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.recipe.RunicShearRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.runic_shear_block.recipeBuilder()
            .name('clay_from_runic_diamond')
            .state(blockstate('minecraft:diamond_block'))
            .replacementState(blockstate('minecraft:air'))
            .output(item('minecraft:clay') * 64)
            .displayItem(item('minecraft:diamond') * 9)
            .register()

        mods.roots.runic_shear_block.recipeBuilder()
            .state(mods.roots.predicates.stateBuilder().blockstate(blockstate('minecraft:yellow_flower:type=dandelion')).properties('type').register())
            .replacementState(blockstate('minecraft:red_flower:type=poppy'))
            .output(item('minecraft:gold_ingot'))
            .register()
        ```



## Removing Recipes

- Removes the Runic Shear Block recipe with the given name:

    ```groovy
    mods.roots.runic_shear_block.removeByName(ResourceLocation)
    ```

- Removes the Runic Shear Block recipe with the given output itemstack:

    ```groovy
    mods.roots.runic_shear_block.removeByOutput(ItemStack)
    ```

- Removes the Runic Shear Block recipe with the given output IBlockState:

    ```groovy
    mods.roots.runic_shear_block.removeByState(IBlockState)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.runic_shear_block.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.runic_shear_block.removeByName(resource('roots:wildewheet'))
    mods.roots.runic_shear_block.removeByOutput(item('roots:spirit_herb'))
    mods.roots.runic_shear_block.removeByState(blockstate('minecraft:beetroots:age=3'))
    mods.roots.runic_shear_block.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.runic_shear_block.streamRecipes()
    ```
