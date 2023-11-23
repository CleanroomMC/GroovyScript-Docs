---
title: "Miniaturization"
description: "Consumes a 3d structure in-world based on keys when an item is thrown into the field."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/compactmachines/Miniaturization.java"
---

# Miniaturization (Compact Machines 3)

## Description

Consumes a 3d structure in-world based on keys when an item is thrown into the field.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="4"
mods.compactmachines.Miniaturization
mods.compactmachines.miniaturization
mods.compactmachines3.Miniaturization
mods.compactmachines3.miniaturization/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Miniaturization also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.compactmachines3.miniaturization.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy List<List<String>>`. Sets the structure in order of a descending Y-axis. (Default `null`).

        ```groovy
        layer(String...)
        layer(List<String>)
        shape(List<List<String>>)
        ```

    - `#!groovy int`. Sets the time in ticks the recipe takes to process before dropping the output item.

        ```groovy
        ticks(int)
        ```

    - `#!groovy Char2ObjectOpenHashMap<Miniaturization.RecipeBuilder.ReferenceValues>`. Sets the IBlockState, specific NBT, if the metadata is checked, and a representative itemstack for each `char` key.

        ```groovy
        key(String, IBlockState)
        key(String, IBlockState, boolean)
        key(String, IBlockState, NBTTagCompound)
        key(String, IBlockState, NBTTagCompound, boolean)
        key(String, IBlockState, NBTTagCompound, boolean, ItemStack)
        ```

    - `#!groovy boolean`. Sets if the recipe does not have to test all 4 rotations to determine if the multiblock is valid.

        ```groovy
        symmetrical()
        symmetrical(boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `org.dave.compactmachines3.miniaturization.MultiblockRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.compactmachines3.miniaturization.recipeBuilder()
            .name('diamond_rectangle')
            .input(item('minecraft:clay'))
            .output(item('minecraft:clay'))
            .symmetrical()
            .ticks(10)
            .shape([['www',
                     'www']])
            .key('w', blockstate('minecraft:diamond_block'))
            .register()

        mods.compactmachines3.miniaturization.recipeBuilder()
            .name('groovy_rocket')
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay') * 64)
            .symmetrical()
            .ticks(5400)
            .key('a', blockstate('minecraft:stained_glass:0'))
            .key('b', blockstate('minecraft:stained_glass:1'))
            .key('c', blockstate('minecraft:stained_glass:2'))
            .key('d', blockstate('minecraft:stained_glass:3'))
            .key('e', blockstate('minecraft:diamond_block'))
            .key('f', blockstate('minecraft:stained_glass:5'))
            .key('g', blockstate('minecraft:stained_glass:6'))
            .layer('       ',
                   '       ',
                   '   a   ',
                   '  aaa  ',
                   '   a   ',
                   '       ',
                   '       ')
            .layer('       ',
                   '   b   ',
                   '  aaa  ',
                   ' baaab ',
                   '  aaa  ',
                   '   b   ',
                   '       ')
            .layer('       ',
                   '   c   ',
                   '  cac  ',
                   ' caeac ',
                   '  cac  ',
                   '   c   ',
                   '       ')
            .layer('       ',
                   '   a   ',
                   '  aaa  ',
                   ' aaeaa ',
                   '  aaa  ',
                   '   a   ',
                   '       ')
            .layer('       ',
                   '   a   ',
                   '  aaa  ',
                   ' aaeaa ',
                   '  aaa  ',
                   '   a   ',
                   '       ')
            .layer('       ',
                   '   a   ',
                   '  aaa  ',
                   ' aaeaa ',
                   '  aaa  ',
                   '   a   ',
                   '       ')
            .layer('       ',
                   '   g   ',
                   '  cac  ',
                   ' caeac ',
                   '  cac  ',
                   '   f   ',
                   '       ')
            .layer('       ',
                   '   a   ',
                   '  aaa  ',
                   ' aaeaa ',
                   '  aaa  ',
                   '   a   ',
                   '       ')
            .layer('       ',
                   '   a   ',
                   '  aaa  ',
                   ' aaeaa ',
                   '  aaa  ',
                   '   a   ',
                   '       ')
            .layer('       ',
                   '   a   ',
                   '  aaa  ',
                   ' aaeaa ',
                   '  aaa  ',
                   '   a   ',
                   '       ')
            .layer('       ',
                   '   c   ',
                   '  cac  ',
                   ' caeac ',
                   '  cac  ',
                   '   c   ',
                   '       ')
            .layer('       ',
                   '   a   ',
                   '  aaa  ',
                   ' aaaaa ',
                   '  aaa  ',
                   '   a   ',
                   '       ')
            .layer('   a   ',
                   '  ccc  ',
                   ' cdddc ',
                   'acdddca',
                   ' cdddc ',
                   '  ccc  ',
                   '   a   ')
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.compactmachines3.miniaturization.removeByCatalyst(ItemStack)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.compactmachines3.miniaturization.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.compactmachines3.miniaturization.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.compactmachines3.miniaturization.removeAll()
    ```

???+ Example
    ```groovy
    mods.compactmachines3.miniaturization.removeByCatalyst(item('minecraft:redstone'))
    mods.compactmachines3.miniaturization.removeByInput(item('minecraft:ender_pearl'))
    mods.compactmachines3.miniaturization.removeByOutput(item('compactmachines3:machine:3'))
    mods.compactmachines3.miniaturization.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.compactmachines3.miniaturization.streamRecipes()
    ```
