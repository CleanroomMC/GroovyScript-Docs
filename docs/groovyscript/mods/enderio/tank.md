# EnderIO Tank

EnderIO Tanks can not only store fluids but also empty and fill fluid containers.
You can add custom fill/drain recipes to get custom behaviour. For example you can add a `water + sponge = wet sponge` recipe.

## Adding Recipes

### Filling

Adds a recipe that will fill the input `IIngredient` with the input `FluidStack` and results in the output `ItemStack`.

```groovy
mods.enderio.Tank.addFill(IIngredient input, FluidStack inputFluid, ItemStack output)
```

### Draining

Adds a recipe that will drain the output `FluidStack` from the input `IIngredient` and results in the output `ItemStack`.

```groovy
mods.enderio.Tank.addDrain(IIngredient input, FluidStack outputFluid, ItemStack output)
```

## Removing Recipes

### Filling

Removes a filling recipe:

```groovy
mods.enderio.Tank.removeFill(FluidStack inputFluid, ItemStack output)
```

### Draining

Removes a filling recipe:

```groovy
mods.enderio.Tank.removeDrain(FluidStack outputFluid, ItemStack output)
```
