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

```groovy hl_lines="1"
mods.roots.life_essence/*(1)!*/
mods.roots.lifeessence
mods.roots.lifeEssence
mods.roots.LifeEssence
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds entries in the format `entity`:

    ```groovy
    mods.roots.life_essence.add(Class<? extends EntityLivingBase>)
    ```

- Adds entries in the format `entity`:

    ```groovy
    mods.roots.life_essence.add(EntityEntry)
    ```

- Adds entries in the format `entity`:

    ```groovy
    mods.roots.life_essence.add(EntityLivingBase)
    ```

???+ Example
    ```groovy
    mods.roots.life_essence.add(entity('minecraft:wither_skeleton'))
    ```

## Removing Entries

- Removes the Life Essence entry for the given Entity:

    ```groovy
    mods.roots.life_essence.remove(Class<? extends EntityLivingBase>)
    ```

- Removes the Life Essence entry for the given Entity:

    ```groovy
    mods.roots.life_essence.remove(EntityEntry)
    ```

- Removes the Life Essence entry for the given Entity:

    ```groovy
    mods.roots.life_essence.remove(EntityLivingBase)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.life_essence.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.life_essence.remove(entity('minecraft:sheep'))
    mods.roots.life_essence.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.life_essence.streamRecipes()
    ```
