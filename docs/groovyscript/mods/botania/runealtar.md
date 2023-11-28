---
title: "Rune Altar"
description: "Converts a items inputs into an item ouput at the cost of mana when a Livingrock item is thrown atop the altar and right clicked with a Wand of the Forest."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/RuneAltar.java"
---

# Rune Altar (Botania)

## Description

Converts a items inputs into an item ouput at the cost of mana when a Livingrock item is thrown atop the altar and right clicked with a Wand of the Forest.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.RuneAltar
mods.botania.runealtar/*(1)!*/
mods.botania.runeAltar
mods.botania.rune_altar
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `mana`, `inputs`:

    ```groovy
    mods.botania.runealtar.add(ItemStack, int, IIngredient...)
    ```


### Recipe Builder

Just like other recipe types, the Rune Altar also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.botania.runealtar.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. Requires that `input` IIngredients cannot contain Botania's Livingrock Item.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 1 and less than or equal to 2.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. Sets the mana cost of processing the recipe. Requires greater than or equal to 1. (Default `0`).

        ```groovy
        mana(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `vazkii.botania.api.recipe.RecipeRuneAltar`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.botania.runealtar.recipeBuilder()
            .input(ore('gemEmerald'), item('minecraft:apple'))
            .output(item('minecraft:diamond'))
            .mana(500)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.runealtar.removeByInput(IIngredient...)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.runealtar.removeByInputs(IIngredient...)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.runealtar.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.runealtar.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.runealtar.removeByInput(ore('runeEarthB'))
    mods.botania.runealtar.removeByInputs(ore('feather'), ore('string'))
    mods.botania.runealtar.removeByOutput(item('botania:rune:1'))
    mods.botania.runealtar.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.runealtar.streamRecipes()
    ```
