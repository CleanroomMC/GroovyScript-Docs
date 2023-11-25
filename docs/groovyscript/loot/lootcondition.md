# LootConditions

Loot conditions are conditions which must be met for the given loot to be rolled, they can be added to pools and entries. Groovy provides some common loot conditions such as:

```groovy
.killedByPlayer() // (1)!
.killedByNonPlayer() // (2)!
.randomChance(float) // (3)!
.randomChanceWithLooting(float /* (4)! */, float /* (5)! */)
```

1. An entity must be killed by a player for this entry to be rolled.
2. An entity must be killed by a non-player for this entry to be rolled.
3. The will only be rolled if the specified random chance (as a float [0, 1]) is successful.
4. random chance (as a float [0, 1]).
5. looting multiplier which is multiplied with the looting level and added to the random chance.

For use in pool builders and entry builders.

## Custom LootConditions

You can pass a [groovy closure](../../../groovy/closure.md) to `loot.condition()` for use in a builder or to store as a groovy variable.

!!! example

    ```groovy
    loot.poolBuilder()
        .table('minecraft:entities/chicken')
        .name('main2')
        .entry(item('minecraft:diamond'))
        .condition{ random, context -> random.nextFloat() < 0.05f } // (1)!
        .register()
    ```

    1. The parameters of the closure should be java.util.Random and net.minecraft.world.storage.loot.LootContext (in that order).

    ```groovy
    def nat20Condition = loot.condition{ Random random, LootContext context -> random.nextFloat() < 0.05f } // (1)!

    loot.poolBuilder()
        .table('minecraft:entities/chicken')
        .name('main2')
        .entry(item('minecraft:diamond'))
        .condition(nat20Condition)
        .register()
    ```

    1. Don't forget to import the classes if specifying types.
