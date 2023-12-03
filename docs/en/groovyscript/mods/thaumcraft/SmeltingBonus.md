# Smelting Bonus

Add or remove bonus outputs from the Infernal Furnace.

## Adding Bonus

The following builder is for creating new Smelting Bonuses. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.thaumcraft.SmeltingBonus.recipeBuilder()
```

Adding input: (requires exactly 1)

```groovy
.input(IIngredient/*(1)!*/)
```

1. Must be a valid furnace input.

Adding outputs: (requires exactly 1)

```groovy
.output(ItemStack)
```

Set bonus chance: (optional (default is 33%))

```groovy
.chance(float/*(1)!*/)
```

1. 0.0 = 0% / 1.0 = 100%

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

    ```groovy
    mods.thaumcraft.SmeltingBonus.recipeBuilder()
            .input(item('minecraft:cobblestone'))
            .output(item('minecraft:stone_button'))
            .chance(0.2F)
            .register()
    ```

### Removing Bonus

```groovy
mods.thaumcraft.SmeltingBonus.removeByOutput(ItemStack)
```

!!! example

    ```groovy
    mods.thaumcraft.SmeltingBonus.removeByOutput(item('minecraft:gold_nugget'))
    ```
