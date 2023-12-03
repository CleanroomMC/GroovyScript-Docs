# 制作台

## 添加有形状的合成配方

```groovy
// 常规添加
crafting.addShaped(ItemStack output, List<List<IIngredient>> input) // （1）！
crafting.addShaped(String name, ItemStack output, List<List<IIngredient>> input) // （2）！

// 替换添加
crafting.replaceShaped(ItemStack output, List<List<IIngredient>> input) // （3）！
crafting.replaceShaped(String name, ItemStack output, List<List<IIngredient>> input) // （2）！
```

1. 如果未提供，系统将为您自动生成一个配方名称。
2. 在签名中的 `List<List<IIngredient>>` 一开始可能看起来有些复杂。请参阅有形状配方示例，以获取更好的表示。
3. `replace` 方法将删除所有输出指定输出的配方，并添加新配方 - 替换旧配方。

!!! 示例

```groovy
crafting.addShaped('balanced_clay', item('minecraft:clay_ball') * 3, [
        [item('minecraft:nether_star'), null, item('minecraft:nether_star')],
        [null, ore('ingotIron'), null], // （1）！
        [item('minecraft:nether_star'), null, item('minecraft:nether_star')]
])

crafting.addShaped('balanced_clay_2x2', item('minecraft:clay_ball') * 2, [
        [item('minecraft:nether_star'), null],
        [null, ore('ingotIron')], // （2）！
])
```

1. 使用 `null` 来指定一个空槽位。
2. 您可以缩小列表的大小以获得更小的配方 - 这是一个 2x2 的配方。只需确保它不是锯齿状的（每行/列的长度不同）。

## 添加无形状的合成配方

与其他配方类型不同，无形状的合成也不使用配方构建器。

```groovy
// 常规添加
crafting.addShapeless(ItemStack output, List<IIngredient> input) // （1）！
crafting.addShapeless(String name, ItemStack output, List<IIngredient> input)

// 替换添加
crafting.replaceShapeless(ItemStack output, List<IIngredient> input) // （2）！
crafting.replaceShapeless(String name, ItemStack output, List<IIngredient> input)
```

1. 如果未提供，系统将为您自动生成一个配方名称。
2. `replace` 方法将删除所有输出指定输出的配方，并添加新配方 - 替换旧配方。

!!! 示例

```groovy
crafting.addShapeless('unbalanced_clay', item('minecraft:clay_ball') * 32, [item('minecraft:dirt'), item('minecraft:dirt'), item('minecraft:leather')])
```

## 移除配方

{--
您还可以在创造模式中使用 JEI/HEI 轻松删除配方。
找到要删除的配方，然后单击 `[X]` 按钮将删除配方的代码复制到剪贴板。
然后只需将代码粘贴到所需的脚本中，就可以了！
--}
（计划功能）

您可以在启用了 `F3+h` 模式的情况下，通过将鼠标悬停在输出上，查看 JEI/HEI 中的配方名称。

```groovy
crafting.remove(String name) // 移除具有相同名称的配方
crafting.removeByOutput(IIngredient output) // 移除所有输出为指定物品的配方
```