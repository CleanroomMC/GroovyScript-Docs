# Arcane Workbench

The recipe builder for the Arcane Workbench works very similar to the vanilla [Crafting Table](../../minecraft/crafting_builders.md). Except that you can add a required Research, Vis and Aspects.

### Adding Shapeless Recipes

Just like other recipe types, the Arcane Workbench also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.thaumcraft.ArcaneWorkbench.shapelessBuilder()
```

Adding inputs: (requires 1-9)

```groovy
.input(IIngredient)
.input(IIngredient...)
.input(Collection<IIngredient>)
```

Adding outputs: (requires exactly 1)

```groovy
.output(ItemStack)
```

Adding research requirement: (optional (default is ""))

```groovy
.researchKey(String) // (1)
```

1. Please see the examples below to better understand how this works

Adding aspects: (optional)

```groovy
.aspect(AspectStack) // must be a primal aspect
```

Adding vis requirement: (optional (default is 0))

```groovy
.vis(int) // (1)
```

1. Amount of vis required to craft, must be >= 0

Register recipe: (returns nothing)

```groovy
.register()
```

### Example

```groovy
mods.thaumcraft.ArcaneWorkbench.shapelessBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .input(item('minecraft:pumpkin'))
        .input(item('minecraft:stick'))
        .input(item('minecraft:stick'))
        .output(item('thaumcraft:void_hoe'))
        .vis(0)
        .register()
```

### Adding Shaped Recipes

```groovy
mods.thaumcraft.ArcaneWorkbench.shapedBuilder()
```

Creating the recipe's layout (required):

```groovy
matrix(String... matrix)
shape(String... matrix) // does the same thing as matrix()

// to input a matrix in the style of non-builder shaped addition
matrix(List<List<IIngredient>> matrix)
shape(List<List<IIngredient>> matrix)
```

Matching ingredients to the recipe layout (required):

```groovy
.key(String, IIngredient)  // (1)
```

1. Please see the examples below to better understand how this works

Adding outputs: (requires exactly 1)

```groovy
.output(ItemStack)
```

Adding research requirement: (optional (default is ""))

```groovy
.researchKey(String)  // (1)
```

1. Please see the examples below to better understand how this works

Adding aspects: (optional)

```groovy
.aspect(AspectStack) // must be a primal aspect
```

Adding vis requirement: (optional (default is 0))

```groovy
.vis(int) // amount of vis required to craft. must be >= 0
```

Register recipe: (returns nothing)

```groovy
.register()
```

### Example

```groovy
mods.thaumcraft.ArcaneWorkbench.shapedBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .output(item('minecraft:pumpkin'))
        .row('SS ')
        .row('   ')
        .row('   ')
        .key('S', item('minecraft:pumpkin_seeds'))
        .aspect(aspect('terra'))
        .vis(5)
        .register()

mods.thaumcraft.ArcaneWorkbench.shapedBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .output(item('minecraft:pumpkin'))
        .matrix('SS ',
                '   ',
                '   ')
        .key('S', item('minecraft:pumpkin_seeds'))
        .aspect(aspect('terra'))
        .vis(5)
        .register()
```

### Removing Recipes

This removes ALL recipes that match the given output:

```groovy
mods.thaumcraft.ArcaneWorkbench.removeByOutput(IIngredient)
```

!!! example
    ```groovy
    mods.thaumcraft.ArcaneWorkbench.removeByOutput(item('thaumcraft:mechanism_simple'))
    ```
