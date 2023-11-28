---
title: "Mechanical Drying Basin"
description: "Takes either an item or fluid input and gives either an item or fluid output after a duration."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/integrateddynamics/MechanicalDryingBasin.java"
---

# Mechanical Drying Basin (Integrated Dynamics)

## Description

Takes either an item or fluid input and gives either an item or fluid output after a duration.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.integrateddynamics.MechanicalDryingBasin
mods.integrateddynamics.mechanicaldryingbasin/*(1)!*/
mods.integrateddynamics.mechanicalDryingBasin
mods.integrateddynamics.mechanical_drying_basin
mods.id.MechanicalDryingBasin
mods.id.mechanicaldryingbasin
mods.id.mechanicalDryingBasin
mods.id.mechanical_drying_basin
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Mechanical Drying Basin also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.integrateddynamics.mechanicaldryingbasin.recipeBuilder()"
    - `#!groovy boolean`. Sets if the recipe is added to the basic (Drying Basin) machine. (Default `false`).

        ```groovy
        basic()
        basic(boolean)
        ```

    - `#!groovy int`. Sets the time in ticks the recipe takes to process. (Default `10`).

        ```groovy
        duration(int)
        ```

    - `#!groovy boolean`. Sets if the recipe is added to the mechanical (Mechanical Drying Basin) machine. (Default `true`).

        ```groovy
        mechanical()
        mechanical(boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `org.cyclops.cyclopscore.recipe.custom.api.IRecipe<org.cyclops.cyclopscore.recipe.custom.component.IngredientAndFluidStackRecipeComponent, org.cyclops.cyclopscore.recipe.custom.component.IngredientAndFluidStackRecipeComponent, org.cyclops.cyclopscore.recipe.custom.component.DurationRecipeProperties>`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.integrateddynamics.mechanicaldryingbasin.recipeBuilder()
            .input(item('minecraft:diamond'))
            .fluidInput(fluid('water') * 50)
            .fluidOutput(fluid('lava') * 20000)
            .duration(300)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.integrateddynamics.mechanicaldryingbasin.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.integrateddynamics.mechanicaldryingbasin.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.integrateddynamics.mechanicaldryingbasin.removeAll()
    ```

???+ Example
    ```groovy
    mods.integrateddynamics.mechanicaldryingbasin.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.integrateddynamics.mechanicaldryingbasin.streamRecipes()
    ```
