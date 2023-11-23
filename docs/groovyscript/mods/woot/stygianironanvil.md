---
title: "Stygian Iron Anvil"
description: "Has a catalyst (which may or may not be consumed) placed on the anvil, with the input items thrown atop the base."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/woot/StygianIronAnvil.java"
---

# Stygian Iron Anvil (Woot)

## Description

Has a catalyst (which may or may not be consumed) placed on the anvil, with the input items thrown atop the base.

???+ Note
    The anvil must be above a Magma Block and then right clicked with a Hammer, converting the input items into the output item.

???+ Warning
    While more than 6 items can function as the input of a Stygian Iron Anvil recipe, only the first 6 are shown in JEI.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.woot.StygianIronAnvil
mods.woot.stygianironanvil/*(1)!*/
mods.woot.stygianIronAnvil
mods.woot.stygian_iron_anvil
mods.woot.Anvil
mods.woot.anvil
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Stygian Iron Anvil also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.woot.stygianironanvil.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to Integer.MAX_VALUE. (Default `null`).

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

    - `#!groovy ItemStack`. Sets the itemstack used for the base. Requires not isEmpty.

        ```groovy
        base(ItemStack)
        ```

    - `#!groovy boolean`. Sets if the base is used as a catalyst and not consumed.

        ```groovy
        preserveBase()
        preserveBase(boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `ipsis.woot.crafting.IAnvilRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.woot.stygianironanvil.recipeBuilder()
            .input(item('minecraft:diamond'),item('minecraft:diamond'),item('minecraft:diamond'))
            .base(item('minecraft:gold_ingot'))
            .output(item('minecraft:clay'))
            .preserveBase(true)
            .register()

        mods.woot.stygianironanvil.recipeBuilder()
            .input(item('minecraft:diamond'), item('minecraft:gold_ingot'), item('minecraft:iron_ingot'), item('minecraft:diamond_block'), item('minecraft:gold_block'), item('minecraft:iron_bars'), item('minecraft:magma'))
            .base(item('minecraft:clay'))
            .output(item('minecraft:clay'))
            .preserveBase()
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given base item:

    ```groovy
    mods.woot.stygianironanvil.removeByBase(ItemStack)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.woot.stygianironanvil.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.woot.stygianironanvil.removeAll()
    ```

???+ Example
    ```groovy
    mods.woot.stygianironanvil.removeByBase(item('minecraft:iron_bars'))
    mods.woot.stygianironanvil.removeByOutput(item('woot:stygianironplate'))
    mods.woot.stygianironanvil.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.woot.stygianironanvil.streamRecipes()
    ```
