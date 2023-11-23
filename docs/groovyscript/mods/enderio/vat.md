---
title: "Vat"
description: "Converts an input fluidstack into an output itemstack at a rate based on up 2 itemstack inputs, and using power. Can be set to require at least NORMAL or ENHANCED tiers, or to IGNORE the tier. NORMAL and IGNORE are effectively the same."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/enderio/Vat.java"
---

# Vat (Ender IO)

## Description

Converts an input fluidstack into an output itemstack at a rate based on up 2 itemstack inputs, and using power. Can be set to require at least NORMAL or ENHANCED tiers, or to IGNORE the tier. NORMAL and IGNORE are effectively the same.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.enderio.Vat
mods.enderio.vat/*(1)!*/
mods.eio.Vat
mods.eio.vat
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Vat also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.enderio.vat.recipeBuilder()"
    - `#!groovy FluidStack`. Sets the input fluid. Requires not null. (Default `null`).

        ```groovy
        input(FluidStack)
        ```

    - `#!groovy RecipeLevel`. Sets the minimum required machine tier of the recipe.

        ```groovy
        tierAny()
        tierNormal()
        tierEnhanced()
        ```

    - `#!groovy int`. Sets the energy cost of the recipe. Requires greater than 0.

        ```groovy
        energy(int)
        ```

    - `#!groovy FluidStack`. Sets the output fluid. Requires not null. (Default `null`).

        ```groovy
        output(FluidStack)
        ```

    - `#!groovy IngredientList<IIngredient>`. Sets the valid input items for the left side. (Default `null`).

        ```groovy
        itemInputLeft(IIngredient, float)
        ```

    - `#!groovy IngredientList<IIngredient>`. Sets the valid input items for the right side. (Default `null`).

        ```groovy
        itemInputRight(IIngredient, float)
        ```

    - `#!groovy FloatList`. Sets the multiplier applied to the respective input item on the left side. (Default `null`).

        ```groovy
        itemInputLeft(IIngredient, float)
        ```

    - `#!groovy FloatList`. Sets the multiplier applied to the respective input item on the right side. (Default `null`).

        ```groovy
        itemInputRight(IIngredient, float)
        ```

    - `#!groovy float`. Sets the base amount of fluid output. Requires greater than 0.

        ```groovy
        baseMultiplier(float)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.enderio.vat.recipeBuilder()
            .input(fluid('lava'))
            .output(fluid('hootch'))
            .baseMultiplier(2)
            .itemInputLeft(item('minecraft:clay'), 2)
            .itemInputLeft(item('minecraft:clay_ball'), 0.5)
            .itemInputRight(item('minecraft:diamond'), 5)
            .itemInputRight(item('minecraft:diamond_block'), 50)
            .itemInputRight(item('minecraft:gold_block'), 10)
            .itemInputRight(item('minecraft:gold_ingot'), 1)
            .itemInputRight(item('minecraft:gold_nugget'), 0.1)
            .energy(1000)
            .tierEnhanced()
            .register()

        mods.enderio.vat.recipeBuilder()
            .input(fluid('hootch') * 100)
            .output(fluid('water') * 50)
            .itemInputLeft(item('minecraft:clay_ball'), 1)
            .itemInputRight(item('minecraft:diamond'), 1)
            .energy(1000)
            .tierNormal()
            .register()

        mods.enderio.vat.recipeBuilder()
            .input(fluid('water'))
            .output(fluid('hootch'))
            .itemInputLeft(item('minecraft:clay'), 2)
            .itemInputLeft(item('minecraft:clay_ball'), 0.5)
            .itemInputRight(item('minecraft:diamond'), 5)
            .itemInputRight(item('minecraft:gold_ingot'), 1)
            .energy(1000)
            .tierAny()
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.enderio.vat.remove(FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.enderio.vat.removeAll()
    ```

???+ Example
    ```groovy
    mods.enderio.vat.remove(fluid('nutrient_distillation'))
    mods.enderio.vat.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.enderio.vat.streamRecipes()
    ```
