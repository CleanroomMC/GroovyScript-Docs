---
title: "Lootbag"
description: "Control what the different rarities of lootbag drop when opened."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/thaumcraft/LootBag.java"
---

# Lootbag (Thaumcraft)

## Description

Control what the different rarities of lootbag drop when opened.

???+ Warning
    This compat is not fully documented. Some or all of its features are not present on the wiki. View the source code to gain an accurate understanding of the compat.

!!! Bug
    Armor chances are hard coded into randomized loot function, and are not currently removable.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.thaumcraft.loot_bag/*(1)!*/
mods.thaumcraft.lootbag
mods.thaumcraft.lootBag
mods.thaumcraft.LootBag
mods.tc.loot_bag
mods.tc.lootbag
mods.tc.lootBag
mods.tc.LootBag
mods.thaum.loot_bag
mods.thaum.lootbag
mods.thaum.lootBag
mods.thaum.LootBag
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds an item with a given weight to the target lootbag in the format `item`, `chance`, `rarity`:

    ```groovy
    mods.thaumcraft.loot_bag.add(ItemStack, int, int)
    ```

???+ Example
    ```groovy
    mods.thaumcraft.loot_bag.add(item('minecraft:diamond_block'), 100, 2)
    mods.thaumcraft.loot_bag.add(item('minecraft:dirt'), 100, 0)
    ```

## Removing Recipes

- Removes an item from the target lootbag in the format `item`, `rarity`:

    ```groovy
    mods.thaumcraft.loot_bag.remove(ItemStack, int)
    ```

- Removes all items from the target lootbag rarity:

    ```groovy
    mods.thaumcraft.loot_bag.removeAll(int)
    ```

???+ Example
    ```groovy
    mods.thaumcraft.loot_bag.remove(item('minecraft:ender_pearl'), 0)
    mods.thaumcraft.loot_bag.removeAll(2)
    ```
