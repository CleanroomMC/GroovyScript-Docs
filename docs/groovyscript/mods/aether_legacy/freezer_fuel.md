---
title: "Freezer"
description: " By default, the Freezer takes Icestone as fuel. Using GroovyScript, custom fuels can be added."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/aether_legacy/FreezerFuel.java"
---

# Freezer (GroovyScript - The Aether)

## Description

 By default, the Freezer takes Icestone as fuel. Using GroovyScript, custom fuels can be added.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.aether_legacy.freezer_fuel/*(1)!*/
mods.aether_legacy.freezerfuel
mods.aether_legacy.freezerFuel
mods.aether_legacy.FreezerFuel
mods.aether.freezer_fuel
mods.aether.freezerfuel
mods.aether.freezerFuel
mods.aether.FreezerFuel
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds a Freezer fuel in the format `item`, `timeGiven`.:

    ```groovy
    mods.aether_legacy.freezer_fuel.add(ItemStack, int)
    ```

???+ Example
    ```groovy
    mods.aether_legacy.freezer_fuel.add(item('minecraft:packed_ice'), 1000)
    ```

## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.aether_legacy.freezer_fuel.removeByItem(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.aether_legacy.freezer_fuel.removeAll()
    ```

???+ Example
    ```groovy
    mods.aether_legacy.freezer_fuel.removeByItem(item('aether_legacy:icestone'))
    mods.aether_legacy.freezer_fuel.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.aether_legacy.freezer_fuel.streamEntries()
    ```
