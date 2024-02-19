---
title: "Kiln"
description: "Converts an item into a new one by burning it. Has a chance to fail"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/pyrotech/Kiln.java"
---

# Kiln (Pyrotech)

## Description

Converts an item into a new one by burning it. Has a chance to fail

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.pyrotech.kiln/*(1)!*/
mods.pyrotech.Kiln
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `name`, `input`, `output`, `burnTime`, `failureChance`, `failureOutput`:

    ```groovy
    mods.pyrotech.kiln.add(String, IIngredient, ItemStack, int, float, Iterable<ItemStack>)
    ```

???+ Example
    ```groovy
    mods.pyrotech.kiln.add('clay_to_iron', item('minecraft:clay_ball') * 5, item('minecraft:iron_ingot'), 1200, 0.5f, [item('minecraft:dirt'), item('minecraft:cobblestone')])
    ```

### Recipe Builder

Just like other recipe types, the Kiln also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.pyrotech.kiln.recipeBuilder()"
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

    - `#!groovy int`. Sets the time required for the recipe to complete. Requires greater than or equal to 1. (Default `0`).

        ```groovy
        burnTime(int)
        ```

    - `#!groovy float`. Sets the chance to fail the recipe. Requires greater than or equal to 0. (Default `0.0f`).

        ```groovy
        failureChance(float)
        ```

    - `#!groovy ItemStackList`. .

        ```groovy
        failureOutput(ItemStack)
        failureOutput(ItemStack...)
        failureOutput(Iterable<ItemStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.codetaylor.mc.pyrotech.modules.tech.basic.recipe.KilnPitRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.pyrotech.kiln.recipeBuilder()
            .input(item('minecraft:iron_ingot'))
            .output(item('minecraft:gold_ingot'))
            .burnTime(400)
            .failureChance(1f)
            .failureOutput(item('minecraft:wheat'), item('minecraft:carrot'), item('minecraft:sponge'))
            .name('iron_to_gold_kiln_with_failure_items')
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.pyrotech.kiln.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.pyrotech.kiln.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.pyrotech.kiln.removeAll()
    ```

???+ Example
    ```groovy
    mods.pyrotech.kiln.removeByOutput(item('pyrotech:bucket_clay'))
    mods.pyrotech.kiln.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.pyrotech.kiln.streamRecipes()
    ```
