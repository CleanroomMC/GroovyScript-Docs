# Combination Crafting
!!! Note
    As of GroovyScript 0.4.6, there are no combination recipes by default added by Extended Crafting, so theoretically, none can be removed as you don't have any yet ¯/\_(ツ)_/¯

As of GroovyScript 0.4.6, all Extended Crafting recipes are made using a recipe builder.
No idea what a builder is? Check [this](../../../groovy/builder.md) out.

Package:

```groovy
mods.extendedcrafting.Combination
mods.extendedcrafting.CombinationCrafting
``` 

## Adding recipes
Works only for items and energy

```groovy
mods.extendedcrafting.combination.recipeBuilder(ItemStack output, long cost, Ingredient input, NonNullList<Ingredient> pedestals)

mods.extendedcrafting.combination.recipeBuilder(ItemStack output, long cost, int perTick, Ingredient input, NonNullList<Ingredient> pedestals)
```

### Input

Requires exactly 1 item

```groovy
input(IIngredient)
```

### Power

We can add a power cost to our recipes using the `cost` or `totalCost` arguments for our builder. You can also add a minimum power supply per tick using `perTick` or `costPerTick`
```groovy
cost(long)
totalCost(long)
```
```groovy
perTick(long)
costPerTick(int)
```
!!! Note
    None of these can be negative

### Catalyst

The item that goes on the Crafting Core can be added using `input`
````groovy
input(IIngredient ingredient)
````

### Pedestal items

Items that go on Pedestals can be added using `pedestals`
````groovy
pedestals(IIngredient ingredient)
pedestals(IIngredient... ingredients)
pedestals(Collection<IIngredient> ingredients)
````

### Output

Works only for items

Outputs can be added using `output`
```groovy
output(ItemStack)
```

### Register recipe

```groovy
register()
```

!!! example

    ```groovy
    mods.extendedcrafting.combination.recipeBuilder()
        .cost(100) //Requires 100FE total
        .perTick(100) //Requires 100FE/t to run
        .output(item('minecraft:diamond') * 2) //Outputs two diamonds
        .input(item('minecraft:pumpkin')) //Requires a pumpkin as catalyst
        .pedestals(item('minecraft:pumpkin') * 8) //requires 8 pumpkins on pedestals
        .register() //Registers your recipe. Very important!
    ```

    ```groovy
    mods.extendedcrafting.combinationcrafting.recipeBuilder()
        .cost(10000) //Requires 10,000 FE
        .output(item('minecraft:gold_ingot') * 2) //Gives two gold ingots as output
        .input(item('minecraft:pumpkin')) //Requires a pumpkin as catalyst
        .pedestals(item('minecraft:pumpkin'), item('minecraft:clay'), item('minecraft:clay'), item('minecraft:pumpkin')) //Requires two pumpkinds and two clay blocks on pedestals
        .register() //Registers your recipe. Very important!
    ```

## Removing Recipes

!!! Note
    No Combination Crafting recipes are registed by default.

This removes ALL recipes that match the given input:

```groovy
mods.bloodmagic.CombinationCrafting.removeByInput(IIngredient)
```

This removes ALL recipes that match the given output:

```groovy
mods.bloodmagic.CombinationCrafting.removeByOutput(ItemStack)
```

Removes all registed Combination Crafting recipes:

```groovy
mods.bloodmagic.CombinationCrafting.removeAll()
```

!!! example

    ```groovy
    // Note: No recipes are registered to Combination Crafting by default.

    //Removes all recipes using pumpkins as inputs
    mods.extendedcrafting.CombinationCrafting.removeByInput(item('minecraft:pumpkin'))

    //Removes all recipes that output gold ingots
    mods.extendedcrafting.CombinationCrafting.removeByOutput(item('minecraft:gold_ingot'))
    ```