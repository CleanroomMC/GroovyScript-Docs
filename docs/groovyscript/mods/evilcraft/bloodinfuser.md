---
title: "Blood Infuser"
description: "Consumes an item, some fluid, and requires a given tier of Promise of Tenacity to produce the output and some experience after a duration."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/evilcraft/BloodInfuser.java"
---

# Blood Infuser (EvilCraft)

## Description

Consumes an item, some fluid, and requires a given tier of Promise of Tenacity to produce the output and some experience after a duration.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.evilcraft.BloodInfuser
mods.evilcraft.bloodinfuser/*(1)!*/
mods.evilcraft.bloodInfuser
mods.evilcraft.blood_infuser
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Blood Infuser also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.evilcraft.bloodinfuser.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        blood(int)
        fluidInput(int)
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy float`. Sets the experience gained by taking the output item out of the Blood Infuser. Requires greater than or equal to 0.

        ```groovy
        xp(float)
        ```

    - `#!groovy int`. Sets the tier of the recipe, determined by the Promise of Tenacity contained within the upgrade slots of the machine. Requires greater than or equal to 0 and less than or equal to 3.

        ```groovy
        tier(int)
        ```

    - `#!groovy int`. Sets the base time in ticks the recipe takes to process. Requires greater than or equal to 0.

        ```groovy
        duration(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.evilcraft.bloodinfuser.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:clay'))
            .fluidInput(fluid('evilcraftblood') * 1000)
            .tier(3)
            .duration(100)
            .xp(10000)
            .register()

        mods.evilcraft.bloodinfuser.recipeBuilder()
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:clay'))
            .fluidInput(100000)
            .register()

        mods.evilcraft.bloodinfuser.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay') * 4)
            .fluidInput(5000)
            .tier(1)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.evilcraft.bloodinfuser.removeByInput(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.evilcraft.bloodinfuser.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.evilcraft.bloodinfuser.removeAll()
    ```

???+ Example
    ```groovy
    mods.evilcraft.bloodinfuser.removeByInput(item('evilcraft:dark_gem'))
    mods.evilcraft.bloodinfuser.removeByOutput(item('minecraft:leather'))
    mods.evilcraft.bloodinfuser.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.evilcraft.bloodinfuser.streamRecipes()
    ```
