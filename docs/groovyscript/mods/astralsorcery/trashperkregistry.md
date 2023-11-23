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

```groovy hl_lines="14"
mods.astral.TrashPerkRegistry
mods.astral.trashperkregistry
mods.astral.trashPerkRegistry
mods.astral.trash_perk_registry
mods.astral_sorcery.TrashPerkRegistry
mods.astral_sorcery.trashperkregistry
mods.astral_sorcery.trashPerkRegistry
mods.astral_sorcery.trash_perk_registry
mods.as.TrashPerkRegistry
mods.as.trashperkregistry
mods.as.trashPerkRegistry
mods.as.trash_perk_registry
mods.astralsorcery.TrashPerkRegistry
mods.astralsorcery.trashperkregistry/*(1)!*/
mods.astralsorcery.trashPerkRegistry
mods.astralsorcery.trash_perk_registry
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds entries in the format `ore`, `weight`:

    ```groovy
    mods.astralsorcery.trashperkregistry.add(String, int)
    ```

???+ Example
    ```groovy
    mods.astralsorcery.trashperkregistry.add(ore('blockDiamond'), 10000)
    ```

## Removing Entries

- Removes entries of the given ore:

    ```groovy
    mods.astralsorcery.trashperkregistry.remove(String)
    ```

- Removes entries of the given ore:

    ```groovy
    mods.astralsorcery.trashperkregistry.remove(OreDictIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.trashperkregistry.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.trashperkregistry.remove(ore('oreDiamond'))
    mods.astralsorcery.trashperkregistry.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.trashperkregistry.streamRecipes()
    ```
