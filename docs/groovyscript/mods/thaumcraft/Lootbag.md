# Lootbag

### Remove All

Removes all items from the given rarity of lootbag (except broken armor which is hard coded into randomized loot function).

```groovy
mods.thaumcraft.LootBag.getRare().removeAll()
mods.thaumcraft.LootBag.getUncommon().removeAll()
mods.thaumcraft.LootBag.getCommon().removeAll()
```


### Remove

Removes chance for an item from the given rarity of lootbag.

```groovy
mods.thaumcraft.LootBag.getRare().removeItem(item('minecraft:ender_pearl'))
mods.thaumcraft.LootBag.getUncommon().removeItem(item('minecraft:gold_ingot'))
mods.thaumcraft.LootBag.getCommon().removeItem(item('minecraft:gold_ingot'))
```


### Add

Adds chance for an item in the given rarity of lootbag.

```groovy
mods.thaumcraft.LootBag.getRare().addItem(item('minecraft:diamond_block'), 10)
mods.thaumcraft.LootBag.getUncommon().addItem(item('minecraft:diamond_block'), 5)
mods.thaumcraft.LootBag.getCommon().addItem(item('minecraft:diamond_block'), 1)
```
