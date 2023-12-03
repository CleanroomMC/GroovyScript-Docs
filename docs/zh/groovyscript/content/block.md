# 创建方块

## 最简单的方法

```groovy
content.createBlock(String name).register()
```

很简单对吧？
让我们来分解一下：

- `content` 是一个全局变量。
- `createBlock(String name)` 创建一个方块和一个物品版本并返回它。名称是注册名，必须只包含小写字母和 `_`。
- `register()` 注册方块和物品。如果没有这个，方块将不会出现在游戏中。

## 注册方块

上面的示例为您创建了一个简单的方块，但是您也可以自己创建方块（以创建自定义行为）。
使用以下方法注册自定义方块。

```groovy
content.registerBlock(String name, Block block)
content.registerBlock(String name, Block block, ItemBlock block)
```

## 纹理

Minecraft 的方块需要纹理（或多个纹理）、一个模型文件来描述纹理的渲染方式，以及一个方块状态文件，将每个方块状态指向一个模型文件。如果 Groovy
找不到模型文件或方块状态文件，它将在 `.minecraft/groovy/assets/[pack id]/models/block/[block name].json` 和 `.minecraft/groovy/assets/[pack id]/blockstates/[item name].json` 生成默认文件。
它将指向一个纹理，您需要将其放置在 `.minecraft/groovy/assets/[pack id]/textures/blocks/[block name].png`。

## 翻译物品名称

默认情况下，物品的名称将显示为 `tile.[pack id].[block name].name`。要更改这一点，您需要在 lang 文件中添加一个条目。GroovyScript 在 `.minecraft/groovy/assets/[pack id]/lang/en_us.lang` 生成默认的 lang 文件。

!!! 示例

    首先创建一个方块

    ```groovy
    content.createBlock('dust_block')
    ```

    假设包 id 为 `nomifactory`，因此物品和方块 id 将为 `nomifactory:dust_block`。
    将以下行插入 lang 文件中。

    ```mclang
    tile.nomifactory.dust_block.name=宇宙之心
    ```

    （`tile.nomifactory.dust_block.name` 是默认生成的翻译键。您可以更改为任何您想要的内容。）<br>
    最后，在 `.minecraft/groovy/assets/nomifactory/textures/items/dust_block.png` 放置一个纹理。