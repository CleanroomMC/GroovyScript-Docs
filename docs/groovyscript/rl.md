# Resource Location for Dummies

Minecraft's resource location is often used as an identifier for items but also for locations of asset files like models
and textures. It consists of two strings: a domain and a path. The domain is usually a mod id. The path is a name
(for items) or a path (for files). A Resource Location can be represented like this: `domain:path`.
A Resource Location can not contain any characters. Upper case letters are not allowed. Numbers are allowed. Underscore
is allowed.

## Creating a Resource Location
There are two ways to do that:

1. Using the `net.minecraft.util.ResourceLocation` constructor (this class is auto imported since version 0.4.0)
    - `new ResourceLocation("domain:path")`
    - `new ResourceLocation("domain", "path")`
    - `new ResourceLocation("path")` (defaults to `minecraft` domain)
2. Using the `resource()` game object handler (acts like a global method)
    - `resource("domain:path")`
    - `resource("domain", "path")`
    - `resource("path")` (defaults to the pack id specified in the run config (see [here](../getting_started.md#run-config)))

We can see that both methods are mostly the same except that the game object handler defaults to the pack id instead of
minecraft. This way is the preferred way.

???+ Example
    ```groovy
    // the following 2 lines are equal
    def rl1 = resource("groovyscript", "path/to/file") // groovyscript:path/to/file
    def rl2 = resource("groovyscript:path/to/file") // groovyscript:path/to/file
    // the domain defaults to the pack id if not specified
    def rl3 = resource("furnace") // packid:furnace
    ```

In GroovyScript there usually exist overrides where you can directly insert mod id and path without
creating a `ResourceLocation`. <br>

## Converting to file path

In the following `.../.minecraft/` is the instance folder. <br>
`.minecraft/resources/` is the root resource folder (requires Resource Loader mod). Resources can be in any valid path
as long as minecraft knows about it.
Since version 0.4.0 the root folder may also be `.minecraft/groovy/assets/`. Resource packs are also a valid way to load
resources.<br>
The whole path is composed of

- the root path
- the domain (mod id)
- the path (of the resource location)

Formatted: `rootPath/domain/path`

## Examples

We use `.minecraft/resources` as the root here.

| Resource Location                        | refers to File path                                           |
|------------------------------------------|---------------------------------------------------------------|
| `minecraft:textures/gui/button.png`      | `.minecraft/resources/minecraft/textures/gui/button.png`      |
| `textures/gui/button.png`                | `.minecraft/resources/minecraft/textures/gui/button.png`      |
| `thaumcraft:research/SOME_RESEARCH.json` | `.minecraft/resources/thaumcraft/research/SOME_RESEARCH.json` |

## Model files

In model or blockstate json files you may also find resource locations. Lets
take `assets/minecraft/models/block/andesite.json` for example (`assets` being the root folder). In there you will find

```json
{
  "parent": "block/cube_all",
  "textures": {
    "all": "blocks/stone_andesite"
  }
}
```

Here `"block/cube_all"` and `"blocks/stone_andesite"` are both resource locations. So you might think the texture is
located in `assets/minecraft/blocks/stone_andesite`, but that is not the case.
The real path is `assets/minecraft/textures/blocks/stone_andesite.png`. The reason for that is that
minecraft knows it should point to a texture and prepends `textures/` and appends `.png` to the path.
It's similar for `"parent": "block/cube_all"` except it points to another model.

## Other uses

Resource locations are also used as identifiers for game registry entries for example items. <br>
When you use the item bracket handler you do something like `item('minecraft:iron_ingot')`. Yes `'minecraft:iron_ingot'` is a resource location, except it doesn't point to a resource.
For game objects like items the resource location is also referred to as the registry name.

!!! Note
    Note that you can't use `item('iron_ingot')`. This is disabled by GroovyScript. You must always input the full registry name.
