# 工作台

## 添加有序合成

```groovy
// 常规方法
crafting.addShaped(ItemStack output, List<List<IIngredient>> input) // (1)
crafting.addShaped(String name, ItemStack output, List<List<IIngredient>> input) // (2)

// "替换"方法
crafting.replaceShaped(ItemStack output, List<List<IIngredient>> input) // (3)
crafting.replaceShaped(String name, ItemStack output, List<List<IIngredient>> input) // (2)
```

1. 你也可以省略配方ID, 它将会自动指定.
2. `List<List<IIngredient>>` 初看或许有些难以理解. 看看例子或许会更易理解一些.
3. `replace` 方法会先移除所有输出配方, 然后再添加你写的新配方.

### 例子
```groovy
crafting.addShaped('balanced_clay', item('minecraft:clay_ball') * 3, [
        [item('minecraft:nether_star'), null, item('minecraft:nether_star')],
        [null, ore('ingotIron'), null], // (1)
        [item('minecraft:nether_star'), null, item('minecraft:nether_star')]
])

crafting.addShaped('balanced_clay_2x2', item('minecraft:clay_ball') * 2, [
        [item('minecraft:nether_star'), null],
        [null, ore('ingotIron')], // (2)
])
```

1. 和CrT一样, 我们用 `null` 表示空.
2. 你可以缩小配方的尺寸(即2x2,1x1), 但你应保证每行/列的长度相同.

## 添加无序合成
Unlike other recipe types, Shapeless Crafting also does not use a recipe builder.

```groovy
// 一般方法
crafting.addShapeless(ItemStack output, List<IIngredient> input) // (1)
crafting.addShapeless(String name, ItemStack output, List<IIngredient> input)

// "替换"方法
crafting.replaceShapeless(ItemStack output, List<IIngredient> input) // (2)
crafting.replaceShapeless(String name, ItemStack output, List<IIngredient> input)
```

1. 一样的, 你也可以省略配方ID, 它将会自动指定.
2. `replace` 方法会先移除所有输出配方, 然后再添加你写的新配方.

### 例子
```groovy
crafting.addShapeless('unbalanced_clay', item('minecraft:clay_ball') * 32, [item('minecraft:dirt'), item('minecraft:dirt'), item('minecraft:leather')])
```

## 删除配方
{--
你可以在创造模式下用JEI/HEI轻松移除配方. 
找到你要移除的配方, 单击 `[X]` 按钮, 它会把自动生成的代码复制到你的剪贴板上.
然后你懂的,复制黏贴走起!
--}
(计划中的功能)

按下 "F3+h "后, 将鼠标悬停在输出上, 即可查看 JEI/HEI 中的配方ID.

```groovy
crafting.remove(String name) // 以配方ID为依据删除配方
crafting.removeByOutput(IIngredient output) // 以输出物品为依据删除配方
```
