# Resource Location for Dummies

Minecraft's resource location consists of two strings which usually marks the location of a file. For example model json
files. <br>
The minecraft class's name is `net.minecraft.util.ResourceLocation`. It is auto imported to any groovy script (version
0.4.0+).
Let's look at how it works. <br>
As mentioned before it consists of two strings, a domain and a path. The domain is usually a mod id. If the domain is
not specified it defaults to `minecraft`.
A resource location can be written as:

- `new ResourceLocation("modid:path")`
- `new ResourceLocation("modid", "path")`

Both are equal. In GroovyScript there usually exist overrides where you can directly insert mod id and path without
creating a `ResourceLocation`. <br>
To clarify: `new ResourceLocation("thaumcraft", "research/SOME_RESEARCH.json")` is the same
as `new ResourceLocation("thaumcraft:research/SOME_RESEARCH.json")`.
In the following examples we would write `thaumcraft:research/SOME_RESEARCH.json` to keep it short.

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
