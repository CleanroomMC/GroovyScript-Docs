---
title: "Alchemy Array"
description: "Converts two items into an output itemstack by using Arcane Ashes in-world. Has a configurable texture for the animation."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/bloodmagic/AlchemyArray.java"
---

# Alchemy Array (Blood Magic: Alchemical Wizardry)

## Description

Converts two items into an output itemstack by using Arcane Ashes in-world. Has a configurable texture for the animation.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="6"
mods.bm.AlchemyArray
mods.bm.alchemyarray
mods.bm.alchemyArray
mods.bm.alchemy_array
mods.bloodmagic.AlchemyArray
mods.bloodmagic.alchemyarray/*(1)!*/
mods.bloodmagic.alchemyArray
mods.bloodmagic.alchemy_array
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `catalyst`, `output`, `circleTexture`:

    ```groovy
    mods.bloodmagic.alchemyarray.add(Ingredient, Ingredient, ItemStack)
    ```

- Adds recipes in the format `input`, `catalyst`, `output`, optional `circleTexture`:

    ```groovy
    mods.bloodmagic.alchemyarray.add(Ingredient, Ingredient, ItemStack, ResourceLocation)
    ```

- Adds recipes in the format `input`, `catalyst`, `output`, optional `circleTexture`:

    ```groovy
    mods.bloodmagic.alchemyarray.add(Ingredient, Ingredient, ItemStack, String)
    ```


### Recipe Builder

Just like other recipe types, the Alchemy Array also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.bloodmagic.alchemyarray.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

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

    - `#!groovy ResourceLocation`. Sets the animation texture.

        ```groovy
        texture(String)
        texture(ResourceLocation)
        ```

    - `#!groovy IIngredient`. Sets the catalyst.

        ```groovy
        catalyst(IIngredient)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `WayofTime.bloodmagic.api.impl.recipe.RecipeAlchemyArray`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.bloodmagic.alchemyarray.recipeBuilder()
            .input(item('minecraft:diamond'))
            .catalyst(item('bloodmagic:slate:1'))
            .output(item('minecraft:gold_ingot'))
            .texture('bloodmagic:textures/models/AlchemyArrays/LightSigil.png')
            .register()

        mods.bloodmagic.alchemyarray.recipeBuilder()
            .input(item('minecraft:clay'))
            .catalyst(item('minecraft:gold_ingot'))
            .output(item('minecraft:diamond'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given catalyst:

    ```groovy
    mods.bloodmagic.alchemyarray.removeByCatalyst(IIngredient)
    ```

- Removes all recipes that match the given input:

    ```groovy
    mods.bloodmagic.alchemyarray.removeByInput(IIngredient)
    ```

- This removes all recipes that match the given input and Catalyst:

    ```groovy
    mods.bloodmagic.alchemyarray.removeByInputAndCatalyst(IIngredient, IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.bloodmagic.alchemyarray.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.bloodmagic.alchemyarray.removeAll()
    ```

???+ Example
    ```groovy
    mods.bloodmagic.alchemyarray.removeByCatalyst(item('bloodmagic:slate:2'))
    mods.bloodmagic.alchemyarray.removeByInput(item('bloodmagic:component:13'))
    mods.bloodmagic.alchemyarray.removeByInputAndCatalyst(item('bloodmagic:component:7'), item('bloodmagic:slate:1'))
    mods.bloodmagic.alchemyarray.removeByOutput(item('bloodmagic:sigil_void'))
    mods.bloodmagic.alchemyarray.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.bloodmagic.alchemyarray.streamRecipes()
    ```
