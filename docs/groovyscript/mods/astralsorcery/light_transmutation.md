---
title: "Light Transmutation"
description: "Converts an input Block or IBlockState into an output IBlockState after being sent a given amount of starlight, with the ability to require a specific constellation of starlight."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/LightTransmutation.java"
---

# Light Transmutation (Astral Sorcery)

## Description

Converts an input Block or IBlockState into an output IBlockState after being sent a given amount of starlight, with the ability to require a specific constellation of starlight.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.astral_sorcery.light_transmutation
mods.astral_sorcery.lighttransmutation
mods.astral_sorcery.lightTransmutation
mods.astral_sorcery.LightTransmutation
mods.astralsorcery.light_transmutation/*(1)!*/
mods.astralsorcery.lighttransmutation
mods.astralsorcery.lightTransmutation
mods.astralsorcery.LightTransmutation
mods.astral.light_transmutation
mods.astral.lighttransmutation
mods.astral.lightTransmutation
mods.astral.LightTransmutation
mods.as.light_transmutation
mods.as.lighttransmutation
mods.as.lightTransmutation
mods.as.LightTransmutation
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Light Transmutation also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.astralsorcery.light_transmutation.recipeBuilder()"
    - `#!groovy double`. Sets the amount of starlight required to complete the craft. Requires greater than or equal to 0. (Default `0.0d`).

        ```groovy
        cost(double)
        ```

    - `#!groovy IBlockState`. Sets the input IBlockState, recipe will convert only the given blockstate. Requires not null and not inBlock.

        ```groovy
        input(IBlockState)
        ```

    - `#!groovy IBlockState`. Sets the output IBlockState. Requires not null.

        ```groovy
        output(Block)
        output(IBlockState)
        ```

    - `#!groovy Block`. Sets the input Block, recipe will convert any blockstate of the provided block. Requires not null and not input.

        ```groovy
        input(Block)
        ```

    - `#!groovy ItemStack`. Sets the item representing the input Block or IBlockState in JEI.

        ```groovy
        inputDisplayStack(ItemStack)
        ```

    - `#!groovy ItemStack`. Sets the item representing the output IBlockState in JEI.

        ```groovy
        outputDisplayStack(ItemStack)
        ```

    - `#!groovy IWeakConstellation`. Sets the required Constellation the starlight must be collected from. Must be either a Major or Weak Constellation.

        ```groovy
        constellation(IWeakConstellation)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `hellfirepvp.astralsorcery.common.base.LightOreTransmutations$Transmutation`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.light_transmutation.recipeBuilder()
            .input(block('minecraft:stone'))
            .output(block('astralsorcery:blockmarble'))
            .cost(100.0)
            .constellation(constellation('armara'))
            .inputDisplayStack(item('minecraft:stone'))
            .outputDisplayStack(item('minecraft:dye:15').withNbt([display:[Name:'Marble']]))
            .register()

        mods.astralsorcery.light_transmutation.recipeBuilder()
            .input(blockstate('minecraft:pumpkin'))
            .output(blockstate('minecraft:diamond_block'))
            .cost(0)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.light_transmutation.removeByInput(Block)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.light_transmutation.removeByInput(IBlockState)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.astralsorcery.light_transmutation.removeByOutput(Block)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.astralsorcery.light_transmutation.removeByOutput(IBlockState)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.light_transmutation.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.light_transmutation.removeByInput(block('minecraft:netherrack'))
    mods.astralsorcery.light_transmutation.removeByInput(blockstate('minecraft:sandstone'))
    mods.astralsorcery.light_transmutation.removeByOutput(block('minecraft:lapis_block'))
    mods.astralsorcery.light_transmutation.removeByOutput(blockstate('minecraft:cake'))
    mods.astralsorcery.light_transmutation.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.light_transmutation.streamRecipes()
    ```
