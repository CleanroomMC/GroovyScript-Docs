# EnderIO Alloy Smelter

## Adding Recipes

Just like other recipe types, the Alloy Smelter also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.enderio.AlloySmelter.recipeBuilder()
```

Adding inputs: (requires 1-3)

```groovy
.input(IIngredient)
.input(IIngredient...)
.input(Collection<IIngredient>)
```

Adding output: (requires exactly 1)

```groovy
.output(ItemStack)
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

Set xp chance: (optional (default is 0))

```groovy
.xp(float) // 0.0 = 0% / 1.0 = 100%
```

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

    ```groovy
    mods.enderio.AlloySmelter.recipeBuilder()
            .input(item('minecraft:iron_ingot'), ore('ingotGold'), item('minecraft:clay_ball') * 64)
            .output(item('minecraft:nether_star'))
            .tierNormal()       // recipes requires normal or enhanced tier
            .energy(6000)
            .xpChance(0.5f)
            .register()
    ```

## Removing Recipes

This removes ALL recipes that match the given output:

```groovy
mods.enderio.AlloySmelter.remove(ItemStack output)
```

!!! example

    ```groovy
    // removes Vibrant Alloy from Alloy Smelter
    mods.enderio.AlloySmelter.remove(item('enderio:item_alloy_ingot:2'))
    ```
