---
title: "Environmental Accumulator"
description: "Consumes an item to give an output, possibly changing the weather. Has a cooldown time or a blood cost."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/evilcraft/EnvironmentalAccumulator.java"
---

# Environmental Accumulator (EvilCraft)

## Description

Consumes an item to give an output, possibly changing the weather. Has a cooldown time or a blood cost.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.evilcraft.EnvironmentalAccumulator
mods.evilcraft.environmentalaccumulator/*(1)!*/
mods.evilcraft.environmentalAccumulator
mods.evilcraft.environmental_accumulator
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Environmental Accumulator also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.evilcraft.environmentalaccumulator.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. Sets the base time in ticks the recipe takes to process. Requires greater than or equal to 0.

        ```groovy
        duration(int)
        ```

    - `#!groovy int`. Sets the time in ticks required before another recipe can be run in this Environmental Accumulator. Also controls the amount of `fluid('evilcraftblood')` consumed by the Sanguinary Environmental Accumulator. Requires greater than or equal to 0.

        ```groovy
        cooldown(int)
        cooldowntime(int)
        ```

    - `#!groovy WeatherType`. Sets the weather type required to start the recipe. Requires not null. (Default `null`).

        ```groovy
        inputWeather(String)
        inputWeather(WeatherType)
        ```

    - `#!groovy WeatherType`. Sets the weather type the world is changed to when the recipe is completed. Requires not null. (Default `null`).

        ```groovy
        outputWeather(String)
        outputWeather(WeatherType)
        ```

    - `#!groovy double`. Sets how fast the item visually rotates while crafting. Requires greater than or equal to 0.

        ```groovy
        speed(double)
        processingspeed(double)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `org.cyclops.cyclopscore.recipe.custom.api.IRecipe<org.cyclops.evilcraft.core.recipe.custom.EnvironmentalAccumulatorRecipeComponent, org.cyclops.evilcraft.core.recipe.custom.EnvironmentalAccumulatorRecipeComponent, org.cyclops.evilcraft.core.recipe.custom.EnvironmentalAccumulatorRecipeProperties>`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.evilcraft.environmentalaccumulator.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:clay') * 2)
            .inputWeather(weather('clear'))
            .outputWeather(weather('rain'))
            .processingspeed(1)
            .cooldowntime(1000)
            .duration(10)
            .register()

        mods.evilcraft.environmentalaccumulator.recipeBuilder()
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:diamond'))
            .inputWeather(weather('rain'))
            .outputWeather(weather('lightning'))
            .speed(10)
            .cooldown(1)
            .register()

        mods.evilcraft.environmentalaccumulator.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay') * 16)
            .inputWeather(weather('lightning'))
            .outputWeather(weather('lightning'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.evilcraft.environmentalaccumulator.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.evilcraft.environmentalaccumulator.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.evilcraft.environmentalaccumulator.removeAll()
    ```

???+ Example
    ```groovy
    mods.evilcraft.environmentalaccumulator.removeByInput(item('evilcraft:exalted_crafter:1'))
    mods.evilcraft.environmentalaccumulator.removeByOutput(item('evilcraft:exalted_crafter:2'))
    mods.evilcraft.environmentalaccumulator.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.evilcraft.environmentalaccumulator.streamRecipes()
    ```
