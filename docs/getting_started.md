# Getting started

Programming knowledge is not necessarily required, but it will help you a lot.<br>
As text editor you can use [Notepad++](https://notepad-plus-plus.org/downloads/) just fine. (We will work on a better alternative in the future)

1. Download Minecraft Forge 1.12.2 and install it
2. Download the latest version of GroovyScript [here](https://www.curseforge.com/minecraft/mc-mods/groovyscript/files) and drop it into the mods folder
3. Also install [MixinBooter](https://www.curseforge.com/minecraft/mc-mods/mixin-booter/files) since GroovyScript depends on it
4. Launch minecraft without adding any files
5. GroovyScript will create several files
    - groovy.log (refer to [Groovy Log](#groovy-log))
    - groovy/runConfig.json (refer to [Groovy Log](#run-config))
    - groovy/postInit/main.groovy (default script file)

## Groovy log
Everything groovy related has its own log, and it generates its own file. If you run into issues with your script you should look here first.
The files directory is always `[Minecraft instance path]/groovy.log`

## Run config
This file defines how each script file should be executed. It can also store some general info about the mod pack. The file will be generated if it doesn't exist. <br>
Let's see what the file can look like.
````json
{
  "packName": "",
  "version": "1.0.0",
  "debug": false,
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
`packName` is the name of the pack. It currently doesn't do anything special. <br>
`version` is the version of the pack. It currently doesn't do anything special. <br>
`debug`: If this is false all messages that logged to debug will not be logged. Great for debugging. <br>
`loaders`: This defines at what stage what files should be loaded. By default, there are two stages: `preInit` and `postInit`. <br>
`preInit` will be ran at an early stage. Do not register recipes here. Use it to register game objects like items and blocks. <br>
`postInit` will run right before JEI loads. Use it to register recipes for example. When GroovyScript gets reloaded only this loader will run.<br>
Inside the square brackets of the loader we define the files or path that will be run. You can NOT run a file in multiple loaders. 
Elements higher in the list will be run first. Files can be put multiple times, but they will only get executed once. <br>
For example:
````json
[
   "postInit/ore_dict.groovy",
   "postInit/"
]
````
Here first `ore_dict.groovy` will be executed and then all files of `postInit/`, but since `ore_dict.groovy` was already executed, it will not run now. <br>
Another example:
````json
[
   "postInit/",
   "postInit/late_stuff.groovy"
]
````
First everything in `postInit/` will be executed, but since `late_stuff.groovy` is specifically put later it will not be executed. After that only `late_stuff.groovy` will be executed.

## Important infos
1. Groovy scripts must end in `.groovy`
2. Groovy scripts must be defined somehow in the [run config](#run-config) to be executed
3. The scripts and folders can have any name
4. All scripts and the [run config](#run-config) must be located in `[Minecraft instance path]/groovy/`