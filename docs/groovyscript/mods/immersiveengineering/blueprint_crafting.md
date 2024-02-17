---
title: "Blueprint Crafting"
description: "Converts any number of input itemstacks into an output itemstack, using a blueprint with the category nbt tag as a catalyst."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/BlueprintCrafting.java"
---

# Blueprint Crafting (Immersive Engineering)

## Description

Converts any number of input itemstacks into an output itemstack, using a blueprint with the category nbt tag as a catalyst.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="7"
mods.ie.blueprint_crafting
mods.ie.blueprintcrafting
mods.ie.blueprintCrafting
mods.ie.BlueprintCrafting
mods.ie.blueprint
mods.ie.Blueprint
mods.immersiveengineering.blueprint_crafting/*(1)!*/
mods.immersiveengineering.blueprintcrafting
mods.immersiveengineering.blueprintCrafting
mods.immersiveengineering.BlueprintCrafting
mods.immersiveengineering.blueprint
mods.immersiveengineering.Blueprint
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `fluidInput`:

    ```groovy
    mods.immersiveengineering.blueprint_crafting.add(String, ItemStack, List<IIngredient>)
    ```


### Recipe Builder

Just like other recipe types, the Blueprint Crafting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.blueprint_crafting.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to Integer.MAX_VALUE.

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

    - `#!groovy String`. Sets the required blueprint. Default blueprint options are `components`, `molds`, `bullet`, `specialBullet`, and `electrode`.

        ```groovy
        category(String)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.crafting.BlueprintCraftingRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.blueprint_crafting.recipeBuilder()
            .input(item('minecraft:diamond'), ore('ingotGold'))
            .output(item('minecraft:clay'))
            .category('groovy')
            .register()
        ```



## Removing Recipes

- Default blueprint categories are `components`, `molds`, `bullet`, `specialBullet`, and `electrode`:

    ```groovy
    mods.immersiveengineering.blueprint_crafting.removeByCategory(String)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.blueprint_crafting.removeByInput(String, ItemStack...)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.blueprint_crafting.removeByOutput(String, ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.blueprint_crafting.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.blueprint_crafting.removeByCategory('electrode')
    mods.immersiveengineering.blueprint_crafting.removeByInput('components', item('immersiveengineering:metal:38'), item('immersiveengineering:metal:38'), item('immersiveengineering:metal'))
    mods.immersiveengineering.blueprint_crafting.removeByOutput('components', item('immersiveengineering:material:8'))
    mods.immersiveengineering.blueprint_crafting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.blueprint_crafting.streamRecipes()
    ```

- Default blueprint categories are `components`, `molds`, `bullet`, `specialBullet`, and `electrode`:

    ```groovy
    mods.immersiveengineering.blueprint_crafting.streamRecipesByCategory(String)
    ```
