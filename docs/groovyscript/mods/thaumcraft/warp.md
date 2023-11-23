---
title: "Warp"
description: "Determines if holding an item or equipping a piece of armor or a bauble gives warp, and how much warp it gives"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/thaumcraft/warp/Warp.java"
---

# Warp (Thaumcraft)

## Description

Determines if holding an item or equipping a piece of armor or a bauble gives warp, and how much warp it gives

## Identifier

Refer to this via any of the following:

```groovy hl_lines="6"
mods.thaum.Warp
mods.thaum.warp
mods.tc.Warp
mods.tc.warp
mods.thaumcraft.Warp
mods.thaumcraft.warp/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds Warp to the given item in the format `item`, `amount`:

    ```groovy
    mods.thaumcraft.warp.addWarp(ItemStack, int)
    ```

???+ Example
    ```groovy
    mods.thaumcraft.warp.addWarp(item('minecraft:pumpkin'), 3)
    ```

## Removing Recipes

- Removes Warp from the given item:

    ```groovy
    mods.thaumcraft.warp.removeWarp(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.thaumcraft.warp.removeAll()
    ```

???+ Example
    ```groovy
    mods.thaumcraft.warp.removeWarp(item('thaumcraft:void_hoe'))
    mods.thaumcraft.warp.removeAll()
    ```
