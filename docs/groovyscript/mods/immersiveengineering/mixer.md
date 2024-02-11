---
title: "Mixer"
description: "Converts any number of input itemstacks and a fluidstack into an output fluidstack, consuming power."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/Mixer.java"
---

# Mixer (Immersive Engineering)

## Description

Converts any number of input itemstacks and a fluidstack into an output fluidstack, consuming power.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="3"
mods.ie.mixer
mods.ie.Mixer
mods.immersiveengineering.mixer/*(1)!*/
mods.immersiveengineering.Mixer
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `fluidOutput`, `fluidInput`, `energy`, `itemInput`:

    ```groovy
    mods.immersiveengineering.mixer.add(FluidStack, FluidStack, int, List<IIngredient>)
    ```


### Recipe Builder

Just like other recipe types, the Mixer also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.mixer.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to Integer.MAX_VALUE.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 1.

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid outputs of the recipe. Requires exactly 1.

        ```groovy
        fluidOutput(FluidStack)
        fluidOutput(FluidStack...)
        fluidOutput(Collection<FluidStack>)
        ```

    - `#!groovy int`. Sets the amount of power consumed to complete the recipe. (Default `0`).

        ```groovy
        energy(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.MixerRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.mixer.recipeBuilder()
            .input(item('minecraft:diamond'), ore('ingotGold'), ore('ingotGold'), ore('ingotGold'))
            .fluidInput(fluid('water'))
            .fluidOutput(fluid('lava'))
            .energy(100)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.mixer.removeByInput(FluidStack, IIngredient...)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.mixer.removeByInput(IIngredient...)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.mixer.removeByOutput(FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.mixer.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.mixer.removeByInput(fluid('water'), item('minecraft:speckled_melon'))
    mods.immersiveengineering.mixer.removeByInput(item('minecraft:sand'), item('minecraft:sand'), item('minecraft:clay_ball'), item('minecraft:gravel'))
    mods.immersiveengineering.mixer.removeByOutput(fluid('potion').withNbt([Potion:'minecraft:night_vision']))
    mods.immersiveengineering.mixer.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.mixer.streamRecipes()
    ```
