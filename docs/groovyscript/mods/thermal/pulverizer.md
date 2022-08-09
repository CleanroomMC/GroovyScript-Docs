# Thermal Expansion Pulverizer

## Adding Recipes
Just like other recipe types, the Pulverizer also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out
```groovy
mods.thermal.Pulverizer.recipeBuilder()
```

Set input: (requires exactly 1)
```groovy
.input(IIngredient)
```

Set output: (requires exactly 1)
```groovy
.output(ItemStack)
```

Set secondary Output: (optional)
````groovy
.secondaryOutput(ItemStack)             // default chance is 100%
.secondaryOutput(ItemStack, int chance) // chance is a number from 0 to 100 where 100 is 100%  
````

Set required total energy: (optional (default is 3000))
```groovy
.energy(int)
```

Register recipe: (returns `cofh.thermalexpansion.util.managers.machine.PulverizerManager.PulverizerRecipe`)
````groovy
.register()
````

### Example
This creates a recipe where bookshelf turns into a diamond with an extra 1% chance for an extra diamond.
````groovy
mods.thermal.Pulverizer.recipeBuilder()
        .input('<minecraft:bookshelf>')
        .output('<minecraft:diamond>')
        .secondaryOutput('<minecraft:diamond>', 1)
        .energy(2000)
        .register()
````

## Removing Recipes
This removes a recipe that match the given input:
````groovy
mods.thermal.Pulverizer.removeByInput(ItemStack output)
````

### Example
````groovy
// removes Iron Ingot from Pulverizer
mods.thermal.Pulverizer.removeByInput('<minecraft:iron_ingot>')
````