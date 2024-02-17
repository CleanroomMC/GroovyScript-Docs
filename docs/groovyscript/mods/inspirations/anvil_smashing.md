---
title: "Anvil Smashing"
description: "Converts a Block or IBlockState into an IBlockState when an anvil falls on top of it (from any height)."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/inspirations/AnvilSmashing.java"
---

# Anvil Smashing (Inspirations)

## Description

Converts a Block or IBlockState into an IBlockState when an anvil falls on top of it (from any height).

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.inspirations.anvil_smashing/*(1)!*/
mods.inspirations.anvilsmashing
mods.inspirations.anvilSmashing
mods.inspirations.AnvilSmashing
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds an Anvil Smashing recipe in the format `input`, `output`:

    ```groovy
    mods.inspirations.anvil_smashing.add(Block, IBlockState)
    ```

- Adds an Anvil Smashing recipe in the format `input`, `output`:

    ```groovy
    mods.inspirations.anvil_smashing.add(IBlockState, IBlockState)
    ```


### Recipe Builder

Just like other recipe types, the Anvil Smashing also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.inspirations.anvil_smashing.recipeBuilder()"
    - `#!groovy IBlockState`. Sets the output IBlockState that replaces the input. Requires not null.

        ```groovy
        output(IBlockState)
        ```

    - `#!groovy Block`. Sets the input Block. Requires either `inputBlock` or `inputBlockState` to be non-null.

        ```groovy
        input(Block)
        ```

    - `#!groovy IBlockState`. Sets the input IBlockState. Requires either `inputBlock` or `inputBlockState` to be non-null.

        ```groovy
        input(IBlockState)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.anvil_smashing.recipeBuilder()
            .input(blockstate('minecraft:diamond_block'))
            .output(blockstate('minecraft:clay'))
            .register()

        mods.inspirations.anvil_smashing.recipeBuilder()
            .input(blockstate('minecraft:clay'))
            .output(blockstate('minecraft:air'))
            .register()
        ```



## Removing Recipes

- Removes an Anvil Smashing recipe in the format `input`, `output`:

    ```groovy
    mods.inspirations.anvil_smashing.remove(Block, IBlockState)
    ```

- Removes an Anvil Smashing recipe in the format `input`, `output`:

    ```groovy
    mods.inspirations.anvil_smashing.remove(IBlockState, IBlockState)
    ```

- Removes an Anvil Smashing recipe matching the given input material:

    ```groovy
    mods.inspirations.anvil_smashing.remove(Material)
    ```

- Removes an Anvil Smashing recipe with the given Block or IBlockState input:

    ```groovy
    mods.inspirations.anvil_smashing.removeByInput(Block)
    ```

- Removes an Anvil Smashing recipe with the given Block or IBlockState input:

    ```groovy
    mods.inspirations.anvil_smashing.removeByInput(IBlockState)
    ```

- Removes all Anvil Smashing recipes with the given IBlockState output:

    ```groovy
    mods.inspirations.anvil_smashing.removeByOutput(IBlockState)
    ```

- Removes all registered recipes:

    ```groovy
    mods.inspirations.anvil_smashing.removeAll()
    ```

???+ Example
    ```groovy
    mods.inspirations.anvil_smashing.removeByInput(blockstate('minecraft:packed_ice'))
    mods.inspirations.anvil_smashing.removeByOutput(blockstate('minecraft:cobblestone'))
    mods.inspirations.anvil_smashing.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.inspirations.anvil_smashing.streamRecipes()
    ```
