---
title: "Metal Press"
description: "Converts an input itemstack into an output itemstack, with a mold catalyst, consuming power."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/MetalPress.java"
---

# Metal Press (Immersive Engineering)

## Description

Converts an input itemstack into an output itemstack, with a mold catalyst, consuming power.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.ie.metal_press
mods.ie.metalpress
mods.ie.metalPress
mods.ie.MetalPress
mods.immersiveengineering.metal_press/*(1)!*/
mods.immersiveengineering.metalpress
mods.immersiveengineering.metalPress
mods.immersiveengineering.MetalPress
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `mold`, `energy`:

    ```groovy
    mods.immersiveengineering.metal_press.add(ItemStack, IIngredient, ItemStack, int)
    ```


### Recipe Builder

Just like other recipe types, the Metal Press also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.metal_press.recipeBuilder()"
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

    - `#!groovy ItemStack`. Sets the mold item placed on the top face of the Metal Press as a catalyst. Requires not empty.

        ```groovy
        mold(ItemStack)
        ```

    - `#!groovy int`. Sets the amount of power consumed to complete the recipe. (Default `0`).

        ```groovy
        energy(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.MetalPressRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.metal_press.recipeBuilder()
            .mold(item('minecraft:diamond'))
            .input(ore('ingotGold'))
            .output(item('minecraft:clay'))
            .energy(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.metal_press.removeByInput(ItemStack)
    ```

- Removes recipes with the given mold and input item, in the format `mold`, `input`:

    ```groovy
    mods.immersiveengineering.metal_press.removeByInput(ItemStack, ItemStack)
    ```

- Removes all recipes with the given mold:

    ```groovy
    mods.immersiveengineering.metal_press.removeByMold(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.metal_press.removeByOutput(ItemStack)
    ```

- Removes recipes with the given mold and output item, in the format `mold`, `output`:

    ```groovy
    mods.immersiveengineering.metal_press.removeByOutput(ItemStack, ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.metal_press.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.metal_press.removeByInput(item('minecraft:iron_ingot'))
    mods.immersiveengineering.metal_press.removeByInput(item('immersiveengineering:mold'), item('immersiveengineering:metal:8'))
    mods.immersiveengineering.metal_press.removeByMold(item('immersiveengineering:mold:4'))
    mods.immersiveengineering.metal_press.removeByOutput(item('immersiveengineering:material:2'))
    mods.immersiveengineering.metal_press.removeByOutput(item('immersiveengineering:mold'), item('immersiveengineering:metal:31'))
    mods.immersiveengineering.metal_press.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.metal_press.streamRecipes()
    ```
