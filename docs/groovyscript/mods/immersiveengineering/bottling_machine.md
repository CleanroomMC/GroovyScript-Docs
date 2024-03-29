---
title: "Bottling Machine"
description: "Converts an input itemstack and fluidstack into an output itemstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/BottlingMachine.java"
---

# Bottling Machine (Immersive Engineering)

## Description

Converts an input itemstack and fluidstack into an output itemstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="7"
mods.ie.bottling_machine
mods.ie.bottlingmachine
mods.ie.bottlingMachine
mods.ie.BottlingMachine
mods.ie.bottling
mods.ie.Bottling
mods.immersiveengineering.bottling_machine/*(1)!*/
mods.immersiveengineering.bottlingmachine
mods.immersiveengineering.bottlingMachine
mods.immersiveengineering.BottlingMachine
mods.immersiveengineering.bottling
mods.immersiveengineering.Bottling
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `fluidInput`:

    ```groovy
    mods.immersiveengineering.bottling_machine.add(ItemStack, IIngredient, FluidStack)
    ```


### Recipe Builder

Just like other recipe types, the Bottling Machine also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.bottling_machine.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

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

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.BottlingMachineRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.bottling_machine.recipeBuilder()
            .input(item('minecraft:diamond'))
            .fluidInput(fluid('water'))
            .output(item('minecraft:clay'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.bottling_machine.removeByInput(ItemStack, FluidStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.bottling_machine.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.bottling_machine.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.bottling_machine.removeByInput(item('minecraft:sponge'), fluid('water') * 1000)
    mods.immersiveengineering.bottling_machine.removeByOutput(item('minecraft:potion').withNbt([Potion:'minecraft:mundane']))
    mods.immersiveengineering.bottling_machine.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.bottling_machine.streamRecipes()
    ```
