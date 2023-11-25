# LootTables

## Adding a LootTable

Registering a new loot table is currently unsupported, since groovyscript does not yet have the capability to add entities and structures that could be assigned these loot tables.

## Removing a LootTable

```groovy
loot.removeTable(String)
loot.removeTable(ResourceLocation)
```

!!! example

    ```groovy
    loot.removeTable("minecraft:entities/chicken")
    loot.removeTable(resource("minecraft:entities/chicken"))
    ```

## Modifying a LootTable

You can fetch and store a loot table to modify like so

```groovy
loot.getTable(String)
loot.getTable(ResourceLocation)
```

!!! example

    ```groovy
    def zombieLootTable = loot.getTable("minecraft:entities/zombie")
    def chickenLootTable = loot.getTable(resource("minecraft:entities/chicken"))
    ```

Read more about modifying loot pools on the [next page](./lootpool.md).
