# LootEntries

## Adding a LootEntry

GroovyScript's Loot module provides a builder that can be used to create and register LootEntry. <br>
Don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out.

```groovy
loot.entryBuilder()
```

Naming the entry: (optional (defaults to Item's resource location))

```groovy
.name(String)
.name(ResourceLocation)
```

Specifying parent loot table: (required (optional if only building))

```groovy
.table(String)
.table(ResourceLocation)
```

Specifying parent loot pool: (required (optional if only building))

```groovy
.pool(String)
.pool(ResourceLocation)
```

Adding a weight: (optional (default is 1))

```groovy
.weight(int) // (1)!
```

1. Weight is this entry's relative likelihood of being selected amongst other entries in the same pool.

Specifying quality: (optional (default is 0))

```groovy
.quality(int) // (1)!
```

1. Quality is a luck multiplier added to the weight of an item. The higher an item's quality, the more likely that player is to roll said entry as their luck value increases.

Specifying random chance: (optional)

```groovy
.randomChance(float) // (1)!
.randomChanceWithLooting(float /* (2)! */, float /* (3)! */)
```

1. The will only be rolled if the specified random chance (as a float [0, 1]) is successful.
2. random chance (as a float [0, 1]).
3. looting multiplier which is multiplied with the looting level and added to the random chance.

Specifying loot conditions: (optional)

```groovy
.killedByPlayer() // (1)!
.killedByNonPlayer() // (2)!
.condition(LootCondition) // (3)!
.condition{ java.util.Random /* (4)! */, net.minecraft.world.storage.loot.LootContext /* (5)! */ -> boolean /* (6)! */ }
```

1. An entity must be killed by a player for this entry to be rolled.
2. An entity must be killed by a non-player for this entry to be rolled.
3. This method exists so you can define and add a custom loot condition which implements net.minecraft.world.storage.loot.conditions.LootCondition.
4. An instance of java.util.Random seeded by minecraft.
5. The current LootContext which contains info about the player, world, etc.
6. LootCondition closures must return a boolean. If true the LootPool will be rolled, if false it will not.

Specifying loot functions: (optional)

```groovy
.enchantWithLevels(boolean /* (1)! */, int /* (2)! */, int /* (3)! */)
.enchantWithLevels(boolean, int, int, LootCondition...) // (4)!
.enchantRandomly() // (5)!
.enchantRandomly(Enchantment...) // (6)!
.enchantRandomly(LootCondition...) // (7)!
.enchantRandomly(Enchantment, LootCondition...)
.enchantRandomly(Enchantment[], LootCondition)
.enchantRandomly(Enchantment[], LootCondition...)
.lootingBonus(float, float) // (8)!
.lootingBonus(float, float, int) // (9)!
.lootingBonus(float, float, LootCondition...)
.lootingBonus(float, float, int, LootCondition...)
.setDamage(int) // (10)!
.setDamage(int, int) // (11)!
.setDamage(int, LootCondition...)
.setDamage(int, int, LootCondition...)
.setCount(int) // (12)!
.setCount(int, int) // (13)!
.setCount(int, LootCondition...)
.setCount(int, int, LootCondition...)
.setMetaData(int) // (14)!
.setMetaData(int, int) // (15)!
.setMetaData(int, LootCondition...)
.setMetaData(int, int, LootCondition...)
.setNBT(String) // (16)!
.setNBT(NBTTagCompount) // (17)!
.setNBT(String, LootCondition...)
.setNBT(NBTTagCompount, LootCondition...)
.smelt() // (18)!
.smelt(LootConditions...)
.function(LootFunction) // (19)!
.function{ ItemStack /* (20)! */, Random /* (21)! */, LootContext /* (22)! */ -> ItemStack /* (23)! */ }
.function({LootFunction}, LootCondition...)
```

1. Whether or not tresure enchantments - mending or frost walker for instance - can be applied to the item.
2. Miniumum player level the enchantments can be rolled with (uniformly distributed).
3. Maximum player level the enchantments can be rolled with (uniformly distributed).
4. Same as the method above but allows for the specification of loot conditions which must be met for the enchantment(s) to be applied.
5. Apply's an random enchantment to the item at a random level.
6. Same as .enchantRandomly() but lets you specify the pool of enchantments selected from.
7. Same as .enchantRandomly() but lets you specify loot conditions which must be met for the enchantment to be met.
8. Minimum and maximum number of bonus items when the player is using looting (uniformly distributed).
9. Same as the above functions but with an integer limit on the max number of the item that the player can get after the bonus is applied.
10. Set durability of the item.
11. Set minimum and maximum durability of the item (uniformly distributed).
12. Set quantity of item recieved.
13. Set minimum and maximum quantity of the item (uniformly distributed).
14. Set metadata of item recieved.
15. Set minimum and maximum metadata of the item (uniformly distributed).
16. Sets NBT data of the item (consumes an nbt json string).
17. You can use the nbt(String) bracket handler to call this method.
18. Smelt's the item using the cooresponding furnace recipe.
19. General function for adding LootFunction to the entry.
20. The item that is going to be given to the player.
21. An instance of java.util.Random seeded by minecraft.
22. The current LootContext which contains info about the player, world, etc.
23. The item that actually gets given to the player (post-modifications).

Build the LootEntry: (returns LootEntry)

```groovy
.build() // (1)!
```

1. Useful for saving an entry so it can be added to many tables/pools manually. Using LootPool.addEntry(LootEntry)

Register LootEntry: (returns nothing)

```groovy
.register() // (1)!
```

1. Builds the loot entry and adds it to the specified pool.

!!! example

    Let's add a new loot entry that makes chickens able to drop a baked potato and a 1/20 chance of dropping 10 baked potatos instead...

    ```groovy
    loot.entryBuilder()
        .table('minecraft:entities/chicken')
        .pool('main')
        .item(item('minecraft:potato'))
        .function({ ItemStack stack, Random random, LootContext context -> // (1)!
                stack.setCount(10)
                return stack
            },
            loot.condition{ Random random, LootContext context -> random.nextFloat() < 0.05f } // (2)!
        )
        .smelt()
        .register()
    ```

    1. Don't forget to import the classes that functions/conditions take as parameters.
    2. When writing a closure condition for any function, you must wrap the closure in a loot.condition() call.

## Removing a LootEntry

```groovy
LootPool.removeEntry(String)
```

!!! example

    ```groovy
    def chickenMainLootPool = loot.getTable('minecraft:entities/chicken').getPool('main')
    chickenMainLootPool.removeEntry('minecraft:feather')
    ```
