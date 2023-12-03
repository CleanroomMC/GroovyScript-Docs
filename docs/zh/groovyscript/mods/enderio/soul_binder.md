# EnderIO Soul Binder

## Adding Recipes

Just like other recipe types, the Soul Binder also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.enderio.SoulBinder.recipeBuilder()
```

Adding inputs: (requires exactly 1)

```groovy
.input(IIngredient)
```

Adding output: (requires exactly 1)

```groovy
.output(ItemStack)
```

Adding soul vial inputs:<br>
Adds entity souls in form of soul vials to the input

```groovy
.entitySoul(String entityName)
.entitySoul(String... entityNames)
.entitySoul(Collection<String> entityNames)
```

Set input xp levels: (optional (default is 2))

```groovy
.xp(int)
```

Set required total energy: (optional (default is 5000))

```groovy
.energy(int)
```

Register recipe: (returns a `crazypants.enderio.base.recipe.Recipe` instance if successful)

```groovy
.register()
```

!!! example

    ```groovy
    mods.enderio.SoulBinder.recipeBuilder()
            .input(item('minecraft:diamond'))
            .entitySoul('minecraft:zombie')      // zombie in a soul vial
            .output(item('minecraft:nether_star'))
            .xp(10)                              // requires 10 xp levels
            .energy(6000)
            .register()
    ```

## Removing Recipes

This removes a recipe that match the given input:

```groovy
mods.enderio.SoulBinder.remove(ItemStack output)
```

!!! example

    ```groovy
    // removes soul binding for enticing crystal
    mods.enderio.SoulBinder.remove(item('enderio:item_material:17'))
    ```
