---
title: "Mineralis Ritual Registry"
description: "Using a mineralis ritual will convert nearby stone blocks into random ores."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/OreChance.java"
---

# Mineralis Ritual Registry (Astral Sorcery)

## Description

Using a mineralis ritual will convert nearby stone blocks into random ores.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.astral_sorcery.mineralis_ritual_registry
mods.astral_sorcery.mineralisritualregistry
mods.astral_sorcery.mineralisRitualRegistry
mods.astral_sorcery.MineralisRitualRegistry
mods.astralsorcery.mineralis_ritual_registry/*(1)!*/
mods.astralsorcery.mineralisritualregistry
mods.astralsorcery.mineralisRitualRegistry
mods.astralsorcery.MineralisRitualRegistry
mods.astral.mineralis_ritual_registry
mods.astral.mineralisritualregistry
mods.astral.mineralisRitualRegistry
mods.astral.MineralisRitualRegistry
mods.as.mineralis_ritual_registry
mods.as.mineralisritualregistry
mods.as.mineralisRitualRegistry
mods.as.MineralisRitualRegistry
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds entries in the format `ore`, `weight`:

    ```groovy
    mods.astralsorcery.mineralis_ritual_registry.add(String, int)
    ```

???+ Example
    ```groovy
    mods.astralsorcery.mineralis_ritual_registry.add(ore('blockDiamond'), 10000)
    ```

## Removing Entries

- Removes entries of the given ore:

    ```groovy
    mods.astralsorcery.mineralis_ritual_registry.remove(OreDictIngredient)
    ```

- Removes entries of the given ore:

    ```groovy
    mods.astralsorcery.mineralis_ritual_registry.remove(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.mineralis_ritual_registry.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.mineralis_ritual_registry.remove(ore('oreDiamond'))
    mods.astralsorcery.mineralis_ritual_registry.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.mineralis_ritual_registry.streamRecipes()
    ```
