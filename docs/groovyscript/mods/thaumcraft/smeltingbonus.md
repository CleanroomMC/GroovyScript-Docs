---
title: "Smelting Bonus"
description: "Additional item output when smelting a given item in the Infernal Furnace Multiblock."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/thaumcraft/SmeltingBonus.java"
---

# Smelting Bonus (Thaumcraft)

## Description

Additional item output when smelting a given item in the Infernal Furnace Multiblock.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="10"
mods.thaum.SmeltingBonus
mods.thaum.smeltingbonus
mods.thaum.smeltingBonus
mods.thaum.smelting_bonus
mods.tc.SmeltingBonus
mods.tc.smeltingbonus
mods.tc.smeltingBonus
mods.tc.smelting_bonus
mods.thaumcraft.SmeltingBonus
mods.thaumcraft.smeltingbonus/*(1)!*/
mods.thaumcraft.smeltingBonus
mods.thaumcraft.smelting_bonus
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `in`, `out`, with chance having a default value of `0.33F`:

    ```groovy
    mods.thaumcraft.smeltingbonus.add(IIngredient, ItemStack)
    ```

- Adds recipes in the format `in`, `out`, `chance`:

    ```groovy
    mods.thaumcraft.smeltingbonus.add(IIngredient, ItemStack, float)
    ```


### Recipe Builder

Just like other recipe types, the Smelting Bonus also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.thaumcraft.smeltingbonus.recipeBuilder()"
    - `#!groovy IIngredient`. Sets the input of the smelting operation. Requires not null.

        ```groovy
        input(IIngredient)
        ```

    - `#!groovy ItemStack`. Sets the bonus item to be produced from the smelting operation. Requires not null.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy float`. Sets the chance of `out` being produced from the smelting operation per attached Arcane Bellows + 1. (Default `0.33F`).

        ```groovy
        chance(float)
        ```

    - First validates the builder, outputting errors to the log file if the validation failed, then registers the builder.

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.thaumcraft.smeltingbonus.recipeBuilder()
            .input(item('minecraft:cobblestone'))
            .output(item('minecraft:stone_button'))
            .chance(0.2F)
            .register()

        mods.thaumcraft.smeltingbonus.recipeBuilder()
            .input(ore('stone'))
            .output(item('minecraft:obsidian'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.thaumcraft.smeltingbonus.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.thaumcraft.smeltingbonus.removeAll()
    ```

???+ Example
    ```groovy
    mods.thaumcraft.smeltingbonus.removeByOutput(item('minecraft:gold_nugget'))
    mods.thaumcraft.smeltingbonus.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.thaumcraft.smeltingbonus.streamRecipes()
    ```
