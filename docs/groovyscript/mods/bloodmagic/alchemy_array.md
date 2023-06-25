# Blood Magic Alchemy Array

Package:

```groovy
mods.bloodmagic.AlchemyArray
```

!!! Note
    An Alchemy Array is created in-world via Right Clicking Arcane Ashes on the ground.
    Right Clicking first the input and then the catalyst on the Arcane Ashes will cause an animation, ending with the item being spawned in-world.

## Adding Recipes

Just like other recipe types, the Alchemy Array also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.bloodmagic.AlchemyArray.recipeBuilder()
```

Adding inputs: (requires exactly 1)

```groovy
.input(IIngredient)
.input(IIngredient...)
.input(Collection<IIngredient>)
```

Setting catalyst item: (required exactly 1)

```groovy
.catalyst(IIngredient)
```

Setting the texture location: (option (default WIP))

```groovy
.texture(String)
.texture(ResourceLocation)
```

Adding output: (requires exactly 1)

```groovy
.output(ItemStack)
```

Register recipe: (returns `WayofTime.bloodmagic.api.impl.recipe.RecipeAlchemyArray`)

```groovy
.register()
```

!!! example

    ```groovy
    mods.bloodmagic.AlchemyArray.recipeBuilder()
            .input(item("minecraft:diamond"))
            .catalyst(item("bloodmagic:slate:1"))
            .output(item("minecraft:gold_ingot"))
            .register()

    mods.bloodmagic.AlchemyArray.recipeBuilder()
            .input(item("minecraft:clay"))
            .catalyst(item("minecraft:gold_ingot"))
            .output(item("minecraft:diamond"))
            .texture("bloodmagic:textures/models/AlchemyArrays/LightSigil.png")
            .register()
    ```

## Removing Recipes

This removes ALL recipes that match the given input:

```groovy
mods.bloodmagic.AlchemyArray.removeByInput(IIngredient)
```

This removes ALL recipes that match the given catalyst:

```groovy
mods.bloodmagic.AlchemyArray.removeByCatalyst(IIngredient)
```

This removes ALL recipes that match both the given input and catalyst:

```groovy
mods.bloodmagic.AlchemyArray.removeByInputAndCatalyst(IIngredient input, IIngredient catalyst)
```

This removes ALL recipes that match the given output:

```groovy
mods.bloodmagic.AlchemyArray.removeByOutput(ItemStack)
```

Removes all registed Alchemy Array recipes:

```groovy
mods.bloodmagic.AlchemyArray.removeAll()
```

!!! example

    ```groovy
    // Removes all recipes that have an input of Haste Reagent. (1)
    mods.bloodmagic.AlchemyArray.removeByInput(item("bloodmagic:component:13"))

    // Removes all recipes that have the target catalyst item. (2)
    mods.bloodmagic.AlchemyArray.removeByCatalyst(item("bloodmagic:slate:2"))

    // Removes all recipes that have both the target input and catalyst items. (3)
    mods.bloodmagic.AlchemyArray.removeByInputAndCatalyst(item("bloodmagic:component:7"), item("bloodmagic:slate:1"))

    // Removes all recipes that output the Sigil of the Void.
    mods.bloodmagic.AlchemyArray.removeByOutput(item("bloodmagic:sigil_void"))
    ```

    1. This would remove the recipe for the Sigil of Haste.
    2. This would remove the recipe for the Sigil of the Claw, Elemental Affinity, Magnetism, Blood Lamp, and Holding.
    3. This would remove the recipe for the Seer's Sigil.
