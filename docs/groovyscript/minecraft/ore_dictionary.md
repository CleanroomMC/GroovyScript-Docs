# Ore Dictionary
!!! Note
    Requires version 0.3.0+
 GroovyScript also allows you to remove and add ore dictionaries to items and reload them.
 
## Adding ore dicts

All three methods are do exactly the same thing.
```groovy
oreDict.add("amogus", item('minecraft:iron_ingot'))

item('minecraft:iron_ingot').addOreDict(ore('amogus'))

ore('amogus').add(item('minecraft:iron_ingot'))
```

## Removing ore dicts

All three methods are do exactly the same thing.
````groovy
oreDict.remove("ingotIron", item('minecraft:iron_ingot'))

item('minecraft:iron_ingot').removeOreDict(ore('ingotIron'))

ore('ingotIron').remove(item('minecraft:iron_ingot'))
````

## Other
You can get all items from an ore dict.
Both ways do the same thing.
````groovy
oreDict.getItems('ingotIron')
oreDict['ingotIron']
````

Checking if an item is in an ore dictionary
````groovy
item('minecraft:iron_ingot') in ore('ingotIron') // returns true
````

