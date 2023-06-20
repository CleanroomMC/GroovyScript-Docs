# Compression Crafting

As of GroovyScript 0.4.6, all Extended Crafting recipes are made using a recipe builder.
No idea what a builder is? Check [this](../../../groovy/builder.md) out.

Package:

```groovy
mods.extendedcrafting.Compression
mods.extendedcrafting.CompressionCrafting
``` 

## Adding recipes

Works only for items and energy

```groovy
mods.extendedcrafting.combination.recipeBuilder(ItemStack output, IIngredient input, int inputCount, IIngredient catalyst, boolean consumeCatalyst, int powerCost)

mods.extendedcrafting.compression.recipeBuilder(ItemStack output, IIngredient input, int inputCount, IIngredient catalyst, boolean consumeCatalyst, int powerCost, int powerRate)
```

### Outputs

Works only for items

Outputs can be added using `output`
```groovy
output(ItemStack)
```

### Inputs

The item to be compressed can be set using `input`
```groovy
input(IIngredient input)
```
The amount of said item to be compressed can be set using `inputCount`
```groovy
inputCount(int)
```

### Catalyst

The catalyst to be used can be set using `catalyst`. 
```groovy
catalyst(IIngredient)
```
!!! Note
    If a catalyst is not provided, it will automatically default to the Ultimate Catalyst from Extended Crafting

    You can also specify whether to consume the catalyst on crafting using `consumeCatalyst`
```groovy
consumeCatalyst(boolean)
```
!!! Note
    `catalyst` cannot be empty

### Power

We can add a power cost to our recipes using `powerCost` for our builder. You can also add a minimum power supply per tick using `powerRate`
```groovy
powerCost(int)
```
```groovy
powerRate(int)
```

!!! Note
    `powerCost` and `powerRate` cannot be negative

### Register recipe

```groovy
register()
```

!!! example

    ```groovy
    mods.extendedcrafting.compression.recipeBuilder()
        .input(item('minecraft:clay') * 10) //Requires 10 clay as input
        .output(item('minecraft:diamond') * 2) //Outputs two diamonds
        .powerCost(1000) //Requires 1,000 FE total to run
        .register() //Registers your recipe. Very important!
    ```

    ```groovy
    mods.extendedcrafting.compressioncrafting.recipeBuilder()
        .input(item('minecraft:clay')) //Requires clay blocks
        .inputCount(100) //Requires 100 clay blocks
        .output(item('minecraft:gold_ingot') * 7) //Outputs 7 gold ingots
        .catalyst(item('minecraft:diamond')) // Uses a diamond as catalyst
        .consumeCatalyst(true) //Consumes the catalyst (diamond)
        .powerCost(10000)//Requires 10,000 FE total to run
        .powerRate(1000) //Requires 1,000 FE/t to run
        .register() //Registers your recipe. Very important!
    ```

## Removing recipes

This removes recipes by inputs:

```groovy
removeByInput(IIngredient input)
removeByInput(Itemstack input)
```

This removes recipes by catalysts

```groovy
removeByCatalyst(IIngredient catalyst)
```

This removes recipe by recipe ID

```groovy
remove(CompressionRecipe recipe)
```

This removes every compression recipe added by Extended Crafting
```groovy
removeAll()
```