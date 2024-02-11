---
title: "Cannon Ammo"
description: "Item and weight, where weight is a factor in how much damage is dealt."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/appliedenergistics2/CannonAmmo.java"
---

# Cannon Ammo (Applied Energistics 2)

## Description

Item and weight, where weight is a factor in how much damage is dealt.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="7"
mods.ae2.cannon_ammo
mods.ae2.cannonammo
mods.ae2.cannonAmmo
mods.ae2.CannonAmmo
mods.ae2.cannon
mods.ae2.Cannon
mods.appliedenergistics2.cannon_ammo/*(1)!*/
mods.appliedenergistics2.cannonammo
mods.appliedenergistics2.cannonAmmo
mods.appliedenergistics2.CannonAmmo
mods.appliedenergistics2.cannon
mods.appliedenergistics2.Cannon
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds ammo in the format `item`, `value`:

    ```groovy
    mods.appliedenergistics2.cannon_ammo.add(ItemStack, double)
    ```

???+ Example
    ```groovy
    mods.appliedenergistics2.cannon_ammo.add(item('minecraft:clay'), 10000)
    ```

## Removing Entries

- Removes the ammo entry for the given item:

    ```groovy
    mods.appliedenergistics2.cannon_ammo.remove(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.appliedenergistics2.cannon_ammo.removeAll()
    ```

???+ Example
    ```groovy
    mods.appliedenergistics2.cannon_ammo.remove(item('minecraft:gold_nugget'))
    mods.appliedenergistics2.cannon_ammo.removeAll()
    ```
