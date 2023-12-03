# EnderIO Enchanter

GroovyScript allows you to add and remove recipes for enchantments in the enchanter with custom book and lapis items.
EnderIO automatically calculates costs and adds recipes for each level of the enchantment.

## Adding Recipes

Just like other recipe types, the Enchanter also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.enderio.Enchanter.recipeBuilder()
```

Set input: (required)

```groovy
.input(IIngredient)
```

Set enchantment: (required)

```groovy
.enchantment(Enchantment)
```

Set input amount per level: (optional (default is amount of input ingredient))

```groovy
.amountPerLevel(int)
```

Set xp multiplier: (optional (default is 1))

```groovy
.xpCostMulitplier(double)
```

Set custom book item: (optional (default is Book and Quill))

```groovy
.customBook(IIngredient)
```

Set custom lapis item: (optional (default is Lapis Lazuli))

```groovy
.customLapis(IIngredient)
```

Register recipe: (returns a `crazypants.enderio.base.recipe.enchanter.EnchanterRecipe` instance if successful)

```groovy
.register()
```

!!! example

    ```groovy
    mods.enderio.Enchanter.recipeBuilder()
            .enchantment(enchantment('efficiency'))
            .input(item('minecraft:nether_star') * 2)
            .xpCostMultiplier(3f)
            .customBook(item('enderio:item_dark_steel_upgrade:0'))
            .customLapis(item('minecraft:poisonous_potato'))
            .register()
    ```

## Removing Recipes

This removes a recipe that match the given input:

```groovy
mods.enderio.Enchantment.remove(Enchantment)
```

!!! example

    ```groovy
    // removes all efficiency enchantment recipes
    mods.enderio.Enchantment.remove(enchantment('efficiency'))
    ```
