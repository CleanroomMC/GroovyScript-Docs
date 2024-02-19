---
title: "Crude Drying Rack"
description: "Converts an item over time into a new one"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/pyrotech/CrudeDryingRack.java"
---

# Crude Drying Rack (Pyrotech)

## Description

Converts an item over time into a new one

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.pyrotech.crude_drying_rack/*(1)!*/
mods.pyrotech.crudedryingrack
mods.pyrotech.crudeDryingRack
mods.pyrotech.CrudeDryingRack
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `name`, `input`, `output`, `dryTime`:

    ```groovy
    mods.pyrotech.crude_drying_rack.add(String, IIngredient, ItemStack, int)
    ```

???+ Example
    ```groovy
    mods.pyrotech.crude_drying_rack.add('apple_to_dirt', item('minecraft:apple'), item('minecraft:dirt'), 1200)
    ```

### Recipe Builder

Just like other recipe types, the Crude Drying Rack also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.pyrotech.crude_drying_rack.recipeBuilder()"
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
        dryTime(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.codetaylor.mc.pyrotech.modules.tech.basic.recipe.CrudeDryingRackRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.pyrotech.crude_drying_rack.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:emerald'))
            .dryTime(260)
            .name('diamond_to_emerald_crude_drying_rack')
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.pyrotech.crude_drying_rack.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.pyrotech.crude_drying_rack.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.pyrotech.crude_drying_rack.removeAll()
    ```

???+ Example
    ```groovy
    mods.pyrotech.crude_drying_rack.removeByInput(item('minecraft:wheat'))
    mods.pyrotech.crude_drying_rack.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.pyrotech.crude_drying_rack.streamRecipes()
    ```
