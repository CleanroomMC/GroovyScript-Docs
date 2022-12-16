# Research

### Add thaumometer trigger to item

The following code specifies the research key unlocked by scanning the specified item with a thaumometer.

```groovy
mods.thaumcraft.Research.addScannable('<research key>', item('minecraft:pumpkin'))
```

## Modifying the thaumonomicon

### New category (research tab)

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
    .icon(new ResourceLocation('thaumcraft', 'textures/aspects/humor.png'))
    .background(new ResourceLocation('thaumcraft', 'textures/gui/gui_research_back_1.jpg'))
    .background2(new ResourceLocation('thaumcraft', 'textures/gui/gui_research_back_over.png'))
    .register()
```

Note: Requires ``import net.minecraft.util.ResourceLocation``. key refers the name of the new tab. researchKey is the research that gates the tab from showing in the thaumonomicon. formulaAspect is optional, it is the aspect(s) and quanity(ies) which must be scanned for the category to appear in the thaumonomicon.

### Remove category (research tab)

```groovy
mods.thaumcraft.Research.removeCategory('<tab name>');
```

### New research entries

A research builder has yet to be created, for now this method takes in a json representation of the thaumonomicon tab's research.

```groovy
mods.thaumcraft.Research.addResearchLocation(new ResourceLocation('thaumcraft', 'research/new.json'))
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
