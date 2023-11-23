---
title: "Drying Basin"
description: "Takes either an item or fluid input and gives either an item or fluid output after a duration."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/integrateddynamics/DryingBasin.java"
---

# Drying Basin (Integrated Dynamics)

## Description

Takes either an item or fluid input and gives either an item or fluid output after a duration.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.integrateddynamics.DryingBasin
mods.integrateddynamics.dryingbasin/*(1)!*/
mods.integrateddynamics.dryingBasin
mods.integrateddynamics.drying_basin
mods.id.DryingBasin
mods.id.dryingbasin
mods.id.dryingBasin
mods.id.drying_basin
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Drying Basin also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.integrateddynamics.dryingbasin.recipeBuilder()"
    - `#!groovy boolean`. Sets if the recipe is added to the basic (Drying Basin) machine.

        ```groovy
        basic()
        basic(boolean)
        ```

    - `#!groovy int`. Sets the time in ticks the recipe takes to process.

        ```groovy
        duration(int)
        ```

    - `#!groovy boolean`. Sets if the recipe is added to the mechanical (Mechanical Drying Basin) machine.

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
        mods.integrateddynamics.dryingbasin.recipeBuilder()
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:clay'))
            .fluidInput(fluid('water') * 500)
            .fluidOutput(fluid('lava') * 2000)
            .mechanical()
            .duration(5)
            .register()

        mods.integrateddynamics.dryingbasin.recipeBuilder()
            .output(item('minecraft:clay'))
            .fluidInput(fluid('water') * 2000)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.integrateddynamics.dryingbasin.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.integrateddynamics.dryingbasin.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.integrateddynamics.dryingbasin.removeAll()
    ```

???+ Example
    ```groovy
    mods.integrateddynamics.dryingbasin.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.integrateddynamics.dryingbasin.streamRecipes()
    ```
