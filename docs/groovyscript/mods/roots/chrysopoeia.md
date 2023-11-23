---
title: "Chrysopoeia"
description: "Chrysopoeia is a spell that transmutes items held in the main hand."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/Chrysopoeia.java"
---

# Chrysopoeia (Roots 3)

## Description

Chrysopoeia is a spell that transmutes items held in the main hand.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.roots.Chrysopoeia
mods.roots.chrysopoeia/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Chrysopoeia also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.chrysopoeia.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe. (Default `null`).

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

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

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.lang.Object`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.chrysopoeia.recipeBuilder()
            .name('clay_transmute')
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:clay'))
            .register()

        mods.roots.chrysopoeia.recipeBuilder()
            .input(item('minecraft:diamond') * 3)
            .output(item('minecraft:gold_ingot') * 3)
            .register()
        ```



## Removing Recipes

- Removes the Chrysopoeia recipe with the given input itemstack:

    ```groovy
    mods.roots.chrysopoeia.removeByInput(ItemStack)
    ```

- Removes the Chrysopoeia recipe with the given name:

    ```groovy
    mods.roots.chrysopoeia.removeByName(ResourceLocation)
    ```

- Removes the Chrysopoeia recipe with the given output itemstack:

    ```groovy
    mods.roots.chrysopoeia.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.chrysopoeia.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.chrysopoeia.removeByInput(item('minecraft:rotten_flesh'))
    mods.roots.chrysopoeia.removeByName(resource('roots:gold_from_silver'))
    mods.roots.chrysopoeia.removeByOutput(item('minecraft:iron_nugget'))
    mods.roots.chrysopoeia.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.chrysopoeia.streamRecipes()
    ```
