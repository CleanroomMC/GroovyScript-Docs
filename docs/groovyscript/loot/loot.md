# Loot

This part of GroovyScript allows for the modification of LootTables. It's equivalent to LootTweaker for CraftTweaker, but for GroovyScript it doesn't require another mod.

!!! Note
    Requires at least version 0.7.0. <br>
    Works for all loot tables (including those added by mods).

## Visualizing LootTables

The following methods are availble for viewing in game loot tables.

```groovy
loot.printTables() // (1)!
loot.printPools() // (2)!
loot.printPools(String tableResourceLocation) // (3)!
loot.printEntries() // (4)!
loot.printEntries(String tableResourceLocation) // (5)!
loot.printEntries(String tableResourceLocation, String poolResourceLocation) // (6)!
```

1. Prints the resource locations of all currently loaded LootTables.
2. Prints the resource locations of all currently loaded LootPools.
3. Prints the resource locations of all LootPools in the specified LootTable.
4. Prints the items of all currently loaded LootEntries.
5. Prints the items of all LootEntries in the specified LootTable.
6. Prints the items of all LootEntries in the specified LootPool.

!!! example

    Below is an example what the output of `loot.printEntries()` looks like in [groovy.log](../../../getting_started.md/#groovy-log)
    ```
    minecraft:entities/shulker
        - main
            - minecraft:shulker_shell
    minecraft:entities/wither_skeleton
        - main
            - minecraft:coal
        - pool1
            - minecraft:bone
        - pool2
            - minecraft:skull
    ...
    ```
