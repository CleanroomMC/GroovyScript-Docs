---
title: "Bark Carving"
description: "Bark Carving is a special set of alternate drops for blocks when broken with an item containing the tool type 'knife'. Amount dropped is up to 2 + fortune/looting level higher than the set amount."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/BarkCarving.java"
---

# Bark Carving (Roots 3)

## Description

Bark Carving is a special set of alternate drops for blocks when broken with an item containing the tool type 'knife'. Amount dropped is up to 2 + fortune/looting level higher than the set amount.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.roots.BarkCarving
mods.roots.barkcarving/*(1)!*/
mods.roots.barkCarving
mods.roots.bark_carving
mods.roots.Bark
mods.roots.bark
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Bark Carving also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.barkcarving.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IBlockState)
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        blockstate(IBlockState)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.recipe.BarkRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.barkcarving.recipeBuilder()
            .name('gold_bark')
            .input(item('minecraft:clay'))
            .output(item('minecraft:gold_ingot'))
            .register()

        mods.roots.barkcarving.recipeBuilder()
            .blockstate(blockstate('minecraft:gold_block'))
            .output(item('minecraft:diamond'))
            .register()

        mods.roots.barkcarving.recipeBuilder()
            .input(blockstate('minecraft:diamond_block'))
            .output(item('minecraft:clay') * 10)
            .register()
        ```



## Removing Recipes

- Removes the Bark Carving recipe with the given input itemstack:

    ```groovy
    mods.roots.barkcarving.removeByBlock(ItemStack)
    ```

- Removes the Bark Carving recipe with the given input itemstack:

    ```groovy
    mods.roots.barkcarving.removeByInput(ItemStack)
    ```

- Removes the Bark Carving recipe with the given name:

    ```groovy
    mods.roots.barkcarving.removeByName(ResourceLocation)
    ```

- Removes the Bark Carving recipe with the given output itemstack:

    ```groovy
    mods.roots.barkcarving.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.barkcarving.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.barkcarving.removeByBlock(item('minecraft:log:1'))
    mods.roots.barkcarving.removeByInput(item('minecraft:log'))
    mods.roots.barkcarving.removeByName(resource('roots:wildwood'))
    mods.roots.barkcarving.removeByOutput(item('roots:bark_dark_oak'))
    mods.roots.barkcarving.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.barkcarving.streamRecipes()
    ```
