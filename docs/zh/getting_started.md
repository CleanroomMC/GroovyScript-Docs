# 入门指南

虽然不一定需要编程知识，但拥有这方面的知识将对你有很大帮助。<br>
作为文本编辑器，你可以很好地使用[Notepad++](https://notepad-plus-plus.org/downloads/)。（我们将来会致力于提供更好的替代品）

1. 下载并安装Minecraft Forge 1.12.2
2. 下载GroovyScript的最新版本[在这里](https://www.curseforge.com/minecraft/mc-mods/groovyscript/files)
   并将其放入mods文件夹
3. 同样安装[MixinBooter](https://www.curseforge.com/minecraft/mc-mods/mixin-booter/files)，因为GroovyScript
   依赖于它
4. 在没有添加任何文件的情况下启动Minecraft
5. GroovyScript将创建几个文件
    - groovy.log (参见[Groovy 日志](#groovy-log))
    - groovy/runConfig.json (参见[运行配置](#run-config))
    - groovy/postInit/main.groovy (默认脚本文件)

## Groovy 日志

与Groovy相关的所有内容都有其自己的日志，并生成自己的文件。如果在脚本中遇到问题，你应该首先查看这里。
文件目录始终为`[Minecraft实例路径]/groovy.log`

## 运行配置

此文件定义了每个脚本文件应该如何执行。它还可以存储有关Mod包的一些一般信息。如果该文件不存在，将会生成它。
如果你不理解这是什么或者如何工作，你可以跳过这一部分。你只需要知道将你的带有配方的脚本放在 `groovy/postInit`，
而带有像物品创建之类的内容的脚本放在 `groovy/preInit`。<br>
让我们看看文件可能是什么样子。

```json
{
  "packName": "",
  "packId": "",
  "version": "1.0.0",
  "debug": false,
  "classes": [
    "classes/"
  ],
  "loaders": {
    "preInit": [
      "preInit/"
    ],
    "postInit": [
      "postInit2/"
    ]
  }
}
```

让我们逐个部分来看：<br>

- `packName` 是包的名称（参见[包名和ID](#pack-name-and-id)）。对于[内容](groovyscript/content/content.md)很重要。<br>
- `packId` (0.4.0+) 是包的ID（参见[包名和ID](#pack-name-and-id)）。对于[内容](groovyscript/content/content.md)很重要。<br>
- `version` 是包的版本。目前它并没有特殊用途。<br>
- `debug`：如果为false，则所有记录到调试的消息都不会被记录。用于调试非常方便。<br>
- `classes`：(0.3.0+) 此处应指定包含单个类的文件。它确保在脚本尝试访问它们时加载类。<br>
- `loaders`：这定义了在什么阶段加载什么文件。默认情况下，有两个阶段：`preInit` 和 `postInit`。<br>
- `preInit` 将在早期阶段运行。不要在这里注册配方。使用它来注册游戏对象，如物品和方块。<br>
- `postInit` 将在JEI加载之前运行。例如，用于注册配方。当GroovyScript重新加载时，只有这个加载器会运行。<br>
  在加载器的方括号内，我们定义将要运行的文件或路径。你不能在多个加载器中运行一个文件。
  列表中较高的元素将首先运行。文件可以多次放置，但它们只会执行一次。<br>

!!! 例子 "例如："

    ```json
    [
    "postInit/ore_dict.groovy",
    "postInit/"
    ]
    ```

    这里首先会执行 `ore_dict.groovy`，然后执行所有位于 `postInit/` 的文件，但由于 `ore_dict.groovy` 已经被执行，
    所以它现在不会再运行。<br>

!!! 例子 "另一个例子："

    ```json
    [
    "postInit/",
    "postInit/late_stuff.groovy"
    ]
    ```

首先会执行 `postInit/` 中的所有内容，但由于 `late_stuff.groovy` 具体放在后面，它将不会被执行。
之后只有 `late_stuff.groovy` 会被执行。

### 包名和ID

包名可以是任何内容。这是将显示在JEI中，你所创建的物品的工具提示中的名称。<br>
包ID非常重要。它只能由小写字母和 `_` 组成。

!!! 警告
    更改包ID将导致在现有世界中创建的物品丢失！

## 重要信息

1. Groovy脚本必须以`.groovy`结尾
2. Groovy脚本必须以某种方式在[运行配置](#run-config)中定义以执行
3. 脚本和文件夹可以使用任何名称
4. 所有脚本和[运行配置](#run-config)必须位于`[Minecraft实例路径]/groovy/`