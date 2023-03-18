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

Let's go through it bit by bit: <br>

- `packName` is the name of the pack (See [pack name and id](#pack-name-and-id)). Important
  for [content](groovyscript/content/content.md). <br>
- `packId` (0.4.0+) is the id of the pack (See [pack name and id](#pack-name-and-id)). Important
  for [content](groovyscript/content/content.md). <br>
- `version` is the version of the pack. It currently doesn't do anything special. <br>
- `debug`: If this is false all messages that logged to debug will not be logged. Great for debugging. <br>
- `classes`: (0.3.0+) Files that contain a single class should be specified here. It makes sure classes are loaded when
  scripts try to access them. <br>
- `loaders`: This defines at what stage what files should be loaded. By default, there are two stages: `preInit`
  and `postInit`. <br>
- `preInit` will run at an early stage. Do not register recipes here. Use it to register game objects like items and
  blocks. <br>
- `postInit` will run right before JEI loads. Use it to register recipes for example. When GroovyScript gets reloaded
  only this loader will run.<br>
  Inside the square brackets of the loader we define the files or path that will be run. You can NOT run a file in
  multiple loaders.
  Elements higher in the list will be run first. Files can be put multiple times, but they will only get executed
  once. <br>
  For example:

````json
[
  "postInit/ore_dict.groovy",
  "postInit/"
]
````

Here first `ore_dict.groovy` will be executed and then all files of `postInit/`, but since `ore_dict.groovy` was already
executed, it will not run now. <br>
Another example:

````json
[
  "postInit/",
  "postInit/late_stuff.groovy"
]
````

First everything in `postInit/` will be executed, but since `late_stuff.groovy` is specifically put later it will not be
executed. After that only `late_stuff.groovy` will be executed.

### Pack name and id

The pack name can be anything. It's the name that will show up in JEI in tooltips on items you created. <br>
The pack id is very important. It must only consist of lower case letters and `_`.

!!! warning
    Changing the pack id will result in created items being lost in existing worlds!

## Important infos

1. Groovy scripts must end in `.groovy`
2. Groovy scripts must be defined somehow in the [run config](#run-config) to be executed
3. The scripts and folders can have any name
4. All scripts and the [run config](#run-config) must be located in `[Minecraft instance path]/groovy/`
