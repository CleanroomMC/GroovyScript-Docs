# Blood Magic Alchemy Table

Package:

```groovy
mods.bloodmagic.AlchemyTable
```

!!! Note
    The Alchemy Table requires a Blood Orb linked to a player inside it to function.
    It consumes Life Essence from the bound player's Life Network to craft.
    !!! Danger ""
        Tier 6 must be enabled in the config to use a Blood Orb of that tier.

## Adding Recipes

Just like other recipe types, the Alchemy Table also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.bloodmagic.AlchemyTable.recipeBuilder()
```

Adding inputs: (requires 1-6)

```groovy
.input(IIngredient)
.input(IIngredient...)
.input(Collection<IIngredient>)
```

Setting cost in Life Essence taken from the owner of the orb: (optional (default is 0))

```groovy
.syphon(int)
.drain(int)
```

Setting the time in ticks the recipe takes: (required)

```groovy
.ticks(int)
.time(int)
```

Setting the minimum tier of Blood Orb: (required)

```groovy
.minimumTier(int)
.tier(int)
```

Adding output: (requires exactly 1)

```groovy
.output(ItemStack)
```

Register recipe: (returns `WayofTime.bloodmagic.api.impl.recipe.RecipeAlchemyTable`)

```groovy
.register()
```

!!! example

    ```groovy
    mods.bloodmagic.AlchemyTable.recipeBuilder()
            .input(item("minecraft:diamond"), item("minecraft:diamond"))
            .output(item("minecraft:clay"))
            .ticks(100)
            .minimumTier(2)
            .syphon(500)
            .register()

    mods.bloodmagic.AlchemyTable.recipeBuilder()
            .input(item("minecraft:diamond"), item("minecraft:diamond"), item("minecraft:gold_ingot"),
                    item("minecraft:gold_ingot"), item("bloodmagic:slate"), item("bloodmagic:slate"))
            .output(item("minecraft:clay"))
            .time(2000)
            .tier(5)
            .drain(25000)
            .register()
    ```

## Removing Recipes

This removes ALL recipes which have all input ingredients[^1]:

```groovy
mods.bloodmagic.AlchemyTable.removeByInput(NonNullList<IIngredient>)
mods.bloodmagic.AlchemyTable.removeByInput(IIngredient...)
```

This removes ALL recipes that match the given output:

```groovy
mods.bloodmagic.AlchemyTable.removeByOutput(ItemStack)
```

Removes all registed Alchemy Table recipes:

```groovy
mods.bloodmagic.AlchemyTable.removeAll()
```

!!! example

    ```groovy
    // Removes all recipes that have inputs including both Nether Wart and Gunpowder. (1)
    mods.bloodmagic.AlchemyTable.removeByInput(item("minecraft:nether_wart"), item("minecraft:gunpowder"))
    // Removes all recipes that output Sand.
    mods.bloodmagic.AlchemyTable.removeByOutput(item("minecraft:sand"))
    ```

    1. This would remove the recipes for both Simple Power Catalyst and Simple Lengthening Catalysts.

[^1]: Note that a recipe with inputs "ABCD" would match with a target containing only "AB".
