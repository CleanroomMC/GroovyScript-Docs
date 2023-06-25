# Infusion Crafting

## Add a recipe

Just like other recipe types, Infusion Crafting also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.thaumcraft.InfusionCrafting.recipeBuilder()
```

Adding center pedestal item: (requires exactly 1)

```groovy
.mainInput(IIngredient)
```

Adding input: (requires at least 1)

```groovy
.input(IIngredient)
.input(IIngredient...)
.input(Collection<IIngredient>)
```

Adding outputs: (requires exactly 1)

```groovy
.output(ItemStack)
```

Adding aspects: (requires at least 1)

```groovy
.aspect(AspectStack)
```

Adding research requirement: (optional (default is ""))

```groovy
.researchKey(String/*(1)!*/)
```

1. The Research Key is the required research to craft the item, research is unlocked via the Thaumonomicon. Obtain a list of all research keys by doing `/tc research list`.

Adding instability: (required)

```groovy
.instability(int)
```

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

    ```groovy
    mods.thaumcraft.InfusionCrafting.recipeBuilder()
            .researchKey('UNLOCKALCHEMY@3')
            .mainInput(item('minecraft:gunpowder'))
            .output(item('minecraft:gold_ingot'))
            .aspect(aspect('terra') * 20)
            .aspect(aspect('ignis') * 30)
            .input(crystal('aer'))
            .input(crystal('ignis'))
            .input(crystal('aqua'))
            .input(crystal('terra'))
            .input(crystal('ordo'))
            .instability(10)
            .register()
    ```

### Remove a recipe

```groovy
mods.thaumcraft.InfusionCrafting.removeByOutput(IIngredient)
```

!!! example

    ```groovy
    mods.thaumcraft.InfusionCrafting.removeByOutput(item('thaumcraft:crystal_terra'))
    ```
