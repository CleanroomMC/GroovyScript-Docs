---
title: "Starlight Altar"
description: "Allows creation of shaped recipes in the Astral Sorcery Crafting Altar chain."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/starlightaltar/StarlightAltar.java"
---

# Starlight Altar (Astral Sorcery)

## Description

Allows creation of shaped recipes in the Astral Sorcery Crafting Altar chain.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="14"
mods.astral.StarlightAltar
mods.astral.starlightaltar
mods.astral.starlightAltar
mods.astral.starlight_altar
mods.astral_sorcery.StarlightAltar
mods.astral_sorcery.starlightaltar
mods.astral_sorcery.starlightAltar
mods.astral_sorcery.starlight_altar
mods.as.StarlightAltar
mods.as.starlightaltar
mods.as.starlightAltar
mods.as.starlight_altar
mods.astralsorcery.StarlightAltar
mods.astralsorcery.starlightaltar/*(1)!*/
mods.astralsorcery.starlightAltar
mods.astralsorcery.starlight_altar
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Starlight Altar also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.astralsorcery.starlightaltar.discoveryRecipeBuilder()"
    - `#!groovy String[]`. Sets the items required in each slot of the grid as char. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        row(String)
        shape(String[])
        shape(String...)
        matrix(String[])
        matrix(String...)
        ```

    - `#!groovy List<List<IIngredient>>`. Sets the items required in each slot in the grid as IIngredients. Requires greater than or equal to 1 and less than or equal to 9. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        shape(List)
        shape(List<List<IIngredient>>)
        matrix(List)
        matrix(List<List<IIngredient>>)
        ```

    - `#!groovy Char2ObjectOpenHashMap<IIngredient>`. Sets the item the given char corresponds to. (Default `\` \` = IIngredient.EMPTY`).

        ```groovy
        key(char, IIngredient)
        key(String, IIngredient)
        key(Map<String, IIngredient>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy String`. Sets the name of the recipe, should be unique.

        ```groovy
        name(String)
        ```

    - `#!groovy int`. Sets how long the craft will take to complete in ticks. Requires greater than 0. (Default `0`).

        ```groovy
        craftTime(int)
        ```

    - `#!groovy IConstellation`. Sets the required Constellation for the Rock Crystal to be attuned to. Only applies to Iridescent Altars.

        ```groovy
        constellation(IConstellation)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `net.minecraft.item.crafting.IRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.starlightaltar.discoveryRecipeBuilder()
            .output(item('minecraft:water_bucket'))
            .row('   ')
            .row(' B ')
            .row('   ')
            .key('B', item('minecraft:bucket'))
            .starlight(1)
            .craftTime(10)
            .register()
        ```

???+ Abstract "mods.astralsorcery.starlightaltar.attunementRecipeBuilder()"
    - `#!groovy String[]`. Sets the items required in each slot of the grid as char. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        row(String)
        shape(String[])
        shape(String...)
        matrix(String[])
        matrix(String...)
        ```

    - `#!groovy List<List<IIngredient>>`. Sets the items required in each slot in the grid as IIngredients. Requires greater than or equal to 1 and less than or equal to 9. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        shape(List)
        shape(List<List<IIngredient>>)
        matrix(List)
        matrix(List<List<IIngredient>>)
        ```

    - `#!groovy Char2ObjectOpenHashMap<IIngredient>`. Sets the item the given char corresponds to. (Default `\` \` = IIngredient.EMPTY`).

        ```groovy
        key(char, IIngredient)
        key(String, IIngredient)
        key(Map<String, IIngredient>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy String`. Sets the name of the recipe, should be unique.

        ```groovy
        name(String)
        ```

    - `#!groovy int`. Sets how long the craft will take to complete in ticks. Requires greater than 0. (Default `0`).

        ```groovy
        craftTime(int)
        ```

    - `#!groovy IConstellation`. Sets the required Constellation for the Rock Crystal to be attuned to. Only applies to Iridescent Altars.

        ```groovy
        constellation(IConstellation)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `net.minecraft.item.crafting.IRecipe`).

        ```groovy
        register()
        ```



???+ Abstract "mods.astralsorcery.starlightaltar.constellationRecipeBuilder()"
    - `#!groovy String[]`. Sets the items required in each slot of the grid as char. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        row(String)
        shape(String[])
        shape(String...)
        matrix(String[])
        matrix(String...)
        ```

    - `#!groovy List<List<IIngredient>>`. Sets the items required in each slot in the grid as IIngredients. Requires greater than or equal to 1 and less than or equal to 9. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        shape(List)
        shape(List<List<IIngredient>>)
        matrix(List)
        matrix(List<List<IIngredient>>)
        ```

    - `#!groovy Char2ObjectOpenHashMap<IIngredient>`. Sets the item the given char corresponds to. (Default `\` \` = IIngredient.EMPTY`).

        ```groovy
        key(char, IIngredient)
        key(String, IIngredient)
        key(Map<String, IIngredient>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy String`. Sets the name of the recipe, should be unique.

        ```groovy
        name(String)
        ```

    - `#!groovy int`. Sets how long the craft will take to complete in ticks. Requires greater than 0. (Default `0`).

        ```groovy
        craftTime(int)
        ```

    - `#!groovy IConstellation`. Sets the required Constellation for the Rock Crystal to be attuned to. Only applies to Iridescent Altars.

        ```groovy
        constellation(IConstellation)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `net.minecraft.item.crafting.IRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.starlightaltar.constellationRecipeBuilder()
            .output(item('minecraft:pumpkin'))
            .matrix('ss ss',
                    's   s',
                    '  d  ',
                    's   s',
                    'ss ss')
            .key('s', item('minecraft:pumpkin_seeds'))
            .key('d', ore('dirt'))
            .register()
        ```

???+ Abstract "mods.astralsorcery.starlightaltar.traitRecipeBuilder()"
    - `#!groovy String[]`. Sets the items required in each slot of the grid as char. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        row(String)
        shape(String[])
        shape(String...)
        matrix(String[])
        matrix(String...)
        ```

    - `#!groovy List<List<IIngredient>>`. Sets the items required in each slot in the grid as IIngredients. Requires greater than or equal to 1 and less than or equal to 9. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        shape(List)
        shape(List<List<IIngredient>>)
        matrix(List)
        matrix(List<List<IIngredient>>)
        ```

    - `#!groovy Char2ObjectOpenHashMap<IIngredient>`. Sets the item the given char corresponds to. (Default `\` \` = IIngredient.EMPTY`).

        ```groovy
        key(char, IIngredient)
        key(String, IIngredient)
        key(Map<String, IIngredient>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy String`. Sets the name of the recipe, should be unique.

        ```groovy
        name(String)
        ```

    - `#!groovy int`. Sets how long the craft will take to complete in ticks. Requires greater than 0. (Default `0`).

        ```groovy
        craftTime(int)
        ```

    - `#!groovy IConstellation`. Sets the required Constellation for the Rock Crystal to be attuned to. Only applies to Iridescent Altars.

        ```groovy
        constellation(IConstellation)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `net.minecraft.item.crafting.IRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.starlightaltar.traitRecipeBuilder()
            .output(item('astralsorcery:itemrockcrystalsimple').setSize(300).setPurity(50).setCutting(50))
            .matrix('sssss',
                    'sgggs',
                    'sgdgs',
                    'sgggs',
                    'sssss')
            .key('s', item('minecraft:pumpkin'))
            .key('g', ore('treeLeaves'))
            .key('d', item('minecraft:diamond_block'))
            .outerInput(item('astralsorcery:blockmarble'))
            .outerInput(ore('ingotAstralStarmetal'))
            .outerInput(fluid('astralsorcery.liquidstarlight') * 1000)
            .outerInput(ore('treeSapling'))
            .constellation(constellation('discidia'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output in all Altar tiers:

    ```groovy
    mods.astralsorcery.starlightaltar.removeByOutput(ItemStack)
    ```

- Removes all recipes that match the given output in only the specified Altar tier, in the format `output`, `altarLevel`:

    ```groovy
    mods.astralsorcery.starlightaltar.removeByOutput(ItemStack, TileAltar.AltarLevel)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.starlightaltar.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.starlightaltar.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.starlightaltar.streamRecipes()
    ```
