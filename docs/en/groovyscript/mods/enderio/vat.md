# EnderIO Vat

## Adding Recipes

Just like other recipe types, the Vat also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.enderio.Vat.recipeBuilder()
```

Adding input: (requires exactly 1)

```groovy
.input(FluidStack)
```

Adding output: (requires exactly 1)

```groovy
.output(FluidStack)
```

Set base multiplier: (optional (default is 1))

```groovy
.baseMultiplier(float)
```

Adding left item input: (optional)

```groovy
.itemInputLeft(ItemStack item, float multiplier)
```

Adding right item input: (optional)

```groovy
.itemInputRight(ItemStack item, float multiplier)
```

Set required machine tier: (optional (default is any))

```groovy
.tierAny() // Default: Allows any tier
.tierNormal()
.tierEnhanced()
```

Set required total energy: (optional (default is 5000))

```groovy
.energy(int)
```

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

    ```groovy
    mods.enderio.Vat.recipeBuilder()
            .input(fluid('water') * 500)
            .output(fluid('lava') * 500)
            .itemInputLeft(item('minecraft:diamond'), 1.5)
            .itemInputRight(item('minecraft:iron_ingot'), 0.7)
            .itemInputRight(item('minecraft:gold_ingot'), 7)
            .baseMultiplier(1)
            .register()
    ```

## Removing Recipes

This removes ALL recipes that match the given output:

```groovy
mods.enderio.Vat.remove(ItemStack output)
```

!!! example

    ```groovy
    // removes Nutrient Distillation recipe from the Vat
    mods.enderio.Vat.remove(fluid('nutrient_distillation'))
    ```
