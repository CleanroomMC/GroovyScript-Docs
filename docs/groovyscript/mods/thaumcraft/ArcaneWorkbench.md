# Arcane Workbench

The recipe builder for the Arcane Workbench works very similar to the vanilla [Crafting Table](../../minecraft/crafting_builders.md). Except that you can add a required Research, Vis and Aspects.

## Adding Shapeless Recipes

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
.researchKey(String/*(1)!*/)
```

1. Please see the examples below to better understand how this works

Adding aspects: (optional)

```groovy
.aspect(AspectStack/*(1)!*/)
```

1. Must be a primal aspect: Ignis, Terra, Aer, Ordo, Aqua, or Perditio

Adding vis requirement: (optional (default is 0))

```groovy
.vis(int/*(1)!*/)
```

1. Amount of vis required to craft, must be >= 0.

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

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
row(String/*(1)!*/)

matrix(String... matrix/*(2)!*/)
shape(String... matrix) // does the same thing as matrix()

// to input a matrix in the style of non-builder shaped addition
matrix(List<List<IIngredient>> matrix)
shape(List<List<IIngredient>> matrix)
```

1. Must be called exactly 3 times, requires a String of length 3 characters. For empty slots use ` ` (space). See examples.
1. Matrix must be an array of 3 Strings, each of length 3 characters. For empty slots use ` ` (space). See examples.

Matching ingredients to the recipe layout (required):

```groovy
.key(Char, IIngredient)/*(1)!*/
```

1. Char is the ASCII character which represents the slot(s) in the recipe IIngredient will occupy.

Adding outputs: (requires exactly 1)

```groovy
.output(ItemStack)
```

Adding research requirement: (optional (default is ""))

```groovy
.researchKey(String/*(1)!*/)
```

1. The Research Key is the required research to craft the item, research is unlocked via the Thaumonomicon. Obtain a list of all research keys by doing `/tc research list`.

Adding aspects: (optional)

```groovy
.aspect(AspectStack/*(1)!*/)
```

1. Must be a primal aspect: Ignis, Terra, Aer, Ordo, Aqua, or Perditio

Adding vis requirement: (optional (default is 0))

```groovy
.vis(int/*(1)!*/)
```

1. Amount of vis required to craft, must be >= 0.

Allow mirroring: (optional)

```groovy
.mirrored()/*(1)!*/
```

1. If called, the resultant recipe inputs can be mirrored along the x and y axis (see vanilla Axe recipes).

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

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
