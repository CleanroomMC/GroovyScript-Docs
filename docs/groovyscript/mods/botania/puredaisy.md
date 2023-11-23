---
title: "Pure Daisy"
description: "Convert a given block to another blockstate after a period of time."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/PureDaisy.java"
---

# Pure Daisy (Botania)

## Description

Convert a given block to another blockstate after a period of time.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.PureDaisy
mods.botania.puredaisy/*(1)!*/
mods.botania.pureDaisy
mods.botania.pure_daisy
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `time`:

    ```groovy
    mods.botania.puredaisy.add(IBlockState, IBlockState, int)
    ```

- Adds recipes in the format `output`, `input`:

    ```groovy
    mods.botania.puredaisy.add(IBlockState, IBlockState)
    ```


### Recipe Builder

Just like other recipe types, the Pure Daisy also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.botania.puredaisy.recipeBuilder()"
    - `#!groovy int`. Sets the duration the recipe takes to complete. Requires greater than or equal to 0.

        ```groovy
        time(int)
        ```

    - `#!groovy Object`. Sets the valid input states. Requires not null. Requires either an IBlockState or String. (Default `null`).

        ```groovy
        input(Block)
        input(String)
        input(IBlockState)
        input(OreDictIngredient)
        ```

    - `#!groovy IBlockState`. Sets the output IBlockState. Requires not null. (Default `null`).

        ```groovy
        output(IBlockState)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `vazkii.botania.api.recipe.RecipePureDaisy`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.botania.puredaisy.recipeBuilder()
            .input(ore('plankWood'))
            .output(blockstate('minecraft:clay'))
            .time(5)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.puredaisy.removeByInput(Block)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.puredaisy.removeByInput(IBlockState)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.puredaisy.removeByInput(OreDictIngredient)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.puredaisy.removeByInput(String)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.puredaisy.removeByOutput(IBlockState)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.puredaisy.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.puredaisy.removeByInput(blockstate('minecraft:water'))
    mods.botania.puredaisy.removeByInput(ore('logWood'))
    mods.botania.puredaisy.removeByOutput(blockstate('botania:livingrock'))
    mods.botania.puredaisy.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.puredaisy.streamRecipes()
    ```
