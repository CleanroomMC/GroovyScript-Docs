---
title: "Perk Tree"
description: "Create a custom perk with a custom effect, at a given location."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/perktree/GroovyPerkTree.java"
---

# Perk Tree (Astral Sorcery)

## Description

Create a custom perk with a custom effect, at a given location.

???+ Warning
    This compat is not fully documented. Some or all of its features are not present on the wiki. View the source code to gain an accurate understanding of the compat.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="14"
mods.astral.PerkTree
mods.astral.perktree
mods.astral.perkTree
mods.astral.perk_tree
mods.astral_sorcery.PerkTree
mods.astral_sorcery.perktree
mods.astral_sorcery.perkTree
mods.astral_sorcery.perk_tree
mods.as.PerkTree
mods.as.perktree
mods.as.perkTree
mods.as.perk_tree
mods.astralsorcery.PerkTree
mods.astralsorcery.perktree/*(1)!*/
mods.astralsorcery.perkTree
mods.astralsorcery.perk_tree
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds the given perk to the perk map:

    ```groovy
    mods.astralsorcery.perktree.add(AbstractPerk)
    ```

- Adds a connection between two perks:

    ```groovy
    mods.astralsorcery.perktree.addConnection(String, String)
    ```

- Moves the given perk to the x and y co-ords specified in the format `perk`, `x`, `z`:

    ```groovy
    mods.astralsorcery.perktree.movePerk(AbstractPerk, int, int)
    ```

???+ Example
    ```groovy
    mods.astralsorcery.perktree.movePerk(mods.astralsorcery.perktree.getPerk('astralsorcery:magnet_ats_reach'), 30, 30)
    ```

## Removing Entries

- Removes the perk with the given name:

    ```groovy
    mods.astralsorcery.perktree.remove(String)
    ```

- Removes a connection between two perks:

    ```groovy
    mods.astralsorcery.perktree.removeConnection(String, String)
    ```

???+ Example
    ```groovy
    mods.astralsorcery.perktree.remove('astralsorcery:mec_inc_ms_2')
    ```

## Getting the value of entries

- Returns the perk with the given name:

    ```groovy
    mods.astralsorcery.perktree.getPerk(ResourceLocation)
    ```

- Returns the perk with the given name:

    ```groovy
    mods.astralsorcery.perktree.getPerk(String)
    ```
