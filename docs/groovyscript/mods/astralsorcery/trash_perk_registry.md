---
title: "Trash Perk Registry"
description: "Having the Trash to Treasure perk turns items the player drops in the list defined in the config at 'perks/key_void_trash/DropList' into a chance at random ores."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/OreChance.java"
---

# Trash Perk Registry (Astral Sorcery)

## Description

Having the Trash to Treasure perk turns items the player drops in the list defined in the config at 'perks/key_void_trash/DropList' into a chance at random ores.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="5"
mods.astral_sorcery.trash_perk_registry
mods.astral_sorcery.trashperkregistry
mods.astral_sorcery.trashPerkRegistry
mods.astral_sorcery.TrashPerkRegistry
mods.astralsorcery.trash_perk_registry/*(1)!*/
mods.astralsorcery.trashperkregistry
mods.astralsorcery.trashPerkRegistry
mods.astralsorcery.TrashPerkRegistry
mods.astral.trash_perk_registry
mods.astral.trashperkregistry
mods.astral.trashPerkRegistry
mods.astral.TrashPerkRegistry
mods.as.trash_perk_registry
mods.as.trashperkregistry
mods.as.trashPerkRegistry
mods.as.TrashPerkRegistry
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds entries in the format `ore`, `weight`:

    ```groovy
    mods.astralsorcery.trash_perk_registry.add(String, int)
    ```

???+ Example
    ```groovy
    mods.astralsorcery.trash_perk_registry.add(ore('blockDiamond'), 10000)
    ```

## Removing Entries

- Removes entries of the given ore:

    ```groovy
    mods.astralsorcery.trash_perk_registry.remove(OreDictIngredient)
    ```

- Removes entries of the given ore:

    ```groovy
    mods.astralsorcery.trash_perk_registry.remove(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.trash_perk_registry.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.trash_perk_registry.remove(ore('oreDiamond'))
    mods.astralsorcery.trash_perk_registry.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.trash_perk_registry.streamRecipes()
    ```
