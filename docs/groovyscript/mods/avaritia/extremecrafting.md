---
title: "Extreme Crafting"
description: "A normal crafting table, by 9x9 instead."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/avaritia/ExtremeCrafting.java"
---

# Extreme Crafting (Avaritia)

## Description

A normal crafting table, by 9x9 instead.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.avaritia.ExtremeCrafting
mods.avaritia.extremecrafting/*(1)!*/
mods.avaritia.extremeCrafting
mods.avaritia.extreme_crafting
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds a shaped crafting recipe in the format `output`, `input`:

    ```groovy
    mods.avaritia.extremecrafting.addShaped(ItemStack, List<List<IIngredient>>)
    ```

- Adds a shapeless crafting recipe in the format `output`, `input`:

    ```groovy
    mods.avaritia.extremecrafting.addShapeless(ItemStack, List<IIngredient>)
    ```


### Recipe Builder

Just like other recipe types, the Extreme Crafting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.avaritia.extremecrafting.shapedBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe. (Default `null`).

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy String[]`. Sets the items required in each slot of the grid as char. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both. (Default `null`).

        ```groovy
        row(String)
        shape(String...)
        matrix(String...)
        ```

    - `#!groovy List<List<IIngredient>>`. Sets the items required in each slot in the grid as IIngredients. Requires greater than or equal to 1 and less than or equal to 81. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both. (Default `null`).

        ```groovy
        shape(List<List<IIngredient>>)
        matrix(List<List<IIngredient>>)
        ```

    - `#!groovy Char2ObjectOpenHashMap<IIngredient>`. Sets the item the given char corresponds to.

        ```groovy
        key(String, IIngredient)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null. (Default `null`).

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy byte`. Sets if the recipe is removed. A value of 1 removes by the output, and a value of 2 removes by the resource location.

        ```groovy
        replace()
        ```

    - `#!groovy boolean`. Sets if the recipe is horizontally mirrored.

        ```groovy
        mirrored()
        mirrored(boolean)
        ```

    - `#!groovy Closure<ItemStack>`. Sets an operation that modifies the input items or output item. (Default `null`).

        ```groovy
        recipeFunction(Closure<ItemStack>)
        ```

    - `#!groovy Closure<Void>`. Sets an operation that happens when the recipe is crafted. (Default `null`).

        ```groovy
        recipeAction(Closure<Void>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `morph.avaritia.recipe.extreme.IExtremeRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.avaritia.extremecrafting.shapedBuilder()
            .matrix([[item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')]])
            .output(item('minecraft:gold_block'))
            .register()

        mods.avaritia.extremecrafting.shapedBuilder()
            .output(item('minecraft:stone') * 64)
            .matrix('DLLLLLDDD',
                    '  DNIGIND',
                    'DDDNIGIND',
                    '  DLLLLLD')
            .key('D', item('minecraft:diamond'))
            .key('L', item('minecraft:redstone'))
            .key('N', item('minecraft:stone').reuse())
            .key('I', item('minecraft:iron_ingot'))
            .key('G', item('minecraft:gold_ingot'))
            .register()
        ```

???+ Abstract "mods.avaritia.extremecrafting.shapelessBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe. (Default `null`).

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy List<IIngredient>`. Sets the items required for the recipe. Requires greater than or equal to 1 and less than or equal to 81. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null. (Default `null`).

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy byte`. Sets if the recipe is removed. A value of 1 removes by the output, and a value of 2 removes by the resource location.

        ```groovy
        replace()
        ```

    - `#!groovy Closure<ItemStack>`. Sets an operation that modifies the input items or output item. (Default `null`).

        ```groovy
        recipeFunction(Closure<ItemStack>)
        ```

    - `#!groovy Closure<Void>`. Sets an operation that happens when the recipe is crafted. (Default `null`).

        ```groovy
        recipeAction(Closure<Void>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.avaritia.extremecrafting.shapelessBuilder()
            .output(item('minecraft:stone') * 64)
            .input(item('minecraft:stone'), item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'), item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'), item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'), item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'), item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.avaritia.extremecrafting.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.avaritia.extremecrafting.removeAll()
    ```

???+ Example
    ```groovy
    mods.avaritia.extremecrafting.removeByOutput(item('avaritia:resource', 6))
    mods.avaritia.extremecrafting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.avaritia.extremecrafting.streamRecipes()
    ```
