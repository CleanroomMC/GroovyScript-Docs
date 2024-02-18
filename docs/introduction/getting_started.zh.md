# 让我们开始

哦不不, 读懂这不一定需要太多的编程知识, 但会对你有很大的帮助.
作为文本文件(.groovy), 你可以使用[VSCode](https://code.visualstudio.com/)来打开并且编写Groovy文件, 或者是一个更像样的IDE. (我们将在未来开发一个更好的替代品)

1. 下载 Minecraft和Forge 1.12.2并且安装它. (我想你的启动器应该可以)
2. 下载最新版的GroovyScript([点这里](https://www.curseforge.com/minecraft/mc-mods/groovyscript/files))
   并且丢到你的mods文件夹里去. (HMCL等主流启动器支持直接从CurseForge下载模组)
3. 另外, 你还需要安装一个[MixinBooter](https://www.curseforge.com/minecraft/mc-mods/mixin-booter/files), 因为GroovyScript依赖于它.
4. 启动游戏, 并且往groovy文件夹里丢一些脚本.
5. 第一次启动时, GroovyScript将生成以下文件
    - groovy.log (即[Groovy Log](#groovy-log))
    - groovy/runConfig.json (即[Groovy运行配置](#run-config))
    - groovy/postInit/main.groovy (默认提供的脚本实例文件)

## Groovy log

所有与groovy有关的东西都有自己的日志, 而且会生成自己的文件.
如果你的脚本写出了问题, 你应该先看看Log. 文件位于[Minecraft实例路径]/groovy.log

## 运行配置
这个文件定义了每个脚本文件应该如何执行, 在哪个加载阶段执行.
它也可以存储一些关于MOD包的一般信息.
如果该文件无法被查找到或不存在, 将重新生成一份.
如果你不明白这是什么或 "它是如何工作的" , 你可以跳过配置.
你所需要知道的是, 你把你的配方脚本放在groovy/postInit中.
诸如 "自定义物品" 之类的脚本则放在groovy/preInit中.
(类似KubeJS的start_scripts-preInit和server_scripts-postInit)
让我们看看这个文件是什么样子的.

````json
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
````

让我们一点一点地过一遍: <br>

- `packName` 是mod包的名称 (参见 [mod包的名称和id](#pack-name-and-id)). 对 [content](../groovyscript/content/content.md) 是必要的. <br>
- `packId` (0.4.0+) 是mod包的Id (参见 [mod包的名称和id](#pack-name-and-id)). 对 [content](../groovyscript/content/content.md) 是必要的. <br>
- `version` 是mod包的版本. 它暂无任何特殊功能. <br>
- `debug`: 如果为假,则不会记录debug信息. 是调试的好帮手. <br>
- `classes`: (0.3.0+) 在此指定包含单个类的文件. 它可确保在脚本尝试访问时装载类. <br>
- `loaders`: 这定义了应在哪个阶段加载相应文件. 默认情况下,有两个阶段: `preInit`
  和 `postInit`. <br>
- `preInit` 将在早期阶段运行. 不要在此注册配方. 我们用它来注册游戏对象(即"自定义物品"),如物品和方块. <br>
- `postInit` 将在 JEI 加载前运行. 我们可以用它来注册配方. 当重新加载 GroovyScript 时 只有它会运行.<br>
在加载器的方括号内, 我们可以指定将要运行的文件或路径. 但要注意的是一个文件不能在多个加载器中运行.
并且它是顺序读取, 这意味着处于较上部的将更先运行. 文件可以指定多次, 但只会运行一次. <br>
例如:

````json
[
  "postInit/ore_dict.groovy",
  "postInit/"
]
````

这里首先运行 `ore_dict.groovy` , 然后是 `postInit/` 中的所有文件, 但是 `ore_dict.groovy` 已经运行过, 所以不会再次运行. <br>
另一个例子:

````json
[
  "postInit/",
  "postInit/late_stuff.groovy"
]
````

这里首先会运行 `postInit/` 中的所有文件，但因为我们将 `late_stuff.groovy` 特别放在了后面, 所以它暂不会被运行. 而之后, 将只有 `late_stuff.groovy` 会被运行.

### mod包的名称和id

mod包可以是任何你喜欢的名称. 它会在JEI的工具提示里显示. <br>
mod包id则比较重要. 它只能由小写字母和 `_` 组成.

!!! warning
    更改mod包 ID 会导致创建的"自定义物品"在已有世界中删除!

## 重要信息

1. Groovy脚本必须以 `.groovy` 结尾.
2. Groovy脚本必须在 [运行配置](#run-config) 中定义后才能运行.
3. 脚本和文件夹可以使用任何名称.
4. 脚本和 [运行配置](#run-config) 必须在 `[Minecraft 实例路径]/groovy/` 中.
