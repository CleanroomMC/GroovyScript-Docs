---
title: "Arc Furnace"
description: "Converts 1 input itemstack with up to 4 additional inputs into an output itemstack and an optional 'slag' itemstack, taking time and using rf power."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/ArcFurnace.java"
---

# Arc Furnace (Immersive Engineering)

## Description

Converts 1 input itemstack with up to 4 additional inputs into an output itemstack and an optional 'slag' itemstack, taking time and using rf power.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.ie.arc_furnace
mods.ie.arcfurnace
mods.ie.arcFurnace
mods.ie.ArcFurnace
mods.immersiveengineering.arc_furnace/*(1)!*/
mods.immersiveengineering.arcfurnace
mods.immersiveengineering.arcFurnace
mods.immersiveengineering.ArcFurnace
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `additives`, `slag`, `time`, `energyPerTick`:

    ```groovy
    mods.immersiveengineering.arc_furnace.add(ItemStack, IIngredient, List<IIngredient>, ItemStack, int, int)
    ```


### Recipe Builder

Just like other recipe types, the Arc Furnace also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.arc_furnace.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 0 and less than or equal to 5.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy ItemStack`. Sets the item output as slag. Requires not null.

        ```groovy
        slag(ItemStack)
        ```

    - `#!groovy int`. Sets the time in ticks the recipe takes to process. Requires greater than 0. (Default `0`).

        ```groovy
        time(int)
        ```

    - `#!groovy IIngredient`. Sets the item input. Requires not null.

        ```groovy
        mainInput(IIngredient)
        ```

    - `#!groovy int`. Sets the amount of power consumed per tick. Requires greater than 0. (Default `0`).

        ```groovy
        energyPerTick(int)
        ```

    - `#!groovy String`. Sets the special recipe type. Default options are `Alloying`, `Ores`, and `Recycling`.

        ```groovy
        ores()
        alloying()
        recycling()
        specialRecipeType(String)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.ArcFurnaceRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.arc_furnace.recipeBuilder()
            .mainInput(item('minecraft:diamond'))
            .input(item('minecraft:diamond'), ore('ingotGold'))
            .output(item('minecraft:clay'))
            .time(100)
            .energyPerTick(100)
            .slag(item('minecraft:gold_nugget'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.arc_furnace.removeByInput(IIngredient, List<IIngredient>)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.arc_furnace.removeByInput(IIngredient...)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.arc_furnace.removeByInput(List<IIngredient>)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.arc_furnace.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.arc_furnace.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.arc_furnace.removeByInput(item('immersiveengineering:metal:18'), item('immersiveengineering:material:17'))
    mods.immersiveengineering.arc_furnace.removeByOutput(item('immersiveengineering:metal:7'))
    mods.immersiveengineering.arc_furnace.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.arc_furnace.streamRecipes()
    ```
