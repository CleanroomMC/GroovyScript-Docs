# 使用 RecipeBuilder 添加合成配方

合成也有一个 RecipeBuilder。
如果你不知道什么是 builder，请查看[这里](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/)！

你可以使用 `shapedBuilder()` 或 `shapelessBuilder()` 来启动 builder 链，这决定了你要添加的配方类型。

```groovy
crafting.shapedBuilder()
crafting.shapelessBuilder()
```

然后，您可以调用 builder 上的其他方法（如 `.name()`、`.replace()` 等）来构建最终结果。查看下面的示例，以获取完整的图片。

设置配方名称（可选）：

```groovy
name(String name) // （1）！
```

1. 如果未提供，系统将为您自动生成一个配方名称。

设置配方产出（必需）：

```groovy
output(ItemStack item)
```

设置配方函数（可选）：

```groovy
recipeFunction(Closure<ItemStack> recipeFunction) // （1）！
```

1. 有关详细信息，请参阅 [Recipe Function and Action 页面](./crafting.md)。

设置配方动作（可选）：

```groovy
recipeFunction(Closure<Void> recipeAction) // （1）！
```

1. 有关详细信息，请参阅 [Recipe Function and Action 页面](TODO)。

设置替换其他配方的配方（可选）：

```groovy
replace() // （1）！
```

1. 有关这些内容的详细信息，请参阅 [Crafting 页面](https://groovyscript-docs.readthedocs.io/en/latest/groovyscript/minecraft/crafting/)。

设置替换其他配方的配方（按名称）（可选）：

```groovy
replaceByName() // （1）！
```

1. 有关这些内容的详细信息，请参阅 [Crafting 页面](https://groovyscript-docs.readthedocs.io/en/latest/groovyscript/minecraft/crafting/)。
它的功能与上面的相同，只是它匹配提供的配方名称。

设置是否允许网格镜像（可选，仅对有形状的有效）：

```groovy
mirrored()
mirrored(boolean mirrored) // （1）！
```

1. 选择配方是否是镜像的，默认为 false。

创建配方布局（必需，仅对有形状的有效）：

```groovy
matrix(String... matrix)
shape(String... matrix) // 与 matrix() 执行相同的操作
// 以非构建器形式输入矩阵的样式
matrix(List<List<IIngredient>> matrix)
shape(List<List<IIngredient>> matrix)
```

将配方布局中的成分与之匹配（必需，仅对有形状的有效）：

```groovy
key(String c, IIngredient ingredient) // （1）！
```

1. 请参阅下面的示例，以更好地理解它的工作原理。

将输入添加到配方（必需，仅对无形状的有效）：

```groovy
input(IIngredient ingredient)
input(IIngredient... ingredients)
input(Collection<IIngredient> ingredients)
```

注册配方（必需）：

```groovy
register()
```

!!! 示例

阅读上面的内容可能会让这显得相当复杂。我们保证它并不复杂！

=== "有形状的"

    ```groovy
    // 有形状的配方
    crafting.shapedBuilder()                    // 创建一个新的有形状的配方
            .name('balanced_clay')              // 将配方命名为 'balanced_clay'
            .output(item('minecraft:clay') * 32)      // 输出 32 个黏土
            .matrix('NIN',                      // 为配方创建布局
                    'DSD',                      // 每个字符表示一个插槽
                    'NIN')
            .key('N', item('minecraft:nether_star'))  // 在布局中的每个 'N' 处使用下界之星
            .key('I', ore('ingotIron'))               // 所有 'I' 字符都是铁锭
            .key('D', item('minecraft:diamond'))      // 所有 'D' 字符都是钻石
            .key('S', ore('stone'))                   // 所有 'I' 字符都是石头
            .register()                         // 注册配方
    ```

=== "无形状的"

    ```groovy
    // 无形状的配方
    crafting.shapelessBuilder()                                     // 添加一个新的无形状的配方
            .name('balanced_clay_v3')                               // 将配方命名为 'balanced_clay_v3'
            .output('minecraft:clay' * 2)                           // 输出 2 个黏土
            .input('minecraft:iron_ingot')                          // 将一个铁锭添加到输入
            .input('minecraft:iron_ingot')                          // 将第二个铁锭添加到输入
            .input('minecraft:gold_nugget', 'minecraft:diamond')    // 将金粒和钻石添加到输入
            .register()
    ```

!!! 注意
    如果要使插槽为空，请不要使用键和