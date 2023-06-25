# Blood Magic Blood Altar

Package:

```groovy
mods.bloodmagic.BloodAltar
```

!!! Note
    The Blood Altar consumes Life Essence from its internal tank to convert the input item into the output item.
    Each tier requires a larger multiblock, which may contain Runes that modify the Blood Altar's functionality.
    !!! Danger ""
        Tier 6 must be enabled in the config to use a Blood Altar of that tier.

## Adding Recipes

Just like other recipe types, the Blood Altar also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.bloodmagic.BloodAltar.recipeBuilder()
```

Adding inputs: (requires exactly 1)

```groovy
.input(IIngredient)
.input(IIngredient...)
.input(Collection<IIngredient>)
```

Setting the minimum tier required: (optional (default is 0))

```groovy
.minimumTier(int)
.tier(int)
```

Setting the required amount of Life Essence: (optional (default is 0))

```groovy
.syphon(int)
```

Setting the base rate the craft consumes Life Essence from the Blood Altar: (optional (default is 0))

```groovy
.consumeRate(int)
```

Setting the base rate the craft loses progress when the Blood Altar does not have enough Life Essence: (optional (default is 0))

```groovy
.drainRate(int)
```

Adding output: (requires exactly 1)

```groovy
.output(ItemStack)
```

Register recipe: (returns `WayofTime.bloodmagic.api.impl.recipe.RecipeBloodAltar`)

```groovy
.register()
```

!!! example

    ```groovy
    mods.bloodmagic.BloodAltar.recipeBuilder()
            .input(item("minecraft:clay"))
            .output(item("minecraft:gold_ingot"))
            .tier(0)
            .drainRate(5)
            .syphon(10)
            .consumeRate(5)
            .register()

    mods.bloodmagic.BloodAltar.recipeBuilder()
            .input(item("minecraft:gold_ingot"))
            .output(item("minecraft:diamond"))
            .minimumTier(3)
            .drainRate(100)
            .syphon(50000)
            .consumeRate(500)
            .register()
    ```

## Removing Recipes

This removes ALL recipes that match the given input:

```groovy
mods.bloodmagic.BloodAltar.removeByInput(IIngredient)
```

This removes ALL recipes that match the given output:

```groovy
mods.bloodmagic.BloodAltar.removeByOutput(ItemStack)
```

Removes all registed Blood Altar recipes:

```groovy
mods.bloodmagic.BloodAltar.removeAll()
```

!!! example

    ```groovy
    // Removes all recipes that have have Ender Pearl as their input. (1)
    mods.bloodmagic.BloodAltar.removeByInput(item("minecraft:ender_pearl"))
    // Removes all recipes that output Ethereal Slates.
    mods.bloodmagic.BloodAltar.removeByOutput(item("bloodmagic:slate:4"))
    ```

    1. This would remove the recipe for the Teleposition Focus.
