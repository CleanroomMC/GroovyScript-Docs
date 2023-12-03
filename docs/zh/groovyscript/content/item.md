# 创建物品

## 最简单的方式

```groovy
content.createItem(String name).register()
```

简单吧？
我们来分解一下：

- `content` 是一个全局变量。
- `createItem(String name)` 创建一个物品并返回它。名称是注册名称，只能包含小写字母和 `_`。
- `register()` 注册这个物品。如果没有这个，物品将不会出现在游戏中。

## 注册物品

上面的例子为您创建了一个简单的物品，但您也可以自己创建物品（以创建自定义行为）。
使用以下方法注册自定义物品。

```groovy
content.registerItem(String name, Item item)
```

## 纹理

Minecraft 的物品需要一个纹理（或多个纹理）和一个描述纹理如何渲染的模型文件。如果 GroovyScript 找不到模型文件，它将生成一个默认文件
在 `.minecraft/groovy/assets/[pack id]/models/item/[item name].json`。
它将指向一个您需要放置的纹理
在 `.minecraft/groovy/assets/[pack id]/textures/items/[item name].png`。

## 翻译物品名称

默认情况下，物品名称将显示为 `item.[pack id].[item name].name`。要更改它，您需要在 lang 文件中添加一个条目。
GroovyScript 会在 `.minecraft/groovy/assets/[pack id]/lang/en_us.lang` 生成一个默认 lang 文件。

!!! 示例

    首先创建一个物品

    ```groovy
    content.createItem('heart_of_the_universe')
    ```

    假设包 id 是 `nomifactory`，以便物品 id 将是 `nomifactory:heart_of_the_universe`。
    将此行插入 lang 文件。

    ```mclang
    item.nomifactory.heart_of_the_universe.name=Heart of the universe
    ```

    (`item.nomifactory.heart_of_the_universe.name` 是默认生成的翻译键。您可以更改为任何内容。) <br>
    最后，在 `.minecraft/groovy/assets/nomifactory/textures/items/heart_of_the_universe.png` 放置一个纹理。