---
title: "Barrel"
description: "Over time converts a fluid with four items into a new fluid"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/pyrotech/Barrel.java"
---

# Barrel (Pyrotech)

## Description

Over time converts a fluid with four items into a new fluid

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.pyrotech.barrel/*(1)!*/
mods.pyrotech.Barrel
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `name`, `input1`, `input2`, `input3`, `input4`, `fluidInput`, `fluidOutput`, `duration`:

    ```groovy
    mods.pyrotech.barrel.add(String, IIngredient, IIngredient, IIngredient, IIngredient, FluidStack, FluidStack, int)
    ```

???+ Example
    ```groovy
    mods.pyrotech.barrel.add('iron_dirt_water_to_lava', ore('ingotIron'), ore('ingotIron'), item('minecraft:dirt'), item('minecraft:dirt'), fluid('water'), fluid('lava'), 1000)
    ```

### Recipe Builder

Just like other recipe types, the Barrel also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.pyrotech.barrel.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 4.

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

    - `#!groovy FluidStackList`. Sets the fluid outputs of the recipe. Requires exactly 1.

        ```groovy
        fluidOutput(FluidStack)
        fluidOutput(FluidStack...)
        fluidOutput(Collection<FluidStack>)
        ```

    - `#!groovy int`. Sets the time required for the recipe to complete. Requires greater than or equal to 1. (Default `0`).

        ```groovy
        duration(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.codetaylor.mc.pyrotech.modules.tech.basic.recipe.BarrelRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.pyrotech.barrel.recipeBuilder()
            .input(item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:diamond'), item('minecraft:emerald'))
            .fluidInput(fluid('water') * 1000)
            .fluidOutput(fluid('amongium') * 1000)
            .duration(1000)
            .name('diamond_emerald_and_water_to_amongium')
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.pyrotech.barrel.removeByOutput(FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.pyrotech.barrel.removeAll()
    ```

???+ Example
    ```groovy
    mods.pyrotech.barrel.removeByOutput(fluid('freckleberry_wine') * 1000)
    mods.pyrotech.barrel.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.pyrotech.barrel.streamRecipes()
    ```
