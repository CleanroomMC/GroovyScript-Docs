---
title: "Mechanical Squeezer"
description: "Takes an item and can give up to 3 chanced item outputs and a fluid."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/integrateddynamics/MechanicalSqueezer.java"
---

# Mechanical Squeezer (Integrated Dynamics)

## Description

Takes an item and can give up to 3 chanced item outputs and a fluid.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.id.mechanical_squeezer
mods.id.mechanicalsqueezer
mods.id.mechanicalSqueezer
mods.id.MechanicalSqueezer
mods.integrateddynamics.mechanical_squeezer/*(1)!*/
mods.integrateddynamics.mechanicalsqueezer
mods.integrateddynamics.mechanicalSqueezer
mods.integrateddynamics.MechanicalSqueezer
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Mechanical Squeezer also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.integrateddynamics.mechanical_squeezer.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid outputs of the recipe. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        fluidOutput(FluidStack)
        fluidOutput(FluidStack...)
        fluidOutput(Collection<FluidStack>)
        ```

    - `#!groovy boolean`. Sets if the recipe is added to the basic (Squeezer) machine. (Default `false`).

        ```groovy
        basic()
        basic(boolean)
        ```

    - `#!groovy List<IngredientRecipeComponent>`. Sets the possible item outputs and chance of those outputs being dropped. Requires greater than or equal to 0 and less than or equal to 3.

        ```groovy
        output(ItemStack)
        output(ItemStack, float)
        ```

    - `#!groovy int`. Sets the time in ticks the recipe takes to process in the Mechanical Squeezer, has no effect on the Squeezer. (Default `10`).

        ```groovy
        duration(int)
        ```

    - `#!groovy boolean`. Sets if the recipe is added to the mechanical (Mechanical Squeezer) machine. (Default `true`).

        ```groovy
        mechanical()
        mechanical(boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `org.cyclops.cyclopscore.recipe.custom.api.IRecipe<org.cyclops.cyclopscore.recipe.custom.component.IngredientRecipeComponent, org.cyclops.cyclopscore.recipe.custom.component.IngredientsAndFluidStackRecipeComponent, org.cyclops.cyclopscore.recipe.custom.component.DummyPropertiesComponent>`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.integrateddynamics.mechanical_squeezer.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay') * 16, 0.9F)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.integrateddynamics.mechanical_squeezer.removeByInput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.integrateddynamics.mechanical_squeezer.removeAll()
    ```

???+ Example
    ```groovy
    mods.integrateddynamics.mechanical_squeezer.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.integrateddynamics.mechanical_squeezer.streamRecipes()
    ```
