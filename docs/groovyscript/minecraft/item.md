# Items

Item stacks can be obtained with the item bracket handler.

```groovy
def iron_ingot = item('minecraft:iron_ingot', 4) * 6
```

The 4 inside the () is the metadata. Iron ingot doesn't have any sub items so it will result in an item that doesn't actually exist.
The `* 6` at the end marks the amount. The item id `'minecraft:iron_ingot'` is a string and can be replaced by anything that makes a string. <br>
The following also returns a iron ingot.

```groovy
def iron_ingot = 'iron_ingot'
item("minecraft:$iron_ingot")
```

## NBT

Nbt data is minecraft data format used for items and world saving. Adding a nbt tag is easy.

```groovy
itemStack.withNbt(Map<String, Object> map)
```

Now this looks complicated, but it isn't.

```groovy
item('minecraft:iron_ingot').withNbt([Name: 'Epic Ingot'])
```

### More

- `.withNbt(null)` removes the nbt tag
- `.withEmptyNbt()` adds an empty nbt tag

## Match Conditions

This allows for dynamic item checking in recipes.
!!! Note
    At this moment (ver. 0.3.1) only crafting and Draconic Evolution fusion crafting is supported.

```groovy
itemStack.when(Closure<Boolean> condition)
```

!!! Example
    ```groovy
    item('minecraft:iron_axe:*').when({stack -> stack.getDamage() < 50})
    ```

Let's see what this does. First `item('minecraft:iron_axe:*')` matches an iron axe with any damage.
Then `.when({stack -> stack.getDamage() < 50})` only validates items that have taken less than 50 damage.

## Transformer

This transforms an item ingredient to a new item on craft. For example a water bucket returns an empty bucket after crafting.

!!! Note
    This only works for crafting.

```groovy
itemStack.transform(Closure<ItemStack> transformer)
```

!!! Example
    ```groovy
    def transformer = { stack -> stack.copyWithMeta(stack.getItemDamage() + 1)}
    item('minecraft:iron_axe:*').transform(transformer)
    ```

First we create a transformer closure, so we can easier see what's going on. It simply creates a new item with one more damage.
In the second line that transformer is applied to the item. So at the end when you craft a recipe with that iron axe it will get damaged by 1.

### Default Transformer

- `.noreturn()` will not return anything. Useful when you want to consume a water bucket with the bucket for example.
- `.reuse()` will return itself. That means the item will not be consumed.

## Comparing items
Sometimes you want to check if items are equal to each other. This is more complicated than it sounds.
Using `==` will almost always fail. Instead, you can use `in` operator. It compares the item, meta and nbt data.
The count is ignored.
???+ Example
    ```groovy
    def wool0 = item('minecraft:wool', 0)
    def wool1 = item('minecraft:wool', 1)
    println wool0 in wool1                          // false, since different meta
    println item('minecraft:wool', 0) in wool0      // true, since same item and meta
    println item('minecraft:wool', 0) * 5 in wool0  // true, amount is ignored
    ```

If you want to check if two items are exactly equal with count you need to use `ItemStack.areItemsEqual(ItemStack, ItemStack)`.
???+ Example
    ```groovy
    def wool0 = item('minecraft:wool', 0)
    def wool1 = item('minecraft:wool', 1)
    println ItemStack.areItemsEqual(wool0, wool1)                       // false
    println ItemStack.areItemsEqual(item('minecraft:wool', 0), wool1)   // true
    println ItemStack.areItemsEqual(item('minecraft:wool', 0) * 5, wool1)   // false
    ```

You can also use the `in` operator if it matches any `IIngredient`.
???+ Example
    ```groovy
    println item('minecraft:iron_ingot') in ore('ingotIron') // true
    println ore('ingotIron') in item('minecraft:iron_ingot') // false, the iron ingot is in the ore dict and not vice versa.
    ```

To elevate the level of cursedness you can use `<<` and `>>` to further compare items.
`<<` is exactly like the `in` operator, but the count of the ingredient must also be greater or equal to the item on the left side.
`>>` is the same thing but sides swapped.