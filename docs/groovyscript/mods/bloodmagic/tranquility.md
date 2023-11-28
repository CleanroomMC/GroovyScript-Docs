---
title: "Tranquility"
description: "Blocks in the area around the Tranquility Altar provide tranquility up to the Altar's cap, with reduced effect the more of a particular type of Tranquility is provided."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/bloodmagic/Tranquility.java"
---

# Tranquility (Blood Magic: Alchemical Wizardry)

## Description

Blocks in the area around the Tranquility Altar provide tranquility up to the Altar's cap, with reduced effect the more of a particular type of Tranquility is provided.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="4"
mods.bm.Tranquility
mods.bm.tranquility
mods.bloodmagic.Tranquility
mods.bloodmagic.tranquility/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `block`, `tranquility`, `value`:

    ```groovy
    mods.bloodmagic.tranquility.add(Block, String, double)
    ```

- Adds recipes in the format `block`, `tranquility`:

    ```groovy
    mods.bloodmagic.tranquility.add(Block, TranquilityStack)
    ```

- Adds recipes in the format `blockstate`, `tranquility`, `value`:

    ```groovy
    mods.bloodmagic.tranquility.add(IBlockState, String, double)
    ```

- Adds recipes in the format `blockstate`, `tranquility`:

    ```groovy
    mods.bloodmagic.tranquility.add(IBlockState, TranquilityStack)
    ```


### Recipe Builder

Just like other recipe types, the Tranquility also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.bloodmagic.tranquility.recipeBuilder()"
    - `#!groovy Block`. Sets the target block.

        ```groovy
        block(Block)
        ```

    - `#!groovy double`. Sets the amount of Tranquility provided. Requires greater than or equal to 0. (Default `0.0d`).

        ```groovy
        value(double)
        ```

    - `#!groovy IBlockState`. Sets the target blockstate.

        ```groovy
        blockstate(IBlockState)
        ```

    - `#!groovy EnumTranquilityType`. Sets the type of Tranquility being modified. Requires not null.

        ```groovy
        tranquility(String)
        tranquility(EnumTranquilityType)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.bloodmagic.tranquility.recipeBuilder()
            .block(block('minecraft:obsidian'))
            .tranquility('LAVA')
            .value(10)
            .register()

        mods.bloodmagic.tranquility.recipeBuilder()
            .block(block('minecraft:obsidian'))
            .tranquility('WATER')
            .value(10)
            .register()

        mods.bloodmagic.tranquility.recipeBuilder()
            .blockstate(blockstate('minecraft:obsidian'))
            .tranquility('LAVA')
            .value(500)
            .register()
        ```



## Removing Recipes

- Removes any Tranquility entry that matches the given Block and EnumTranquilityType:

    ```groovy
    mods.bloodmagic.tranquility.remove(Block, EnumTranquilityType)
    ```

- Removes any Tranquility entry that matches the given Block and Tranquility type as String:

    ```groovy
    mods.bloodmagic.tranquility.remove(Block, String)
    ```

- Removes any Tranquility entry that matches the given IBlockState and EnumTranquilityType:

    ```groovy
    mods.bloodmagic.tranquility.remove(IBlockState, EnumTranquilityType)
    ```

- Removes any Tranquility entry that matches the given IBlockState and Tranquility as String:

    ```groovy
    mods.bloodmagic.tranquility.remove(IBlockState, String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.bloodmagic.tranquility.removeAll()
    ```

???+ Example
    ```groovy
    mods.bloodmagic.tranquility.remove(block('minecraft:dirt'), 'EARTHEN')
    mods.bloodmagic.tranquility.remove(blockstate('minecraft:netherrack'), 'FIRE')
    mods.bloodmagic.tranquility.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.bloodmagic.tranquility.streamRecipes()
    ```
