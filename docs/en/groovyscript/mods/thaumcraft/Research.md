# Research

## Thaumometer Scanning

The following methods allow for scanning a specified Object with a Thaumometer to discover the Object's component aspects.

```groovy
mods.thaumcraft.Research.addScannable(Block)
mods.thaumcraft.Research.addScannable(Enchantment)
mods.thaumcraft.Research.addScannable(Material)
mods.thaumcraft.Research.addScannable(Potion)
```

The following methods specify the research key unlocked by scanning a specified Object, with a Thaumometer.

```groovy
mods.thaumcraft.Research.addScannable(String, Block)
mods.thaumcraft.Research.addScannable(String, ItemStack)
mods.thaumcraft.Research.addScannable(String, Material)
```

!!! example

    ```groovy
    mods.thaumcraft.Research.addScannable('UNLOCKAUROMANCY', item('minecraft:pumpkin'))
    ```


## Modifying The Thaumonomicon

### New Category (research tab)

The following builder is for creating new Research Categories (research tab). <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.thaumcraft.Research.researchCategoryBuilder()
```

Adding category name: (required)

```groovy
.key(String)
```

Adding research requirement: (optional (default is ""))

```groovy
.researchKey(String/*(1)!*/)
```

1. The Research Key is the required research to craft the item, research is unlocked via the Thaumonomicon. Obtain a list of all research keys by doing `/tc research list`.

Adding required aspects: (optional)

```groovy
.formulaAspect(AspectStack)/*(1)!*/
```

1. Aspects specified here must be discovered before the category is revealed in the Thaumonomicon. May be called multiple times.

Adding tab icon: (required) <br>
This is a [resource location](../../rl.md).

```groovy
.icon(String)/*(1)!*/
.icon(String mod, String path)/*(2)!*/
```

1. Path to the new tab's icon in the Thaumcraft assets folder.
2. Path to the new tab's icon in the "mod" assets folder.

Adding background: (required) <br>
This is a [resource location](../../rl.md).

```groovy
.background(String)/*(1)!*/
.background(String mod, String path)/*(2)!*/
```

1. Path to the new tab's background in the Thaumcraft assets folder.
2. Path to the new tab's background in the "mod" assets folder.

Adding background overlay: (optional) <br>
This is a [resource location](../../rl.md).

```groovy
.background2(String)/*(1)!*/
.background2(String mod, String path)/*(2)!*/
```

1. Path to the new tab's background overlay in the Thaumcraft assets folder.
2. Path to the new tab's background overlay in the "mod" assets folder.

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

    ```groovy
    mods.thaumcraft.Research.researchCategoryBuilder()
        .key('BASICS2')
        .researchKey('UNLOCKAUROMANCY')
        .formulaAspect(aspect('herba') * 5)
        .formulaAspect(aspect('ordo') * 5)
        .formulaAspect(aspect('perditio') * 5)
        .formulaAspect(aspect('aer') * 5)
        .formulaAspect(aspect('ignis') * 5)
        .formulaAspect(aspect('terra') * 5)
        .formulaAspect(aspect('aqua') * 5)
        .icon('textures/aspects/humor.png')
        .background('textures/gui/gui_research_back_1.jpg')
        .background2('textures/gui/gui_research_back_over.png')
        .register()
    ```

### Remove Category (research tab)

```groovy
mods.thaumcraft.Research.removeCategory(String/*(1)!*/)
```

1. Target tab name.

!!! example

    ```groovy
    mods.thaumcraft.Research.removeCategory('BASICS')
    ```

### New research entries

[WIP]

A research builder has yet to be created, for now this method takes in a json representation of the Thaumonomicon tab's research.

```groovy
mods.thaumcraft.Research.addResearchLocation(String)/*(1)!*/
mods.thaumcraft.Research.addResearchLocation(String mod, String path)/*(2)!*/
```

1. Path to the additional research JSON in the Thaumcraft assets folder.
2. Path to the additional research JSON in the "mod" assets folder.

!!! example

    ```groovy
    mods.thaumcraft.Research.addResearchLocation('thaumcraft', 'research/new.json')
    ```

    ```json
    {
        "entries" :[
            {
                "key": "FIRSTSTEPS",
                "name": "research.FIRSTSTEPS.title",
                "icons": [ "thaumcraft:textures/items/thaumonomicon.png" ],
                "category": "BASICS",
                "location": [ 0,0 ],
                "parents": [ "!gotthaumonomicon" ],
                "siblings": [ "KNOWLEDGETYPES", "!gotdream" ],
                "meta": [ "ROUND","SPIKY" ],
                "stages": [
                    {
                        "text": "research.FIRSTSTEPS.stage.1",
                        "required_craft":["thaumcraft:arcane_workbench"],
                        "recipes": ["thaumcraft:salismundusfake"]
                    },
                    {
                        "text": "research.FIRSTSTEPS.stage.2",
                        "required_craft":["thaumcraft:thaumometer"],
                        "required_knowledge":["OBSERVATION;BASICS;1"],
                        "recipes": ["thaumcraft:thaumometer","thaumcraft:salismundusfake"]
                    },
                    {
                        "text": "research.FIRSTSTEPS.stage.3",
                        "recipes": ["thaumcraft:thaumometer","thaumcraft:salismundusfake","thaumcraft:StoneArcane","thaumcraft:BrickArcane"]
                    }
                ]
            },
            { ... }
        ]
    }
    ```
