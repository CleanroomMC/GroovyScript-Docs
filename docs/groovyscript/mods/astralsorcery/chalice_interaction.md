---
title: "Chalice Interaction"
description: "When two chalices containing different fluids are placed nearby, fluid may be consumed to produce an output itemstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/ChaliceInteraction.java"
---

# Chalice Interaction (Astral Sorcery)

## Description

When two chalices containing different fluids are placed nearby, fluid may be consumed to produce an output itemstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.astral_sorcery.chalice_interaction
mods.astral_sorcery.chaliceinteraction
mods.astral_sorcery.chaliceInteraction
mods.astral_sorcery.ChaliceInteraction
mods.astralsorcery.chalice_interaction/*(1)!*/
mods.astralsorcery.chaliceinteraction
mods.astralsorcery.chaliceInteraction
mods.astralsorcery.ChaliceInteraction
mods.astral.chalice_interaction
mods.astral.chaliceinteraction
mods.astral.chaliceInteraction
mods.astral.ChaliceInteraction
mods.as.chalice_interaction
mods.as.chaliceinteraction
mods.as.chaliceInteraction
mods.as.ChaliceInteraction
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds entries in the format `probability`, `component1`, `component2`, `action`:

    ```groovy
    mods.astralsorcery.chalice_interaction.add(int, FluidStack, FluidStack, LiquidInteraction.FluidInteractionAction)
    ```


### Recipe Builder

Just like other recipe types, the Chalice Interaction also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.astralsorcery.chalice_interaction.recipeBuilder()"
    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 2.

        ```groovy
        component(FluidStack)
        component(FluidStack, float)
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(FluidStack, float)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 0.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(ItemStack, int)
        output(Collection<ItemStack>)
        result(ItemStack)
        result(ItemStack, int)
        ```

    - `#!groovy FloatArrayList`. Sets the chance to consume fluids from the Chalices. Requires exactly 2.

        ```groovy
        component(FluidStack)
        component(FluidStack, float)
        fluidInput(FluidStack)
        fluidInput(FluidStack, float)
        ```

    - `#!groovy IntArrayList`. Sets the chance a given output will occur among all possible combinations of the fluid.. Requires greater than 0.

        ```groovy
        output(ItemStack)
        output(ItemStack, int)
        result(ItemStack)
        result(ItemStack, int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `hellfirepvp.astralsorcery.common.base.LiquidInteraction`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.chalice_interaction.recipeBuilder()
            .output(item('astralsorcery:blockmarble'))
            .fluidInput(fluid('water') * 10)
            .fluidInput(fluid('astralsorcery.liquidstarlight') * 30)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.chalice_interaction.removeByInput(Fluid)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.chalice_interaction.removeByInput(Fluid, Fluid)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.chalice_interaction.removeByInput(FluidStack)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.astralsorcery.chalice_interaction.removeByInput(FluidStack, FluidStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.astralsorcery.chalice_interaction.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.chalice_interaction.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.chalice_interaction.removeByInput(fluid('astralsorcery.liquidstarlight'))
    mods.astralsorcery.chalice_interaction.removeByInput(fluid('water'), fluid('lava'))
    mods.astralsorcery.chalice_interaction.removeByOutput(item('minecraft:ice'))
    mods.astralsorcery.chalice_interaction.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.chalice_interaction.streamRecipes()
    ```
