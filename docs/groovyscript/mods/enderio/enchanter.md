---
title: "Enchanter"
description: "Convert an input itemstack, player xp, and either a written book and lapis or a custom alternative into an enchanted book."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/enderio/Enchanter.java"
---

# Enchanter (Ender IO)

## Description

Convert an input itemstack, player xp, and either a written book and lapis or a custom alternative into an enchanted book.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.enderio.Enchanter
mods.enderio.enchanter/*(1)!*/
mods.eio.Enchanter
mods.eio.enchanter
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `enchantment`, `input`:

    ```groovy
    mods.enderio.enchanter.add(Enchantment, IIngredient)
    ```


### Recipe Builder

Just like other recipe types, the Enchanter also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.enderio.enchanter.recipeBuilder()"
    - `#!groovy IIngredient`. Sets the item used in the book slot. Requires not null. (Default `item('minecraft:writable_book')`).

        ```groovy
        customBook(IIngredient)
        ```

    - `#!groovy IIngredient`. Sets the key item to create the enchantment. Requires not null.

        ```groovy
        input(IIngredient)
        ```

    - `#!groovy IIngredient`. Sets the item used in the lapis slot. Requires not null. (Default `ore('gemLapis')`).

        ```groovy
        customLapis(IIngredient)
        ```

    - `#!groovy int`. Sets the amount of the input item used to create a single level of enchantment. Requires greater than 0. (Default `0`).

        ```groovy
        amountPerLevel(int)
        ```

    - `#!groovy Enchantment`. Sets the enchantment applied to the output book. Requires not null.

        ```groovy
        enchantment(Enchantment)
        ```

    - `#!groovy double`. Sets the experience cost multiplier per enchantment level created. (Default `1`).

        ```groovy
        xpCostMultiplier(double)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `crazypants.enderio.base.recipe.enchanter.EnchanterRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.enderio.enchanter.recipeBuilder()
            .enchantment(enchantment('minecraft:unbreaking'))
            .input(item('minecraft:diamond'))
            .register()

        mods.enderio.enchanter.recipeBuilder()
            .enchantment(enchantment('minecraft:sharpness'))
            .input(item('minecraft:clay'))
            .amountPerLevel(3)
            .xpCostMultiplier(2)
            .customBook(item('minecraft:book'))
            .customLapis(item('minecraft:diamond'))
            .register()
        ```



## Removing Recipes

- Removes entries by enchantment:

    ```groovy
    mods.enderio.enchanter.remove(Enchantment)
    ```

- Removes all registered recipes:

    ```groovy
    mods.enderio.enchanter.removeAll()
    ```

???+ Example
    ```groovy
    mods.enderio.enchanter.remove(enchantment('minecraft:mending'))
    mods.enderio.enchanter.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.enderio.enchanter.streamRecipes()
    ```
