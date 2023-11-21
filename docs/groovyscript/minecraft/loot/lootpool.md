# LootPools

## Adding a LootPool

GroovyScript's Loot module provides a builder that can be used to create and register LootPools. <br>
Don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out.

```groovy
loot.poolBuilder()
```

Naming the pool: (required)

```groovy
.name(String)
.name(ResourceLocation)
```

Specifying parent loot table: (required (optional if only building))

```groovy
.table(String)
.table(ResourceLocation)
```

Adding [LootEntries](./lootentry.md): (optional)

```groovy
.entry(LootEntry) // (1)!
.entry(ItemStack, int) // (2)!
```

1. See LootEntries
2. A quick method for adding an entry with the specified ItemStack with a cooresponding weight.

Specifying roll chance: (optional (default is 1 roll))

```groovy
.rollsRange(float) // (1)!
.rollsRange(float, float) // (2)!
```

1. The loot pool will always generate the specified number of rolls.
2. Specifies a minimum number of rolls and a maximum number of rolls respectivly (probabilities are uniformly distributed).

Specifying bonus roll chance: (optional (default is 0 rolls))

```groovy
.bonusRollsRange(float) // (1)!
.bonusRollsRange(float, float) // (2)!
```

1. The loot pool will always generate the specified number of bonus rolls.
2. Specifies a minimum number of bonus rolls and a maximum number of bonus rolls respectivly (probabilities are uniformly distributed).

Adding a random chance: (optional)

```groovy
.randomChance(float) // (1)!
.randomChanceWithLooting(float /* (2)! */, float /* (3)! */)
```

1. The will only be rolled if the specified random chance (as a float [0, 1]) is successful.
2. random chance (as a float [0, 1]).
3. looting multiplier which is multiplied with the looting level and added to the random chance.

Adding loot conditions: (optional)

```groovy
.killedByPlayer() // (1)!
.killedByNonPlayer() // (2)!
.condition(LootCondition) // (3)!
.condition{ java.util.Random /* (4)! */, net.minecraft.world.storage.loot.LootContext /* (5)! */ -> boolean /* (6)! */ }
```

1. An entity must be killed by a player for this pool to be rolled.
2. An entity must be killed by a non-player for this pool to be rolled.
3. This method exists so you can define and add a custom loot condition which implements net.minecraft.world.storage.loot.conditions.LootCondition.
4. An instance of java.util.Random seeded by minecraft.
5. The current LootContext which contains info about the player, world, etc.
6. LootCondition closures must return a boolean. If true the LootPool will be rolled, if false it will not.

Build the LootPool: (returns LootPool)

```groovy
.build() // (1)!
```

1. Useful for saving a pool so it can be added to many tables manually using LootTable.addPool(LootPool)

Register LootPool: (returns nothing)

```groovy
.register() // (1)!
```

1. Builds the loot pool and adds it to the specified table.

!!! example

    Let's add a new loot pool with a condition that rolling a nat 20 makes slain chickens drop a diamond.

    ```groovy
    loot.poolBuilder()
        .table('minecraft:entities/chicken')
        .name('main2')
        .entry(item('minecraft:diamond'), 1)
        .randomChance(0.05f)
        .register()
    ```

    The same thing could also be acomplished through using a condition closure.

    ```groovy
    loot.poolBuilder()
        .table('minecraft:entities/chicken')
        .name('main2')
        .entry(item('minecraft:diamond'), 1)
        .condition{ Random random, LootContext context -> random.nextFloat() < 0.05f } // (1)!
        .register()
    ```

    1. Don't forget to import java.util.Random and net.minecraft.world.storage.loot.LootContext

## Removing a LootPool

```groovy
LootTable.removePool(String)
```

!!! example

    ```groovy
    def chickenLootTable = loot.getTable('minecraft:entities/chicken')
    chickenLootTable.removePool('main')
    ```

## Modifying a LootPool

You can fetch and store a loot table to modify like so

```groovy
LootTable.getPool(String)
```

!!! example

    ```groovy
    def zombieMainLootPool = loot.getTable('minecraft:entities/zombie').getPool('main')
    ```

Read more about modifying loot pools on the [next page](./lootentry.md).
