---
title: "Brew Recipe"
description: "Converts a non-infused Managlass Vial, Alfglass Flask, Incense Stick, or Tainted Blood Pendant into one infused to hold the given brew at the cost of item inputs and mana."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/BrewRecipe.java"
---

# Brew Recipe (Botania)

## Description

Converts a non-infused Managlass Vial, Alfglass Flask, Incense Stick, or Tainted Blood Pendant into one infused to hold the given brew at the cost of item inputs and mana.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.BrewRecipe
mods.botania.brewrecipe/*(1)!*/
mods.botania.brewRecipe
mods.botania.brew_recipe
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Brew Recipe also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.botania.brewrecipe.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to 6.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy Brew`. Sets the brew the recipe is being created for. Requires not null.

        ```groovy
        brew(Brew)
        output(Brew)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `vazkii.botania.api.recipe.RecipeBrew`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.botania.brewrecipe.recipeBuilder()
            .input(item('minecraft:clay'), ore('ingotGold'), ore('gemDiamond'))
            .brew(brew('absorption'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.brewrecipe.removeByInput(IIngredient...)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.botania.brewrecipe.removeByInputs(IIngredient...)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.brewrecipe.removeByOutput(Brew)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.brewrecipe.removeByOutput(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.brewrecipe.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.brewrecipe.removeByInput(item('minecraft:iron_ingot'))
    mods.botania.brewrecipe.removeByOutput(brew('allure'))
    mods.botania.brewrecipe.removeByOutput('speed')
    mods.botania.brewrecipe.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.brewrecipe.streamRecipes()
    ```
