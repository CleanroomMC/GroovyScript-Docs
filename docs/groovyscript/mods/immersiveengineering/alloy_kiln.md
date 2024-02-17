---
title: "Alloy Kiln"
description: "Converts two input itemstacks into an output itemstack, consuming fuel (based on burn time)."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/AlloyKiln.java"
---

# Alloy Kiln (Immersive Engineering)

## Description

Converts two input itemstacks into an output itemstack, consuming fuel (based on burn time).

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.ie.alloy_kiln
mods.ie.alloykiln
mods.ie.alloyKiln
mods.ie.AlloyKiln
mods.immersiveengineering.alloy_kiln/*(1)!*/
mods.immersiveengineering.alloykiln
mods.immersiveengineering.alloyKiln
mods.immersiveengineering.AlloyKiln
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input0`, `input1`, `time`:

    ```groovy
    mods.immersiveengineering.alloy_kiln.add(ItemStack, IIngredient, IIngredient, int)
    ```


### Recipe Builder

Just like other recipe types, the Alloy Kiln also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.alloy_kiln.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 2.

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

    - `#!groovy int`. Sets the time in ticks the recipe takes to process. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        time(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.AlloyRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.alloy_kiln.recipeBuilder()
            .input(item('minecraft:diamond'), ore('ingotGold'))
            .output(item('minecraft:clay'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.alloy_kiln.removeByInput(ItemStack, ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.alloy_kiln.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.alloy_kiln.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.alloy_kiln.removeByInput(item('minecraft:gold_ingot'), item('immersiveengineering:metal:3'))
    mods.immersiveengineering.alloy_kiln.removeByOutput(item('immersiveengineering:metal:6'))
    mods.immersiveengineering.alloy_kiln.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.alloy_kiln.streamRecipes()
    ```
