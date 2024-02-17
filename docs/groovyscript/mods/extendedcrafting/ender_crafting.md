---
title: "Ender Crafting"
description: "A normal crafting recipe, with the recipe being slowly crafted based on nearby Ender Alternators."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/extendedcrafting/EnderCrafting.java"
---

# Ender Crafting (Extended Crafting)

## Description

A normal crafting recipe, with the recipe being slowly crafted based on nearby Ender Alternators.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.extendedcrafting.ender_crafting/*(1)!*/
mods.extendedcrafting.endercrafting
mods.extendedcrafting.enderCrafting
mods.extendedcrafting.EnderCrafting
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds a shaped crafting recipe in the format `time`, `output`, `input`:

    ```groovy
    mods.extendedcrafting.ender_crafting.addShaped(int, ItemStack, List<List<IIngredient>>)
    ```

- Adds a shaped crafting recipe in the format `output`, `input`:

    ```groovy
    mods.extendedcrafting.ender_crafting.addShaped(ItemStack, List<List<IIngredient>>)
    ```

- Adds a shapeless crafting recipe in the format `time`, `output`, `input`:

    ```groovy
    mods.extendedcrafting.ender_crafting.addShapeless(int, ItemStack, List<IIngredient>)
    ```

- Adds a shapeless crafting recipe in the format `output`, `input`:

    ```groovy
    mods.extendedcrafting.ender_crafting.addShapeless(ItemStack, List<List<IIngredient>>)
    ```


### Recipe Builder

Just like other recipe types, the Ender Crafting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.extendedcrafting.ender_crafting.shapedBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy Char2ObjectOpenHashMap<IIngredient>`. Sets the item the given char corresponds to. (Default `' ' = IIngredient.EMPTY`).

        ```groovy
        key(char, IIngredient)
        key(String, IIngredient)
        key(Map<String, IIngredient>)
        ```

    - `#!groovy String[]`. Sets the items required in each slot of the grid as char. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        row(String)
        shape(String...)
        matrix(String...)
        ```

    - `#!groovy List<List<IIngredient>>`. Sets the items required in each slot in the grid as IIngredients. Requires greater than or equal to 1 and less than or equal to 9. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        shape(List<List<IIngredient>>)
        matrix(List<List<IIngredient>>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy int`. Sets the duration in seconds for the recipe, reduced by each Ender Accelerator. Requires greater than or equal to 0. (Default `ModConfig.confEnderTimeRequired`).

        ```groovy
        time(int)
        ticks(int)
        seconds(int)
        ```

    - `#!groovy byte`. Sets if the recipe is removed. A value of 1 removes by the output, and a value of 2 removes by the resource location. (Default `0`).

        ```groovy
        replace()
        ```

    - `#!groovy boolean`. Sets if the recipe is horizontally mirrored. (Default `false`).

        ```groovy
        mirrored()
        mirrored(boolean)
        ```

    - `#!groovy Closure<ItemStack>`. Sets an operation that modifies the input items or output item.

        ```groovy
        recipeFunction(Closure<ItemStack>)
        ```

    - `#!groovy Closure<Void>`. Sets an operation that happens when the recipe is crafted.

        ```groovy
        recipeAction(Closure<Void>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `net.minecraft.item.crafting.IRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.extendedcrafting.ender_crafting.shapedBuilder()
            .output(item('minecraft:stone'))
            .matrix('BXX',
                    'X B')
            .key('B', item('minecraft:stone'))
            .key('X', item('minecraft:gold_ingot'))
            .time(1)
            .mirrored()
            .register()

        mods.extendedcrafting.ender_crafting.shapedBuilder()
            .output(item('minecraft:diamond') * 32)
            .matrix([[item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')]])
            .time(1)
            .register()
        ```

???+ Abstract "mods.extendedcrafting.ender_crafting.shapelessBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy List<IIngredient>`. Sets the items required for the recipe. Requires greater than or equal to 1 and less than or equal to 9.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy int`. Sets the duration in seconds for the recipe, reduced by each Ender Accelerator. Requires greater than or equal to 0. (Default `ModConfig.confEnderTimeRequired`).

        ```groovy
        time(int)
        ticks(int)
        seconds(int)
        ```

    - `#!groovy byte`. Sets if the recipe is removed. A value of 1 removes by the output, and a value of 2 removes by the resource location. (Default `0`).

        ```groovy
        replace()
        ```

    - `#!groovy Closure<ItemStack>`. Sets an operation that modifies the input items or output item.

        ```groovy
        recipeFunction(Closure<ItemStack>)
        ```

    - `#!groovy Closure<Void>`. Sets an operation that happens when the recipe is crafted.

        ```groovy
        recipeAction(Closure<Void>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `net.minecraft.item.crafting.IRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.extendedcrafting.ender_crafting.shapelessBuilder()
            .output(item('minecraft:clay') * 8)
            .input(item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'))
            .register()

        mods.extendedcrafting.ender_crafting.shapelessBuilder()
            .output(item('minecraft:clay') * 32)
            .input(item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:diamond'))
            .time(1)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.extendedcrafting.ender_crafting.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.extendedcrafting.ender_crafting.removeAll()
    ```

???+ Example
    ```groovy
    mods.extendedcrafting.ender_crafting.removeByOutput(item('extendedcrafting:material:40'))
    mods.extendedcrafting.ender_crafting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.extendedcrafting.ender_crafting.streamRecipes()
    ```
