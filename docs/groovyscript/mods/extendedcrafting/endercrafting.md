# Ender Crafting
As of GroovyScript 0.4.6, all Extended Crafting recipes are made using a recipe builder.

No idea what a builder is? Check [this](../../../groovy/builder.md) out.

## Adding recipes directly
Adding recipes directly works in almost the same way as adding vanilla recipes, except the `time` can also be added to specify how long the craft takes 
### Add shaped
```groovy
mods.extendedcrafting.endercrafting.addShaped(ItemStack output, List<List<IIngredient>> input)
mods.extendedcrafting.endercrafting.addShaped(int time, ItemStack output, List<List<IIngredient>> input)
```
!!! Note
1. Time is specified in seconds here instead of ticks.
2. If a time taken to craft is not specified, it will default to whatever is set in Extended Crafting's config (default is 60 seconds)
#### Example
```groovy
mods.extendedcrafting.endercrafting.addShaped(item('minecraft:clay_ball') * 3, /*Outputs 3 clay balls*/ [ 
        [item('minecraft:nether_star'), null, item('minecraft:nether_star')],
        [null, ore('ingotIron'), null],
        [item('minecraft:nether_star'), null, item('minecraft:nether_star')] //Recipe
])

mods.extendedcrafting.endercrafting.addShaped(60, /*Takes 60 seconds*/ item('minecraft:clay_ball') * 2, /*Outputs 2 clay balls*/ [
        [item('minecraft:nether_star'), null],
        [null, ore('ingotIron')] //Recipe
])
```
### Add shapeless
```groovy
mods.extendedcrafting.endercrafting.addShapeless(ItemStack output, List<List<IIngredient>> input)
mods.extendedcrafting.endercrafting.addShapeless(int time, ItemStack output, List<IIngredient> input)
```

#### Example
```groovy
mods.extendedcrafting.endercrafting.addShapeless(item('minecraft:clay_ball') * 32, /*Outputs 32 clay balls*/ [item('minecraft:dirt'), item('minecraft:dirt'), item('minecraft:leather')]) //Recipe

mods.extendedcrafting.endercrafting.addShapeless(60, /*Takes 60 seconds*/ item('minecraft:clay_ball') * 32, /*Outputs 32 clay balls*/ [item('minecraft:dirt'), item('minecraft:dirt'), item('minecraft:leather')]) //Recipe
```

## Adding recipes using a builder
### Add shaped
```groovy
mods.extendedcrafting.endercrafting.shapedBuilder()
```
#### Inputs
```groovy
matrix(input(List<IIngredient))
matrix(input(List<List<IIngredient>>))
```
`matrix` can be replaced with `shape` as well
#### Outputs
```groovy
output(ItemStack)
```
#### Time taken to craft
```groovy
time(int)
```
!!! Note
1. Time is specified in seconds here instead of ticks.
2. If a time taken to craft is not specified, it will default to whatever is set in Extended Crafting's config (default is 60 seconds)
#### Example
```groovy
mods.extendedcrafting.endercrafting.shapedBuilder()
        .output(item('minecraft:stone')) //Outputs one stone block
        .matrix('BXX',
                'X B') //Recipe
        .key('B', item('minecraft:stone')) //Sets B key to stone
        .key('X', item('minecraft:gold_ingot')) //Sets X key to gold ingot
        .time(1) //Takes one second
        .mirrored() //Enables you to craft the recipe when mirrored as well
        .register()
```
```groovy
mods.extendedcrafting.endercrafting.shapedBuilder()
        .output(item('minecraft:diamond') * 32) //Outputs 32 diamonds
        .matrix([[item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')],
                [item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')],
                [item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot')]]) //Recipe
        .time(1) //Takes one second to craft
        .register()
```