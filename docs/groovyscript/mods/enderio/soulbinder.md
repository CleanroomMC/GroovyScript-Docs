---
title: "Soulbinder"
description: "Converts an input itemstack into an output itemstack, requiring one of several entities in soul vials, using energy and giving XP. Must have a unique name. To function properly, the input entities must be allowed in Soul Vials."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/enderio/SoulBinder.java"
---

# Soulbinder (Ender IO)

## Description

Converts an input itemstack into an output itemstack, requiring one of several entities in soul vials, using energy and giving XP. Must have a unique name. To function properly, the input entities must be allowed in Soul Vials.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.enderio.SoulBinder
mods.enderio.soulbinder/*(1)!*/
mods.enderio.soulBinder
mods.enderio.soul_binder
mods.eio.SoulBinder
mods.eio.soulbinder
mods.eio.soulBinder
mods.eio.soul_binder
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Soulbinder also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.enderio.soulbinder.recipeBuilder()"
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

    - `#!groovy int`. Sets the experience levels required to start the recipe. Requires greater than 0.

        ```groovy
        xp(int)
        ```

    - `#!groovy String`. Sets the unique identifier of the recipe.

        ```groovy
        name(String)
        ```

    - `#!groovy int`. Sets the energy cost of the recipe. Requires greater than 0.

        ```groovy
        energy(int)
        ```

    - `#!groovy NNList<ResourceLocation>`. Sets the valid entities. Entities must be allowed in Soul Vials. Requires greater than or equal to 1. (Default `null`).

        ```groovy
        entity(EntityEntry)
        entity(EntityEntry...)
        entity(Collection<EntityEntry>)
        entitySoul(String)
        entitySoul(String...)
        entitySoul(Collection<String>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `crazypants.enderio.base.recipe.soul.BasicSoulBinderRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.enderio.soulbinder.recipeBuilder()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay'))
            .entity(entity('minecraft:zombie'), entity('minecraft:enderman'))
            .name('groovy_example')
            .energy(1000)
            .xp(5)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.enderio.soulbinder.remove(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.enderio.soulbinder.removeAll()
    ```

???+ Example
    ```groovy
    mods.enderio.soulbinder.remove(item('enderio:item_material:17'))
    mods.enderio.soulbinder.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.enderio.soulbinder.streamRecipes()
    ```
