---
title: "Nether Mining Lens"
description: "A weighted oredict for the block obtained via firing a Mining Lens at a block of Netherrack. The oredict must have a block, or the world will hang."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/actuallyadditions/NetherMiningLens.java"
---

# Nether Mining Lens (Actually Additions)

## Description

A weighted oredict for the block obtained via firing a Mining Lens at a block of Netherrack. The oredict must have a block, or the world will hang.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="6"
mods.aa.NetherMiningLens
mods.aa.nethermininglens
mods.aa.netherMiningLens
mods.aa.nether_mining_lens
mods.actuallyadditions.NetherMiningLens
mods.actuallyadditions.nethermininglens/*(1)!*/
mods.actuallyadditions.netherMiningLens
mods.actuallyadditions.nether_mining_lens
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Nether Mining Lens also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.actuallyadditions.nethermininglens.recipeBuilder()"
    - `#!groovy String`. Sets the ore given by the recipe. Requires not null.

        ```groovy
        ore(String)
        ore(OreDictIngredient)
        ```

    - `#!groovy int`. Sets how likely this ore is to be rolled. Requires greater than or equal to 0.

        ```groovy
        weight(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `de.ellpeck.actuallyadditions.api.recipe.WeightedOre`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.actuallyadditions.nethermininglens.recipeBuilder()
            .ore(ore('blockDiamond'))
            .weight(100)
            .register()

        mods.actuallyadditions.nethermininglens.recipeBuilder()
            .ore('blockGold')
            .weight(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given ore:

    ```groovy
    mods.actuallyadditions.nethermininglens.removeByOre(OreDictIngredient)
    ```

- Removes all recipes that match the given ore:

    ```groovy
    mods.actuallyadditions.nethermininglens.removeByOre(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.actuallyadditions.nethermininglens.removeAll()
    ```

???+ Example
    ```groovy
    mods.actuallyadditions.nethermininglens.removeByOre(ore('oreQuartz'))
    mods.actuallyadditions.nethermininglens.removeByOre('oreQuartz')
    mods.actuallyadditions.nethermininglens.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.actuallyadditions.nethermininglens.streamRecipes()
    ```
