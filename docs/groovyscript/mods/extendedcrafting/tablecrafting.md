---
title: "Table Crafting"
description: "A normal crafting recipe, but requiring either a specific tier, or at least a given tier, from 3x3 to 9x9."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/extendedcrafting/TableCrafting.java"
---

# Table Crafting (Extended Crafting)

## Description

A normal crafting recipe, but requiring either a specific tier, or at least a given tier, from 3x3 to 9x9.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.extendedcrafting.TableCrafting
mods.extendedcrafting.tablecrafting/*(1)!*/
mods.extendedcrafting.tableCrafting
mods.extendedcrafting.table_crafting
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds a shaped crafting recipe in the format `tier`, `output`, `input`:

    ```groovy
    mods.extendedcrafting.tablecrafting.addShaped(int, ItemStack, List<List<IIngredient>>)
    ```

- Adds a shaped crafting recipe in the format `output`, `input`:

    ```groovy
    mods.extendedcrafting.tablecrafting.addShaped(ItemStack, List<List<IIngredient>>)
    ```

- Adds a shapeless crafting recipe in the format `tier`, `output`, `input`:

    ```groovy
    mods.extendedcrafting.tablecrafting.addShapeless(int, ItemStack, List<IIngredient>)
    ```

- Adds a shapeless crafting recipe in the format `output`, `input`:

    ```groovy
    mods.extendedcrafting.tablecrafting.addShapeless(ItemStack, List<List<IIngredient>>)
    ```


### Recipe Builder

Just like other recipe types, the Table Crafting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.extendedcrafting.tablecrafting.shapedBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy Char2ObjectOpenHashMap<IIngredient>`. Sets the item the given char corresponds to. (Default `\` \` = IIngredient.EMPTY`).

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

    - `#!groovy List<List<IIngredient>>`. Sets the items required in each slot in the grid as IIngredients. Requires greater than or equal to 1 and less than or equal to 81. Requires either the key-based matrix or the ingredient-based matrix can be defined, not both.

        ```groovy
        shape(List<List<IIngredient>>)
        matrix(List<List<IIngredient>>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy int`. Sets the tier of table required, with 0 indicating any table size that can fit the recipe. Requires greater than or equal to 0 and less than or equal to 4. (Default `0`).

        ```groovy
        tier(int)
        tierAny()
        tierBasic()
        tierElite()
        tierAdvanced()
        tierUltimate()
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
        mods.extendedcrafting.tablecrafting.shapedBuilder()
            .output(item('minecraft:stone') * 64)
            .matrix('DLLLLLDDD',
                    '  DNIGIND',
                    'DDDNIGIND',
                    '  DLLLLLD')
            .key('D', item('minecraft:diamond'))
            .key('L', item('minecraft:redstone'))
            .key('N', item('minecraft:stone'))
            .key('I', item('minecraft:iron_ingot'))
            .key('G', item('minecraft:gold_ingot'))
            .tierUltimate()
            .register()

        mods.extendedcrafting.tablecrafting.shapedBuilder()
            .tierAdvanced()
            .output(item('minecraft:stone') * 8)
            .matrix('BXX')
            .mirrored()
            .key('B', item('minecraft:stone'))
            .key('X', item('minecraft:gold_ingot'))
            .register()

        mods.extendedcrafting.tablecrafting.shapedBuilder()
            .tierAny()
            .output(item('minecraft:diamond'))
            .matrix('BXXXBX')
            .mirrored()
            .key('B', item('minecraft:stone'))
            .key('X', item('minecraft:gold_ingot'))
            .register()

        mods.extendedcrafting.tablecrafting.shapedBuilder()
            .matrix([[item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')]])
            .output(item('minecraft:gold_ingot') * 64)
            .tier(4)
            .register()

        mods.extendedcrafting.tablecrafting.shapedBuilder()
            .matrix([[item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')],
                    [item('minecraft:gold_ingot'), item('minecraft:gold_ingot'), item('minecraft:gold_ingot')]])
            .output(item('minecraft:gold_ingot') * 64)
            .register()
        ```

???+ Abstract "mods.extendedcrafting.tablecrafting.shapelessBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy List<IIngredient>`. Sets the items required for the recipe. Requires greater than or equal to 1 and less than or equal to 81.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStack`. Sets the item output. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy int`. Sets the tier of table required, with 0 indicating any table size that can fit the recipe. Requires greater than or equal to 0 and less than or equal to 4. (Default `0`).

        ```groovy
        tier(int)
        tierAny()
        tierBasic()
        tierElite()
        tierAdvanced()
        tierUltimate()
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
        mods.extendedcrafting.tablecrafting.shapelessBuilder()
            .output(item('minecraft:stone') * 64)
            .input(item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'), item('minecraft:stone'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.extendedcrafting.tablecrafting.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.extendedcrafting.tablecrafting.removeAll()
    ```

???+ Example
    ```groovy
    mods.extendedcrafting.tablecrafting.removeByOutput(item('extendedcrafting:singularity_ultimate'))
    mods.extendedcrafting.tablecrafting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.extendedcrafting.tablecrafting.streamRecipes()
    ```
