# Erste Schritte

Programmierkenntnisse sind nicht unbedingt erforderlich, aber sie werden Ihnen sehr helfen.<br>
Als Texteditor können Sie [Notepad++] (https://notepad-plus-plus.org/downloads/) gut verwenden. (Wir werden an einer besseren
Alternative in der Zukunft arbeiten)


1. Minecraft Forge 1.12.2 herunterladen und installieren
2. Laden Sie die neueste Version von GroovyScript [hier](https://www.curseforge.com/minecraft/mc-mods/groovyscript/files)
   und legen Sie es in den Mods-Ordner
3. Installieren Sie auch [MixinBooter] (https://www.curseforge.com/minecraft/mc-mods/mixin-booter/files), da GroovyScript
   davon abhängt
4. Minecraft starten, ohne Dateien hinzuzufügen
5. GroovyScript erstellt mehrere Dateien
    - groovy.log (siehe [Groovy Log](#groovy-log))
    - groovy/runConfig.json (siehe [Groovy Log](#run-config))
    - groovy/postInit/main.groovy (Standard-Skriptdatei)

## Groovy log

Für alles, was mit Groovy zu tun hat, gibt es ein eigenes Protokoll, und es wird eine eigene Datei erzeugt. Wenn Sie auf Probleme mit Ihrem Skript stoßen, sollten Sie
solltest du zuerst hier nachsehen.
Das Dateiverzeichnis ist immer `[Minecraft-Instanzpfad]/groovy.log`.

## Konfiguration ausführen

This file defines how each script file should be executed. It can also store some general info about the mod pack. The
file will be generated if it doesn't exist.
If you don't understand what this is or how it works you can skip this. All you need to know is that you put your
scripts with recipes in `groovy/postInit`.
Scripts with stuff like Item Creation go in `groovy/preInit`.<br>
Let's see what the file can look like.

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

Zuerst wird alles in `postInit/` ausgeführt, aber da `late_stuff.groovy` speziell später eingefügt wird, wird es nicht
ausgeführt. Danach wird nur noch `late_stuff.groovy` ausgeführt.

### Name und Kennung des Pakets

Der Name des Pakets kann beliebig sein. Es ist der Name, der in JEI in den Tooltips der von Ihnen erstellten Gegenstände angezeigt wird.<br>
Die Pack-ID ist sehr wichtig. Sie darf nur aus Kleinbuchstaben bestehen und `_`.

!!! Warnung
    Das Ändern der Pack-ID führt dazu, dass erstellte Gegenstände in bestehenden Welten verloren gehen!

## Wichtige Informationen

1. Groovy-Skripte müssen mit `.groovy` enden.
2. Groovy-Skripte müssen irgendwie in der [run-config](#run-config) definiert sein, um ausgeführt zu werden
3. Die Skripte und Verzeichnisse können beliebige Namen haben
4. Alle Skripte und die [run-config](#run-config) müssen sich in `[Minecraft-Instanzpfad]/groovy/` befinden
