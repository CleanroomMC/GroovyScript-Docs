---
title: "Enchanter"
description: "Enchanting is a mechanic used to create new items, as well as repair tools, armor, and weapons, using the Altar block."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/aether_legacy/Enchanter.java"
---

# Enchanter (GroovyScript - The Aether)

## Description

Enchanting is a mechanic used to create new items, as well as repair tools, armor, and weapons, using the Altar block.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.aether_legacy.enchanter/*(1)!*/
mods.aether_legacy.enchanter
mods.aether.enchanter
mods.aether.enchanter
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds an Enchanting recipe in the format `input`, `output`, `time`.:

    ```groovy
    mods.aether_legacy.enchanter.add(ItemStack, ItemStack, int)
    ```


### Recipe Builder

Just like other recipe types, the Enchanter also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.aether_legacy.enchanter.recipeBuilder()"
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

    - `#!groovy int`. groovyscript.wiki.aether_legacy.enchanter.time.value. Requires greater than or equal to 0. (Default `0`).

        ```groovy
        time(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.gildedgames.the_aether.api.enchantments.AetherEnchantment`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.aether_legacy.enchanter.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:diamond'))
            .time(200)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.aether_legacy.enchanter.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.aether_legacy.enchanter.removeAll()
    ```

???+ Example
    ```groovy
    mods.aether_legacy.enchanter.removeByOutput(item('aether_legacy:enchanted_gravitite'))
    mods.aether_legacy.enchanter.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.aether_legacy.enchanter.streamRecipes()
    ```
