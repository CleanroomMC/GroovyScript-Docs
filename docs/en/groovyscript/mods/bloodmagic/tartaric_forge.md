# Blood Magic Tartaric Forge

Package:

```groovy
mods.bloodmagic.TartaricForge
```

!!! Note
    The Tartaric Forge requires a Tartaric Gem to provide Demonic Will to the recipe. Only Raw Will can be used.
    Each recipe requires a minimum amount of Will inside the Gem to start, and consumes a smaller amount of Will on completion.

## Adding Recipes

Just like other recipe types, the Tartaric Forge also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.bloodmagic.TartaricForge.recipeBuilder()
```

Adding inputs: (requires 1-4)

```groovy
.input(IIngredient)
.input(IIngredient...)
.input(Collection<IIngredient>)
```

Setting the amount of souls removed from the Tartaic Gem: (required)

```groovy
.drain(int)
.soulDrain(int)
```

Setting the amount of souls required in the Tartaric Gem: (required (if less than the amount removed, set to the amount removed))

```groovy
.minimumSouls(int)
```

Adding output: (requires exactly 1)

```groovy
.output(ItemStack)
```

Register recipe: (returns `WayofTime.bloodmagic.api.impl.recipe.RecipeTartaricForge`)

```groovy
.register()
```

!!! example

    ```groovy
    mods.bloodmagic.TartaricForge.recipeBuilder()
            .input(item("minecraft:clay"), item("minecraft:clay"), item("minecraft:clay"), item("minecraft:clay"))
            .output(item("minecraft:gold_ingot"))
            .drain(5)
            .minimumSouls(10)
            .register()

    mods.bloodmagic.TartaricForge.recipeBuilder()
            .input(item("minecraft:gold_ingot"), item("minecraft:clay"))
            .output(item("minecraft:diamond"))
            .soulDrain(200)
            .minimumSouls(500)
            .register()
    ```

## Removing Recipes

This removes ALL recipes which have all input ingredients[^1]:

```groovy
mods.bloodmagic.TartaricForge.removeByInput(NonNullList<IIngredient>)
mods.bloodmagic.TartaricForge.removeByInput(IIngredient...)
```

This removes ALL recipes that match the given output:

```groovy
mods.bloodmagic.TartaricForge.removeByOutput(ItemStack)
```

Removes all registed Tartaric Forge recipes:

```groovy
mods.bloodmagic.TartaricForge.removeAll()
```

!!! example

    ```groovy
    // Removes all recipes that have inputs Cauldron, Stone, Lapis, and Diamond. (1)
    mods.bloodmagic.TartaricForge.removeByInput(item("minecraft:cauldron"), item("minecraft:stone"), item("minecraft:dye:4"), item("minecraft:diamond"))

    // Removes all recipes that have inputs including both Gunpowder and Redstone. (2)
    mods.bloodmagic.TartaricForge.removeByInput(item("minecraft:gunpowder"), item("minecraft:redstone"))

    // Removes all recipes that output Blood Magic's Demon Crystal.
    mods.bloodmagic.TartaricForge.removeByOutput(item("bloodmagic:demon_crystal"))
    ```

    1. This would remove the recipe for the Demon Crucible.
    2. This would the remove recipes for both Arcane Ashes and Binding Reagent.

[^1]: Note that a recipe with inputs "ABCD" would match with a target containing only "AB".
