# Lootbag

## Rarity

Each lootbag modification is rarity specific. Rarities can be specified using the following methods.

```groovy
mods.thaumcraft.LootBag.getRare()
mods.thaumcraft.LootBag.getUncommon()
mods.thaumcraft.LootBag.getCommon()
```

### Remove All

Removes all items from the specified rarity of lootbag.

```groovy
.removeAll()
```

!!! example

    ```groovy
    mods.thaumcraft.LootBag.getCommon().removeAll()
    ```

!!! Bug
    Armor chances are hard coded into randomized loot function, and are not currently removable.

### Remove

Removes chance for an item from the specified rarity of lootbag.

```groovy
.removeItem(ItemStack)
```

!!! example

    ```groovy
    mods.thaumcraft.LootBag.getRare().removeItem(item('minecraft:ender_pearl'))
    ```

### Add

Adds chance for an item in the given rarity of lootbag.

```groovy
.addItem(ItemStack, int/*(1)!*/)
```

1. a non-negative weight (higher number = more likely)

!!! example

    ```groovy
    mods.thaumcraft.LootBag.getRare().addItem(item('minecraft:diamond_block'), 10)
    ```
