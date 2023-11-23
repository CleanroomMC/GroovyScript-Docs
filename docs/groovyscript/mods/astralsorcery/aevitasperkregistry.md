---
title: "Aevitas Perk Registry"
description: "Having the Stone Enrichment perk will convert nearby stone blocks into random ores."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/OreChance.java"
---

# Aevitas Perk Registry (Astral Sorcery)

## Description

Having the Stone Enrichment perk will convert nearby stone blocks into random ores.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="14"
mods.astral.AevitasPerkRegistry
mods.astral.aevitasperkregistry
mods.astral.aevitasPerkRegistry
mods.astral.aevitas_perk_registry
mods.astral_sorcery.AevitasPerkRegistry
mods.astral_sorcery.aevitasperkregistry
mods.astral_sorcery.aevitasPerkRegistry
mods.astral_sorcery.aevitas_perk_registry
mods.as.AevitasPerkRegistry
mods.as.aevitasperkregistry
mods.as.aevitasPerkRegistry
mods.as.aevitas_perk_registry
mods.astralsorcery.AevitasPerkRegistry
mods.astralsorcery.aevitasperkregistry/*(1)!*/
mods.astralsorcery.aevitasPerkRegistry
mods.astralsorcery.aevitas_perk_registry
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds entries in the format `ore`, `weight`:

    ```groovy
    mods.astralsorcery.aevitasperkregistry.add(String, int)
    ```

???+ Example
    ```groovy
    mods.astralsorcery.aevitasperkregistry.add(ore('blockDiamond'), 10000)
    ```

## Removing Entries

- Removes entries of the given ore:

    ```groovy
    mods.astralsorcery.aevitasperkregistry.remove(String)
    ```

- Removes entries of the given ore:

    ```groovy
    mods.astralsorcery.aevitasperkregistry.remove(OreDictIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.aevitasperkregistry.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.aevitasperkregistry.remove(ore('oreDiamond'))
    mods.astralsorcery.aevitasperkregistry.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.aevitasperkregistry.streamRecipes()
    ```
