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

```groovy hl_lines="8"
mods.ie.BlueprintCrafting
mods.ie.blueprintcrafting
mods.ie.blueprintCrafting
mods.ie.blueprint_crafting
mods.ie.Blueprint
mods.ie.blueprint
mods.immersiveengineering.BlueprintCrafting
mods.immersiveengineering.blueprintcrafting/*(1)!*/
mods.immersiveengineering.blueprintCrafting
mods.immersiveengineering.blueprint_crafting
mods.immersiveengineering.Blueprint
mods.immersiveengineering.blueprint
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `input`, `fluidInput`:

    ```groovy
    mods.immersiveengineering.blueprintcrafting.add(String, ItemStack, List<IIngredient>)
    ```


### Recipe Builder

Just like other recipe types, the Blueprint Crafting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.blueprintcrafting.recipeBuilder()"
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
        mods.immersiveengineering.blueprintcrafting.recipeBuilder()
            .input(item('minecraft:diamond'), ore('ingotGold'))
            .output(item('minecraft:clay'))
            .category('groovy')
            .register()
        ```



## Removing Recipes

- Default blueprint categories are `components`, `molds`, `bullet`, `specialBullet`, and `electrode`:

    ```groovy
    mods.immersiveengineering.blueprintcrafting.removeByCategory(String)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.immersiveengineering.blueprintcrafting.removeByInput(String, ItemStack...)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.immersiveengineering.blueprintcrafting.removeByOutput(String, ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.blueprintcrafting.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.blueprintcrafting.removeByCategory('electrode')
    mods.immersiveengineering.blueprintcrafting.removeByInput('components', item('immersiveengineering:metal:38'), item('immersiveengineering:metal:38'), item('immersiveengineering:metal'))
    mods.immersiveengineering.blueprintcrafting.removeByOutput('components', item('immersiveengineering:material:8'))
    mods.immersiveengineering.blueprintcrafting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.blueprintcrafting.streamRecipes()
    ```

- Default blueprint categories are `components`, `molds`, `bullet`, `specialBullet`, and `electrode`:

    ```groovy
    mods.immersiveengineering.blueprintcrafting.streamRecipesByCategory(String)
    ```
