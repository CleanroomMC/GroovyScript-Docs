---
title: "Sawmill"
description: "Converts an input itemstack into an output itemstack, with an optional additional output."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/Sawmill.java"
---

# Sawmill (Mekanism)

## Description

Converts an input itemstack into an output itemstack, with an optional additional output.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.Sawmill
mods.mekanism.sawmill/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `ingredient`, `output`, `secondary`, `chance`:

    ```groovy
    mods.mekanism.sawmill.add(IIngredient, ItemStack, ItemStack, double)
    ```

???+ Example
    ```groovy
    mods.mekanism.sawmill.add(item('minecraft:diamond_block'), item('minecraft:diamond') * 9, item('minecraft:clay_ball'), 0.7)
    ```

### Recipe Builder

Just like other recipe types, the Sawmill also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.sawmill.recipeBuilder()"
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

    - `#!groovy ItemStack`. Sets the extra itemstack produced by the recipe. (Default `ItemStack.EMPTY`).

        ```groovy
        ```

    - `#!groovy double`. Sets the chance the extra itemstack has to be produced. Requires greater than or equal to 0 and less than or equal to 1. (Default `1.0`).

        ```groovy
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.SawmillRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.sawmill.recipeBuilder()
            .input(item('minecraft:diamond_block'))
            .output(item('minecraft:diamond') * 9)
            .extra(item('minecraft:clay_ball'))
            .register()
        ```



## Removing Recipes

- Adds recipes in the format `ingredient`, `output`:

    ```groovy
    mods.mekanism.sawmill.add(IIngredient, ItemStack)
    ```

- Adds recipes in the format `ingredient`, `output`, `secondary`:

    ```groovy
    mods.mekanism.sawmill.add(IIngredient, ItemStack, ItemStack)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.sawmill.removeByInput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.sawmill.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.sawmill.removeByInput(item('minecraft:ladder'))
    mods.mekanism.sawmill.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.sawmill.streamRecipes()
    ```
