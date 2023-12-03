# 资源位置入门

Minecraft的资源位置通常用作物品的标识符，同时也用于资产文件（如模型和纹理）的位置。它由两个字符串组成：域（domain）和路径（path）。域通常是一个mod id。路径是一个名称（对于物品）或路径（对于文件）。资源位置可以表示为 `domain:path`。资源位置不能包含任何特殊字符。不允许大写字母，但允许数字和下划线。

## 创建资源位置
有两种方法：

1. 使用 `net.minecraft.util.ResourceLocation` 构造函数（自0.4.0版本以来，此类被自动导入）
    - `new ResourceLocation("domain:path")`
    - `new ResourceLocation("domain", "path")`
    - `new ResourceLocation("path")`（默认为 `minecraft` 域）
2. 使用 `resource()` 游戏对象处理器（类似全局方法）
    - `resource("domain:path")`
    - `resource("domain", "path")`
    - `resource("path")`（默认为运行配置中指定的包ID（参见[此处](../getting_started.md#run-config)））

我们可以看到，这两种方法大部分相同，只是游戏对象处理器默认为包ID而不是minecraft。这种方式是首选方式。

???+ 示例
    ```groovy
    // 以下两行是相等的
    def rl1 = resource("groovyscript", "path/to/file") // groovyscript:path/to/file
    def rl2 = resource("groovyscript:path/to/file") // groovyscript:path/to/file
    // 如果未指定，域会默认为包ID
    def rl3 = resource("furnace") // packid:furnace
    ```

在GroovyScript中，通常存在一些重载，你可以直接插入mod id和路径，而无需创建 `ResourceLocation`。<br>

## 转换为文件路径

在以下内容中，`.../.minecraft/` 是实例文件夹。<br>
`.minecraft/resources/` 是根资源文件夹（需要Resource Loader模组）。只要Minecraft知道它，资源可以位于任何有效路径中。
自0.4.0版本起，根文件夹还可以是 `.minecraft/groovy/assets/`。资源包也是加载资源的有效方式。<br>
整个路径由以下组成

- 根路径
- 域（mod id）
- 路径（资源位置的路径）

格式化为：`rootPath/domain/path`

## 示例

在这里，我们使用 `.minecraft/resources` 作为根。

| 资源位置                                 | 对应的文件路径                                           |
|------------------------------------------|----------------------------------------------------------|
| `minecraft:textures/gui/button.png`      | `.minecraft/resources/minecraft/textures/gui/button.png` |
| `textures/gui/button.png`                | `.minecraft/resources/minecraft/textures/gui/button.png` |
| `thaumcraft:research/SOME_RESEARCH.json` | `.minecraft/resources/thaumcraft/research/SOME_RESEARCH.json` |

## 模型文件

在模型或blockstate JSON文件中，你可能还会发现资源位置。以 `assets/minecraft/models/block/andesite.json` 为例（`assets` 是根文件夹）。在其中，你会发现

```json
{
  "parent": "block/cube_all",
  "textures": {
    "all": "blocks/stone_andesite"
  }
}
```

在这里，`"block/cube_all"` 和 `"blocks/stone_andesite"` 都是资源位置。因此，你可能认为纹理位于 `assets/minecraft/blocks/stone_andesite`，但事实并非如此。
实际路径是 `assets/minecraft/textures/blocks/stone_andesite.png`。其原因是Minecraft知道它应该指向一个纹理，并在路径前面添加了 `textures/` 并在路径末尾添加了 `.png`。
对于 `"parent": "block/cube_all"` 也是类似的，只不过它指向另一个模型。

## 其他用途

资源位置还用作游戏注册表条目（例如物品）的标识符。<br>
当你使用物品方括号处理程序时，你会做类似于 `item('minecraft:iron_ingot')` 的操作。是的，`'minecraft:iron_ingot'` 是一个资源位置，只不过它并不指向资源。
对于像物品这样的游戏对象，资源位置也被称为注册表名。

!!! 注意
    请注意，你不能使用 `item('iron_ingot')`。这被GroovyScript禁用。你必须始终输入完整的注册表名。