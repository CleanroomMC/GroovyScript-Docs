---
title: "Enchanter Fuel"
description: "By default, the Enchantar (Altar) takes Ambrosium Shards as fuel. Using GroovyScript, custom fuels can be added."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/aether_legacy/EnchanterFuel.java"
---

# Enchanter Fuel (GroovyScript - The Aether)

## Description

By default, the Enchantar (Altar) takes Ambrosium Shards as fuel. Using GroovyScript, custom fuels can be added.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.aether_legacy.enchanter_fuel/*(1)!*/
mods.aether_legacy.enchanterfuel
mods.aether_legacy.enchanterFuel
mods.aether_legacy.EnchanterFuel
mods.aether.enchanter_fuel
mods.aether.enchanterfuel
mods.aether.enchanterFuel
mods.aether.EnchanterFuel
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds an Enchanting fuel in the format `item`, `timeGiven`.:

    ```groovy
    mods.aether_legacy.enchanter_fuel.add(ItemStack, int)
    ```

???+ Example
    ```groovy
    mods.aether_legacy.enchanter_fuel.add(item('minecraft:blaze_rod'), 1000)
    ```

## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.aether_legacy.enchanter_fuel.removeByItem(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.aether_legacy.enchanter_fuel.removeAll()
    ```

???+ Example
    ```groovy
    mods.aether_legacy.enchanter_fuel.removeByItem(item('aether_legacy:ambrosium_shard'))
    mods.aether_legacy.enchanter_fuel.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.aether_legacy.enchanter_fuel.streamEntries()
    ```
