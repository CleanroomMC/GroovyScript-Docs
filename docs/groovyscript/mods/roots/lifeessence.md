---
title: "Life Essence"
description: "When shift right clicking a mob in the Life Essence Pool with Runic Shears, it will drop a Life-Essence, which allows that mob to be spawned via the Creature Summoning ritual."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/LifeEssence.java"
---

# Life Essence (Roots 3)

## Description

When shift right clicking a mob in the Life Essence Pool with Runic Shears, it will drop a Life-Essence, which allows that mob to be spawned via the Creature Summoning ritual.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.roots.LifeEssence
mods.roots.lifeessence/*(1)!*/
mods.roots.lifeEssence
mods.roots.life_essence
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds entries in the format `entity`:

    ```groovy
    mods.roots.lifeessence.add(EntityEntry)
    ```

- Adds entries in the format `entity`:

    ```groovy
    mods.roots.lifeessence.add(EntityLivingBase)
    ```

- Adds entries in the format `entity`:

    ```groovy
    mods.roots.lifeessence.add(Class<? extends EntityLivingBase>)
    ```

???+ Example
    ```groovy
    mods.roots.lifeessence.add(entity('minecraft:wither_skeleton'))
    ```

## Removing Entries

- Removes the Life Essence entry for the given Entity:

    ```groovy
    mods.roots.lifeessence.remove(EntityEntry)
    ```

- Removes the Life Essence entry for the given Entity:

    ```groovy
    mods.roots.lifeessence.remove(EntityLivingBase)
    ```

- Removes the Life Essence entry for the given Entity:

    ```groovy
    mods.roots.lifeessence.remove(Class<? extends EntityLivingBase>)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.lifeessence.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.lifeessence.remove(entity('minecraft:sheep'))
    mods.roots.lifeessence.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.lifeessence.streamRecipes()
    ```
