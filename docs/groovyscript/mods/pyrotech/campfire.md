---
title: "Campfire"
description: "Can cook food"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/pyrotech/Campfire.java"
---

# Campfire (Pyrotech)

## Description

Can cook food

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.pyrotech.campfire/*(1)!*/
mods.pyrotech.Campfire
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `name`, `input`, `output`, `duration`:

    ```groovy
    mods.pyrotech.campfire.add(String, IIngredient, ItemStack, int)
    ```

???+ Example
    ```groovy
    mods.pyrotech.campfire.add('apple_to_dirt', item('minecraft:apple'), item('minecraft:dirt'), 1000)
    ```

### Recipe Builder

Just like other recipe types, the Campfire also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.pyrotech.campfire.recipeBuilder()"
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
        duration(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.codetaylor.mc.pyrotech.modules.tech.basic.recipe.CampfireRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.pyrotech.campfire.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:emerald'))
            .duration(400)
            .name('diamond_campfire_to_emerald')
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.pyrotech.campfire.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.pyrotech.campfire.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.pyrotech.campfire.removeAll()
    ```

???+ Example
    ```groovy
    mods.pyrotech.campfire.removeByInput(item('minecraft:porkchop'))
    mods.pyrotech.campfire.removeByOutput(item('minecraft:cooked_porkchop'))
    mods.pyrotech.campfire.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.pyrotech.campfire.streamRecipes()
    ```
