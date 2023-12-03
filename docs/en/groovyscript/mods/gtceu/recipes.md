# Recipes

GTCEu has a great recipe structure. Adding and removing is pretty much the same for each machine.
Recipes for a machine are stored in a `RecipeMap`.
You can get a recipe map like this:

```groovy
def recipeMap = mods.gregtech.recipe_map_name
// this works also:
def recipeMap2 = recipemap('recipe_map_name')
```

You can find a list of all machines [here](https://github.com/GregTechCEu/GregTech/wiki/CraftTweaker-for-Machines). <br>
Let's use `alloy_smelter` as an example here.
With the recipe map you can create a recipe builder.

```groovy
mods.gregtech.alloy_smelter.recipeBuilder()
```

You don't know what a builder is? Check [this](../../../groovy/builder.md) out.

## Builder functions

GregTechs recipe builder has tons of helper functions. We'll only focus on the important ones.

### Adding inputs

Works for fluid and items

```groovy
inputs(IIngredient ingredient)
inputs(IIngredient... ingredients)
inputs(Collection<IIngredient> ingredients)
notConsumable(IIngredient ingredient) // this will not be consumed
```

### Adding outputs

```groovy
outputs(ItemStack)
outputs(ItemStack...)
outputs(Collection<ItemStack>)
chancedOutput(ItemStack, int chance, int tierChanceBoost) // this will not be consumed

fluidOutputs(FluidStack)
fluidOutputs(FluidStack...)
fluidOutputs(Collection<FluidStack>)
```

### Other

```groovy
duration(int duration) // base recipe duration int ticks (20 ticks = 1 sec)
EUt(int EUt)
hidden() // hides recipe in jei

cleanroom(CleanroomType) // makes the recipe require cleanroom
```

### Register recipe

```groovy
buildAndRegister()
```

## Example

```groovy
import gregtech.api.metatileentity.multiblock.CleanroomType // needed when you want to use cleanroom

mods.gregtech.alloy_smelter.recipeBuilder()
    .inputs(item('minecraft:dirt'), ore('stone'))
    .outputs(item('minecraft:nether_star') * 2)
    .cleanroom(CleanroomType.CLEANROOM) // CLEANROOM and STERILE_CLEANROOM are valid
    .duration(200) // 10 seconds
    .EUt(512) // HV recipe
    .buildAndRegister()
```
