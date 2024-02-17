---
title: "Grinder"
description: "Converts an item into one item, with up to two additional items as chance byproducts after a number of turns."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/appliedenergistics2/Grinder.java"
---

# Grinder (Applied Energistics 2)

## Description

Converts an item into one item, with up to two additional items as chance byproducts after a number of turns.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="3"
mods.ae2.grinder
mods.ae2.Grinder
mods.appliedenergistics2.grinder/*(1)!*/
mods.appliedenergistics2.Grinder
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Grinder also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.appliedenergistics2.grinder.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 1 and less than or equal to 3.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. Sets the number of turns of the Hand Crank are required. Requires greater than 0. (Default `0`).

        ```groovy
        turns(int)
        ```

    - `#!groovy float`. Sets the chance of the second output item being output. Requires greater than or equal to 0 and less than or equal to 1. (Default `1.0f`).

        ```groovy
        chance(float, float)
        chance1(float)
        ```

    - `#!groovy float`. Sets the chance of the third output item being output. Requires greater than or equal to 0 and less than or equal to 1. (Default `1.0f`).

        ```groovy
        chance(float, float)
        chance2(float)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `appeng.api.features.IGrinderRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.appliedenergistics2.grinder.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:diamond'), item('minecraft:gold_ingot'), item('minecraft:diamond'))
            .turns(1)
            .chance1(0.5)
            .chance2(0.3)
            .register()

        mods.appliedenergistics2.grinder.recipeBuilder()
            .input(item('minecraft:stone'))
            .output(item('minecraft:clay') * 4)
            .turns(10)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.appliedenergistics2.grinder.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.appliedenergistics2.grinder.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.appliedenergistics2.grinder.removeAll()
    ```

???+ Example
    ```groovy
    mods.appliedenergistics2.grinder.removeByInput(item('minecraft:gold_ingot'))
    mods.appliedenergistics2.grinder.removeByOutput(item('minecraft:quartz'))
    mods.appliedenergistics2.grinder.removeAll()
    ```
