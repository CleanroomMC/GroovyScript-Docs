# Ender Crafting

As of GroovyScript 0.4.6, all Extended Crafting recipes are made using a recipe builder.
No idea what a builder is? Check [this](../../../groovy/builder.md) out.

Package:

```groovy
mods.extendedcrafting.EnderCrafting
```

## Adding recipes directly

Adding recipes directly works in almost the same way as adding vanilla recipes, except the `time` can also be added to specify how long the craft takes 

### Add shaped

```groovy
mods.extendedcrafting.endercrafting.addShaped(ItemStack output, List<List<IIngredient>> input)
mods.extendedcrafting.endercrafting.addShaped(int time, ItemStack output, List<List<IIngredient>> input)
```

!!! example
        ```groovy
        //Uses four nether stars and one iron ingot to give 3 clay balls
        mods.extendedcrafting.endercrafting.addShaped(item('minecraft:clay_ball') * 3, [ 
                [item('minecraft:nether_star'), null, item('minecraft:nether_star')],
                [null, ore('ingotIron'), null],
                [item('minecraft:nether_star'), null, item('minecraft:nether_star')]
        ])

        //Uses one nether star and one iron ingot to give 2 clay balls, takes 60 seconds
        mods.extendedcrafting.endercrafting.addShaped(60, item('minecraft:clay_ball') * 2, [
        [item('minecraft:nether_star'), null],
        [null, ore('ingotIron')]
        ])
        ```

!!! Note
        Time is specified in seconds here instead of ticks.
        
        If a time taken to craft is not specified, it will default to whatever is set in Extended Crafting's config (default is 60 seconds)

### Add shapeless

```groovy
mods.extendedcrafting.endercrafting.addShapeless(ItemStack output, List<List<IIngredient>> input)
mods.extendedcrafting.endercrafting.addShapeless(int time, ItemStack output, List<IIngredient> input)
```

!!! example
        ```groovy
        //Uses two dirt and a piece of leather to give 32 clay balls
        mods.extendedcrafting.endercrafting.addShapeless(item('minecraft:clay_ball') * 32, [item('minecraft:dirt'), item('minecraft:dirt'), item('minecraft:leather')])

        //Uses two dirt and a piece of leather to give 32 clay balls, takes 60 seconds to craft
        mods.extendedcrafting.endercrafting.addShapeless(60, item('minecraft:clay_ball') * 32, [item('minecraft:dirt'), item('minecraft:dirt'), item('minecraft:leather')])
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

### Mirror recipe

Allows you to craft the recipe when mirrored, similar to how iron axes can be crafted with a mirrored recipe in Vanilla
```groovy
mirrored()
```

### Register recipe

```groovy
register()
```

!!! example
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

!!! Note
        Time is specified in seconds here instead of ticks.
        
        If a time taken to craft is not specified, it will default to whatever is set in Extended Crafting's config (default is 60 seconds)

## Removing recipes

Removes all recipes having the item as an output
```groovy
mods.extendedcrafting.endercrafting.removeByOutput(ItemStack stack) 
```

Removes a recipe with that specific ID
```groovy
mods.extendedcrafting.endercrafting.remove(IRecipe recipe)
```

Removes all ender crafting recipes
```groovy
mods.extendedcrafting.endercrafting.removeAll()
```

!!! example

        ```groovy
        //Removes all recipes that gives the Ender Star from Extended Crafting as an output
        mods.extendedcrafting.endercrafting.removeByOutput(item('extendedcrafting:material:40'))
        ```