---
title: "Compost Bin"
description: "Can convert multiple items into a new one when its full"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/pyrotech/CompostBin.java"
---

# Compost Bin (Pyrotech)

## Description

Can convert multiple items into a new one when its full

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.pyrotech.compost_bin/*(1)!*/
mods.pyrotech.compostbin
mods.pyrotech.compostBin
mods.pyrotech.CompostBin
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `name`, `input`, `output`, `compostValue`:

    ```groovy
    mods.pyrotech.compost_bin.add(String, IIngredient, ItemStack, int)
    ```

???+ Example
    ```groovy
    mods.pyrotech.compost_bin.add('iron_to_clay2', ore('ingotIron') * 5, item('minecraft:clay_ball') * 20, 2)
    ```

### Recipe Builder

Just like other recipe types, the Compost Bin also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.pyrotech.compost_bin.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

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

    - `#!groovy int`. Sets how much the items fills the bin. Requires greater than or equal to 1. (Default `0`).

        ```groovy
        compostValue(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.codetaylor.mc.pyrotech.modules.tech.basic.recipe.CompostBinRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.pyrotech.compost_bin.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:emerald') * 4)
            .compostValue(25)
            .name('diamond_to_emerald_compost_bin')
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.pyrotech.compost_bin.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.pyrotech.compost_bin.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.pyrotech.compost_bin.removeAll()
    ```

???+ Example
    ```groovy
    mods.pyrotech.compost_bin.removeByInput(item('minecraft:golden_carrot'))
    mods.pyrotech.compost_bin.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.pyrotech.compost_bin.streamRecipes()
    ```
