# Research

### Thaumometer Scanning

The following methods allow for scanning a specified Object with a thaumometer to discover the Object's component aspects.

```groovy
mods.thaumcraft.Research.addScannable(Block)
mods.thaumcraft.Research.addScannable(Enchantment)
mods.thaumcraft.Research.addScannable(Material)
mods.thaumcraft.Research.addScannable(Potion)
```

The following methods specify the research key unlocked by scanning a specified Object, with a thaumometer.

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

[WIP]

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
.researchKey(String)  // (1)
```

1. Please see the examples below to better understand how this works

Adding required aspects: (optional)

```groovy
.formulaAspect(AspectStack) // (1)
```

1. Aspects specified here must be discovered before the category is revealed in the thaumonomicon

Adding tab icon: (required)

```groovy
.icon(String) // (1)
.icon(String mod, String path) // (2)
```

1. Both methods are for specifying the path to the new tab's icon
2. Please see the examples below to better understand how this works

Adding background: (required)

```groovy
.background(String) // (1)
.background(String mod, String path) // (2)
```

1. Both methods are for specifying the path to the new tab's background
2. Please see the examples below to better understand how this works

Adding background overlay: (optional)

```groovy
.background2(String) // (1)
.background2(String mod, String path) // (2)
```

1. Both methods are for specifying the path to the new tab's background overlay
2. Please see the examples below to better understand how this works

Register recipe: (returns nothing)

```groovy
.register()
```

### Example

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
mods.thaumcraft.Research.removeCategory(String) // target tab name
```

!!! example
    ```groovy
    mods.thaumcraft.Research.removeCategory('BASICS')
    ```

### New research entries

A research builder has yet to be created, for now this method takes in a json representation of the thaumonomicon tab's research.

```groovy
mods.thaumcraft.Research.addResearchLocation(String) // (1)
mods.thaumcraft.Research.addResearchLocation(String mod, String path) // (2)
```

1. Both methods are for specifying the path to additional json research
2. Please see the examples below to better understand how this works

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
                "category": "BASICS", "location": [ 0,0 ], 
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
