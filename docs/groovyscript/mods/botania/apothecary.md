---
title: "Petal Apothecary"
description: "Converts item inputs into an item output consuming water and a seed."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/Apothecary.java"
---

# Petal Apothecary (Botania)

## Description

Converts item inputs into an item output consuming water and a seed.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.Apothecary
mods.botania.apothecary/*(1)!*/
mods.botania.PetalApothecary
mods.botania.petalapothecary
mods.botania.petalApothecary
mods.botania.petal_apothecary
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `inputs`:

    ```groovy
    mods.botania.apothecary.add(ItemStack, IIngredient...)
    ```


### Recipe Builder

Just like other recipe types, the Petal Apothecary also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.botania.apothecary.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to 20. (Default `null`).

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

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `vazkii.botania.api.recipe.RecipePetals`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.botania.apothecary.recipeBuilder()
            .input(ore('blockGold'), ore('ingotIron'), item('minecraft:apple'))
            .output(item('minecraft:golden_apple'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.apothecary.removeByInput(IIngredient...)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.apothecary.removeByInputs(IIngredient...)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.apothecary.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.apothecary.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.apothecary.removeByInput(ore('runeFireB'))
    mods.botania.apothecary.removeByInputs(ore('petalYellow'), ore('petalBrown'))
    mods.botania.apothecary.removeByOutput(item('botania:specialflower').withNbt(['type': 'puredaisy']))
    mods.botania.apothecary.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.apothecary.streamRecipes()
    ```
