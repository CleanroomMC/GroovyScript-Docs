# LootFunctions

Loot functions are modifications to the item that a player rolls from a LootTable, they can be added to loot entries. Loot functions are always applied to the LootEntries item unless a condition(s) is specified, in which case the condition must be met for the function to be applied. Groovy provides some common loot functions such as:

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

For use in LootEntry builders.

## Custom LootFunctions

You can pass a [groovy closure](../../../groovy/closure.md) to `loot.function()` for use in a builder or to store as a groovy variable.

!!! example

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

    ```groovy
    def nat20Condition = loot.condition{ Random random, LootContext context -> random.nextFloat() < 0.05f }
    def lootPinataFunction = loot.function({ ItemStack stack, Random random, LootContext context ->
        stack.setCount(10)
        return stack
    }, nat20Condition)

    loot.entryBuilder()
        .table('minecraft:entities/chicken')
        .pool('main')
        .item(item('minecraft:potato'))
        .function(lootPinataFunction)
        .smelt()
        .register()
    ```
