---
title: "Accessory"
description: "The Aether Accessory system."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/aether_legacy/Accessory.java"
---

# Accessory (GroovyScript - The Aether)

## Description

The Aether Accessory system.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.aether_legacy.accessory/*(1)!*/
mods.aether_legacy.accessory
mods.aether.accessory
mods.aether.accessory
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds an Accessory in the format `item`, `type`, where type is one of the following: "Ring", "Pendant", "Cape", "Shield", "Glove", or "Misc".:

    ```groovy
    mods.aether_legacy.accessory.add(ItemStack, String)
    ```


### Recipe Builder

Just like other recipe types, the Accessory also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.aether_legacy.accessory.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy the_aether.AccessoryType`. groovyscript.wiki.aether_legacy.accessory.accessoryType.value.

        ```groovy
        accessoryType(String)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.gildedgames.the_aether.api.accessories.AetherAccessory`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.aether_legacy.accessory.recipeBuilder()
            .input(item('minecraft:shield'))
            .accessoryType('shield')
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.aether_legacy.accessory.removeByInput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.aether_legacy.accessory.removeAll()
    ```

???+ Example
    ```groovy
    mods.aether_legacy.accessory.removeByInput(item('aether_legacy:iron_pendant'))
    mods.aether_legacy.accessory.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.aether_legacy.accessory.streamEntries()
    ```
