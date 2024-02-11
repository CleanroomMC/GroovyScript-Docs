---
title: "Pyre"
description: "Converts 5 input items into the ouput after a period of time when the Pyre is lit on fire."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/Pyre.java"
---

# Pyre (Roots 3)

## Description

Converts 5 input items into the ouput after a period of time when the Pyre is lit on fire.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.roots.pyre/*(1)!*/
mods.roots.Pyre
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Pyre also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.pyre.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 5.

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

    - `#!groovy int`. Sets the XP given when the recipe finishes in levels. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        xp(int)
        levels(int)
        ```

    - `#!groovy int`. Sets the time in ticks for the recipe to process. (Default `200`).

        ```groovy
        time(int)
        burnTime(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.recipe.PyreCraftingRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.pyre.recipeBuilder()
            .name('clay_from_fire')
            .input(item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'),item('minecraft:stone'))
            .output(item('minecraft:clay'))
            .xp(5)
            .time(1)
            .register()

        mods.roots.pyre.recipeBuilder()
            .input(item('minecraft:gold_ingot'),item('minecraft:clay'),item('minecraft:clay'),item('minecraft:stone'),item('minecraft:stone'))
            .output(item('minecraft:diamond') * 32)
            .levels(5)
            .burnTime(1000)
            .register()
        ```



## Removing Recipes

- Removes the Pyre recipe with the given name:

    ```groovy
    mods.roots.pyre.removeByName(ResourceLocation)
    ```

- Removes the Pyre recipe with the given output itemstack:

    ```groovy
    mods.roots.pyre.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.pyre.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.pyre.removeByName(resource('roots:infernal_bulb'))
    mods.roots.pyre.removeByOutput(item('minecraft:gravel'))
    mods.roots.pyre.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.pyre.streamRecipes()
    ```
