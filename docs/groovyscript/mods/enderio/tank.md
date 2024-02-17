---
title: "Tank"
description: "Converts an input itemstack into an output fluidstack with an optional output itemstack in drain mode, or converts an input itemstack and fluidstack into an output itemstack in fill mode."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/enderio/Tank.java"
---

# Tank (Ender IO)

## Description

Converts an input itemstack into an output fluidstack with an optional output itemstack in drain mode, or converts an input itemstack and fluidstack into an output itemstack in fill mode.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.enderio.tank/*(1)!*/
mods.enderio.Tank
mods.eio.tank
mods.eio.Tank
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds drain recipes in the format `input`, `outputFluid`, `output`, and autogenerates a recipe name:

    ```groovy
    mods.enderio.tank.addDrain(IIngredient, FluidStack, ItemStack)
    ```

- Adds drain recipes in the format `recipeName`, `input`, `outputFluid`, `output`:

    ```groovy
    mods.enderio.tank.addDrain(String, IIngredient, FluidStack, ItemStack)
    ```

- Adds fill recipes in the format `input`, `inputFluid`, `output`, and autogenerates a recipe name:

    ```groovy
    mods.enderio.tank.addFill(IIngredient, FluidStack, ItemStack)
    ```

- Adds fill recipes in the format `recipeName`, `input`, `inputFluid`, `output`:

    ```groovy
    mods.enderio.tank.addFill(String, IIngredient, FluidStack, ItemStack)
    ```


### Recipe Builder

Just like other recipe types, the Tank also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.enderio.tank.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid outputs of the recipe. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        fluidOutput(FluidStack)
        fluidOutput(FluidStack...)
        fluidOutput(Collection<FluidStack>)
        ```

    - `#!groovy boolean`. Sets if the recipe is filling or emptying. (Default `false`).

        ```groovy
        fill()
        drain()
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `crazypants.enderio.base.recipe.tank.TankMachineRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.enderio.tank.recipeBuilder()
            .drain()
            .input(item('minecraft:clay'))
            .output(item('minecraft:diamond'))
            .fluidInput(fluid('water') * 500)
            .register()

        mods.enderio.tank.recipeBuilder()
            .fill()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay'))
            .fluidOutput(fluid('water') * 500)
            .register()

        mods.enderio.tank.recipeBuilder()
            .drain()
            .input(item('minecraft:diamond'))
            .fluidInput(fluid('fire_water') * 8000)
            .register()

        mods.enderio.tank.recipeBuilder()
            .fill()
            .input(item('minecraft:diamond'))
            .fluidOutput(fluid('fire_water') * 8000)
            .register()
        ```



## Removing Recipes

- Removes drain recipe by `fluid`, `output`:

    ```groovy
    mods.enderio.tank.removeDrain(FluidStack, ItemStack)
    ```

- Removes drain recipe by `input`, `fluid`:

    ```groovy
    mods.enderio.tank.removeDrain(ItemStack, FluidStack)
    ```

- Removes fill recipe by `fluid`, `output`:

    ```groovy
    mods.enderio.tank.removeFill(FluidStack, ItemStack)
    ```

- Removes fill recipe by `input`, `fluid`:

    ```groovy
    mods.enderio.tank.removeFill(ItemStack, FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.enderio.tank.removeAll()
    ```

???+ Example
    ```groovy
    mods.enderio.tank.removeDrain(item('minecraft:experience_bottle'), fluid('xpjuice'))
    mods.enderio.tank.removeFill(item('minecraft:glass_bottle'), fluid('xpjuice'))
    mods.enderio.tank.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.enderio.tank.streamRecipes()
    ```
