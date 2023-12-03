# Crucible

## Adding Recipes

Just like other recipe types, the Crucible also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.thaumcraft.Crucible.recipeBuilder()
```

Adding catalyst: (requires exactly 1)

```groovy
.catalyst(IIngredient)
```

Adding outputs: (requires exactly 1)

```groovy
.output(ItemStack)
```

Adding research requirement: (optional (default is ""))

```groovy
.researchKey(String/*(1)!*/)
```

1. The Research Key is the required research to craft the item, research is unlocked via the Thaumonomicon. Obtain a list of all research keys by doing `/tc research list`.

Adding aspects: (requires at least 1)

```groovy
.aspect(AspectStack)
```

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

    ```groovy
    mods.thaumcraft.Crucible.recipeBuilder()
            .researchKey('UNLOCKALCHEMY@3')
            .catalyst(item('minecraft:rotten_flesh'))
            .output(item('minecraft:gold_ingot'))
            .aspect(aspect('metallum') * 10)
            .register()
    ```

### Removing Recipes

```groovy
mods.thaumcraft.Crucible.removeByOutput(IIngredient)
```

!!! example

    ```groovy
    mods.thaumcraft.Crucible.removeByOutput(item('minecraft:gunpowder'))
    ```
