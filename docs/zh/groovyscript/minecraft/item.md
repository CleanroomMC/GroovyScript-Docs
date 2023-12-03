# 物品

物品堆栈可以通过物品括号处理器获得。

```groovy
def iron_ingot = item('minecraft:iron_ingot', 4) * 6
```

括号中的 4 是元数据。铁锭没有任何子物品，因此将导致一个实际上不存在的物品。
末尾的 `* 6` 表示数量。物品ID `'minecraft:iron_ingot'` 是一个字符串，可以用任何生成字符串的内容替换。<br>
以下也会返回一个铁锭。

```groovy
def iron_ingot = 'iron_ingot'
item("minecraft:$iron_ingot")
```

## NBT

NBT 数据是用于物品和世界保存的 Minecraft 数据格式。添加一个 NBT 标签很容易。

```groovy
itemStack.withNbt(Map<String, Object> map)
```

现在这看起来复杂，但实际上并不复杂。

```groovy
item('minecraft:iron_ingot').withNbt([Name: 'Epic Ingot'])
```

### 更多

- `.withNbt(null)` 移除 NBT 标签
- `.withEmptyNbt()` 添加一个空的 NBT 标签

## 匹配条件

这允许在配方中进行动态物品检查。
!!! 注意
    目前（版本 0.3.1），仅支持合成和龙之进化融合合成。

```groovy
itemStack.when(Closure<Boolean> condition)
```

!!! 示例
    ```groovy
    item('minecraft:iron_axe:*').when({stack -> stack.getDamage() < 50})
    ```

让我们看看这是做什么的。首先 `item('minecraft:iron_axe:*')` 匹配任何损伤的铁斧。
然后 `.when({stack -> stack.getDamage() < 50})` 只验证已受损伤少于 50 的物品。

## 转换器

这将物品配料转换为合成时的新物品。例如，一个水桶在合成后返回一个空桶。

!!! 注意
    这仅适用于合成。

```groovy
itemStack.transform(Closure<ItemStack> transformer)
```

!!! 示例
    ```groovy
    def transformer = { stack -> stack.copyWithMeta(stack.getItemDamage() + 1)}
    item('minecraft:iron_axe:*').transform(transformer)
    ```

首先我们创建一个转换器闭包，以便更容易看到发生了什么。它简单地创建一个新的带有更多损伤的物品。
在第二行，该转换器被应用于物品。因此，在合成带有该铁斧的配方时，它的损伤将增加 1。

### 默认转换器

- `.noreturn()` 将不返回任何东西。在你想要消耗一个水桶和桶的情况下很有用。
- `.reuse()` 将返回自身。这意味着物品不会被消耗。