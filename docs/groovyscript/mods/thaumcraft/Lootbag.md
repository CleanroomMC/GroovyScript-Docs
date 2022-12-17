# Lootbag

## Rarity

Each lootbag modification is rarity specific. Rarities can be specified using the following methods

```groovy
mods.thaumcraft.LootBag.getRare()
mods.thaumcraft.LootBag.getUncommon()
mods.thaumcraft.LootBag.getCommon()
```

### Remove All

Removes all items from the specified rarity of lootbag (except broken armor which is hard coded into randomized loot function).

```groovy
.removeAll()
```

!!! example
    ```groovy
    mods.thaumcraft.LootBag.getCommon().removeAll()
    ```

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
.addItem(ItemStack, int) // int as a non-negative weight (higher number = more likely)
```

!!! example
    ```groovy
    mods.thaumcraft.LootBag.getRare().addItem(item('minecraft:diamond_block'), 10)
    ```
