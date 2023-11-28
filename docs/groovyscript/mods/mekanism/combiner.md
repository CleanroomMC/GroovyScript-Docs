---
title: "Combiner"
description: "Combines an input itemstack with an extra itemstack to create an output itemstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/Combiner.java"
---

# Combiner (Mekanism)

## Description

Combines an input itemstack with an extra itemstack to create an output itemstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.Combiner
mods.mekanism.combiner/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `ingredient`, `extra`, `output`:

    ```groovy
    mods.mekanism.combiner.add(IIngredient, ItemStack, ItemStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.combiner.add(ore('gemQuartz') * 8, item('minecraft:netherrack'), item('minecraft:quartz_ore'))
    ```

### Recipe Builder

Just like other recipe types, the Combiner also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.combiner.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy ItemStack`. Sets the extra input item, defaults to Cobblestone. (Default `new ItemStack(Blocks.COBBLESTONE)`).

        ```groovy
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.CombinerRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.combiner.recipeBuilder()
            .input(ore('gemQuartz') * 8)
            .extra(item('minecraft:netherrack'))
            .output(item('minecraft:quartz_ore'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.combiner.removeByInput(IIngredient, ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.combiner.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.combiner.removeByInput(item('minecraft:flint'), item('minecraft:cobblestone'))
    mods.mekanism.combiner.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.combiner.streamRecipes()
    ```
