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

```groovy hl_lines="14"
mods.astral.LightTransmutation
mods.astral.lighttransmutation
mods.astral.lightTransmutation
mods.astral.light_transmutation
mods.astral_sorcery.LightTransmutation
mods.astral_sorcery.lighttransmutation
mods.astral_sorcery.lightTransmutation
mods.astral_sorcery.light_transmutation
mods.as.LightTransmutation
mods.as.lighttransmutation
mods.as.lightTransmutation
mods.as.light_transmutation
mods.astralsorcery.LightTransmutation
mods.astralsorcery.lighttransmutation/*(1)!*/
mods.astralsorcery.lightTransmutation
mods.astralsorcery.light_transmutation
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Light Transmutation also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.astralsorcery.lighttransmutation.recipeBuilder()"
    - `#!groovy double`. Sets the amount of starlight required to complete the craft. Requires greater than or equal to 0.

        ```groovy
        cost(double)
        ```

    - `#!groovy IBlockState`. Sets the input IBlockState, recipe will convert only the given blockstate. Requires not null and not inBlock. (Default `null`).

        ```groovy
        input(IBlockState)
        ```

    - `#!groovy IBlockState`. Sets the output IBlockState. Requires not null. (Default `null`).

        ```groovy
        output(Block)
        output(IBlockState)
        ```

    - `#!groovy Block`. Sets the input Block, recipe will convert any blockstate of the provided block. Requires not null and not input. (Default `null`).

        ```groovy
        input(Block)
        ```

    - `#!groovy ItemStack`. Sets the item representing the input Block or IBlockState in JEI. (Default `null`).

        ```groovy
        inputDisplayStack(ItemStack)
        ```

    - `#!groovy ItemStack`. Sets the item representing the output IBlockState in JEI. (Default `null`).

        ```groovy
        outputDisplayStack(ItemStack)
        ```

    - `#!groovy IWeakConstellation`. Sets the required Constellation the starlight must be collected from. Must be either a Major or Weak Constellation. (Default `null`).

        ```groovy
        constellation(IWeakConstellation)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `hellfirepvp.astralsorcery.common.base.LightOreTransmutations$Transmutation`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.lighttransmutation.recipeBuilder()
            .input(block('minecraft:stone'))
            .output(block('astralsorcery:blockmarble'))
            .cost(100.0)
            .constellation(constellation('armara'))
            .inputDisplayStack(item('minecraft:stone'))
            .outputDisplayStack(item('minecraft:dye:15').withNbt([display:[Name:'Marble']]))
            .register()

        mods.astralsorcery.lighttransmutation.recipeBuilder()
            .input(blockstate('minecraft:pumpkin'))
            .output(blockstate('minecraft:diamond_block'))
            .cost(0)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.lighttransmutation.removeByInput(Block)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.lighttransmutation.removeByInput(IBlockState)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.astralsorcery.lighttransmutation.removeByOutput(Block)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.astralsorcery.lighttransmutation.removeByOutput(IBlockState)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.lighttransmutation.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.lighttransmutation.removeByInput(block('minecraft:netherrack'))
    mods.astralsorcery.lighttransmutation.removeByInput(blockstate('minecraft:sandstone'))
    mods.astralsorcery.lighttransmutation.removeByOutput(block('minecraft:lapis_block'))
    mods.astralsorcery.lighttransmutation.removeByOutput(blockstate('minecraft:cake'))
    mods.astralsorcery.lighttransmutation.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.lighttransmutation.streamRecipes()
    ```
