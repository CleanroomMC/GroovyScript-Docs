# EnderIO SAG Mill

## Adding Recipes

Just like other recipe types, the SAG Mill also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.enderio.SagMill.recipeBuilder()
```

Adding inputs: (requires exactly 1)

```groovy
.input(IIngredient)
```

Adding output: (requires 1 - 4)

```groovy
.output(ItemStack)
.output(ItemStack...)
.output(Collection<ItemStack>)
```

Adding output with chance: (counts as output)

```groovy
.output(ItemStack itemStack, float chance)
```

Set required machine tier: (optional)

```groovy
.tierAny() // Default: Allows any tier
.tierSimple()
.tierNormal()
.tierEnhanced()
```

Set required total energy: (optional (default is 5000))

```groovy
.energy(int)
```

Set recipe bonus type: (unknown behaviour) TODO

```groovy
.bonusTypeNone() // Default
.bonusTypeMultiply()
.bonusTypeChance()
```

Register recipe: (returns a `crazypants.enderio.base.recipe.Recipe` instance if successful)

```groovy
.register()
```

!!! example

    ```groovy
    mods.enderio.SagMill.recipeBuilder()
            .input(item('minecraft:nether_star'))
            .output(item('minecraft:diamond'))              // guaranteed diamond
            .output(item('minecraft:nether_star'), 0.05f)   // 5% chance to get nether star back
            .tierNormal()       // recipes requires normal or enhanced tier
            .energy(6000)
            .register()
    ```

## Removing Recipes

This removes a recipe that match the given input:

```groovy
mods.enderio.SagMill.removeByInput(ItemStack input)
```

!!! example

    ```groovy
    // removes wheat milling in Sag Mill
    mods.enderio.SagMill.removeByInput(item('minecraft:wheat'))
    ```
