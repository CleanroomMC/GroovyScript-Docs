---
title: "Elven Trade"
description: "Convert in any number of item inputs into an item output."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/ElvenTrade.java"
---

# Elven Trade (Botania)

## Description

Convert in any number of item inputs into an item output.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.ElvenTrade
mods.botania.elventrade/*(1)!*/
mods.botania.elvenTrade
mods.botania.elven_trade
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `inputs`:

    ```groovy
    mods.botania.elventrade.add(ItemStack, IIngredient[])
    ```

- Adds recipes in the format `output`, `inputs`:

    ```groovy
    mods.botania.elventrade.add(ItemStack[], IIngredient[])
    ```


### Recipe Builder

Just like other recipe types, the Elven Trade also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.botania.elventrade.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to 99. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 1 and less than or equal to 99. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `vazkii.botania.api.recipe.RecipeElvenTrade`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.botania.elventrade.recipeBuilder()
            .input(ore('ingotGold'), ore('ingotIron'))
            .output(item('botania:manaresource:7'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.elventrade.removeByInputs(IIngredient...)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.elventrade.removeByOutputs(ItemStack...)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.elventrade.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.elventrade.removeByInputs(ore('ingotManasteel'))
    mods.botania.elventrade.removeByOutputs(item('botania:dreamwood'))
    mods.botania.elventrade.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.elventrade.streamRecipes()
    ```
