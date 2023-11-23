---
title: "Metallurgic Infuser"
description: "Converts and input itemstack and a varible amount of an infusion type into an output itemstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/MetallurgicInfuser.java"
---

# Metallurgic Infuser (Mekanism)

## Description

Converts and input itemstack and a varible amount of an infusion type into an output itemstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.MetallurgicInfuser
mods.mekanism.metallurgicinfuser/*(1)!*/
mods.mekanism.metallurgicInfuser
mods.mekanism.metallurgic_infuser
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `ingredient`, `infuseType`, `infuseAmount`, `output`:

    ```groovy
    mods.mekanism.metallurgicinfuser.add(IIngredient, InfuseType, int, ItemStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.metallurgicinfuser.add(item('minecraft:nether_star'), infusion('groovy_example'), 50, item('minecraft:clay'))
    ```

### Recipe Builder

Just like other recipe types, the Metallurgic Infuser also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.metallurgicinfuser.recipeBuilder()"
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

    - `#!groovy int`. Sets the amount of the provided Infusion type consumed. Requires greater than 0.

        ```groovy
        ```

    - `#!groovy InfuseType`. Sets the Infusion type the recipe uses. Requires not null. (Default `null`).

        ```groovy
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.MetallurgicInfuserRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.metallurgicinfuser.recipeBuilder()
            .input(item('minecraft:nether_star'))
            .infuse(infusion('groovy_example'))
            .amount(50)
            .output(item('minecraft:clay'))
            .register()
        ```



## Removing Recipes

- Adds recipes in the format `ingredient`, `infuseType`, `infuseAmount`, `output`:

    ```groovy
    mods.mekanism.metallurgicinfuser.add(IIngredient, String, int, ItemStack)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.metallurgicinfuser.removeByInput(IIngredient, InfuseType)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.metallurgicinfuser.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.metallurgicinfuser.removeByInput(ore('dustObsidian'), 'DIAMOND')
    mods.mekanism.metallurgicinfuser.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.metallurgicinfuser.streamRecipes()
    ```
