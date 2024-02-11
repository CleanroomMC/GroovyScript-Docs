---
title: "Tartaric Forge"
description: "Converts up to 4 input items into an output itemstack, requiring a Tartaric gem with a minimum amount of souls, and consuming some."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/bloodmagic/TartaricForge.java"
---

# Tartaric Forge (Blood Magic: Alchemical Wizardry)

## Description

Converts up to 4 input items into an output itemstack, requiring a Tartaric gem with a minimum amount of souls, and consuming some.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.bm.tartaric_forge
mods.bm.tartaricforge
mods.bm.tartaricForge
mods.bm.TartaricForge
mods.bloodmagic.tartaric_forge/*(1)!*/
mods.bloodmagic.tartaricforge
mods.bloodmagic.tartaricForge
mods.bloodmagic.TartaricForge
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `output`, `minimumSouls`, `soulDrain`:

    ```groovy
    mods.bloodmagic.tartaric_forge.add(NonNullList<Ingredient>, ItemStack, double, double)
    ```


### Recipe Builder

Just like other recipe types, the Tartaric Forge also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.bloodmagic.tartaric_forge.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to 4.

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

    - `#!groovy double`. Sets how much Demonic Will is drained from the Tartaric Gem when the craft is completed. Requires greater than or equal to 0. (Default `0.0d`).

        ```groovy
        drain(int)
        soulDrain(double)
        ```

    - `#!groovy double`. Sets how much Demonic Will is required in the Tartaric Gem to start the craft. Requires greater than or equal to 0. (Default `0.0d`).

        ```groovy
        minimumSouls(double)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `WayofTime.bloodmagic.api.impl.recipe.RecipeTartaricForge`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.bloodmagic.tartaric_forge.recipeBuilder()
            .input(item('minecraft:clay'), item('minecraft:clay'), item('minecraft:clay'), item('minecraft:clay'))
            .output(item('minecraft:gold_ingot'))
            .soulDrain(5)
            .minimumSouls(10)
            .register()

        mods.bloodmagic.tartaric_forge.recipeBuilder()
            .input(item('minecraft:gold_ingot'), item('minecraft:clay'))
            .output(item('minecraft:diamond'))
            .drain(200)
            .minimumSouls(500)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.bloodmagic.tartaric_forge.removeByInput(IIngredient...)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.bloodmagic.tartaric_forge.removeByInput(NonNullList<IIngredient>)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.bloodmagic.tartaric_forge.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.bloodmagic.tartaric_forge.removeAll()
    ```

???+ Example
    ```groovy
    mods.bloodmagic.tartaric_forge.removeByInput(item('minecraft:cauldron'), item('minecraft:stone'), item('minecraft:dye:4'), item('minecraft:diamond'))
    mods.bloodmagic.tartaric_forge.removeByInput(item('minecraft:gunpowder'), item('minecraft:redstone'))
    mods.bloodmagic.tartaric_forge.removeByOutput(item('bloodmagic:demon_crystal'))
    mods.bloodmagic.tartaric_forge.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.bloodmagic.tartaric_forge.streamRecipes()
    ```
