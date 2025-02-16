---
title: "Altar of Blood"
titleTemplate: "Harken Scythe: Resharpened | Elite Modding Team"
description: "Converts an item into another item by using blood essence as fuel."
source_code_link: "https://github.com/Elite-Modding-Team/HarkenScytheResharpened/blob/main/src/main/java/mod/emt/harkenscythe/compat/groovyscript/HSGroovyScriptBloodAltarRecipes.java"
---

# Altar of Blood (Harken Scythe: Resharpened)

## Description

Converts an item into another item by using blood essence as fuel.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="3"
mods.harkenscythe.blood_altar
mods.harkenscythe.bloodaltar
mods.harkenscythe.bloodAltar
mods.harkenscythe.BloodAltar
```

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Altar of Blood also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../getting_started/builder.md) out.

???+ Abstract "mods.harkenscythe.blood_altar.recipeBuilder()"
	- `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

		```groovy
		input(IIngredient)
		input(IIngredient...)
		input(Collection<IIngredient>)
		```

	- `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1.

		```groovy
		output(ItemStack)
		output(ItemStack...)
		output(Collection<ItemStack>)
		```

	- `#!groovy int`. Required blood. Requires greater than or equal to 1.

		```groovy
		requiredBlood(int)
		```

	- First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mod.emt.harkenscythe.recipe.HSRecipeBloodAltar`).

		```groovy
		register()
		```

	???+ Example
		```groovy
		mods.harkenscythe.blood_altar.recipeBuilder()
			.input(item('minecraft:cobblestone'))
			.output(item('minecraft:gravel'))
			.requiredBlood(42)
			.register()
		```

## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.harkenscythe.blood_altar.removeByInput(IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.harkenscythe.blood_altar.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.harkenscythe.blood_altar.removeAll()
    ```

???+ Example
	```groovy
	mods.harkenscythe.blood_altar.removeByInput(item('minecraft:glass_bottle'))
	mods.harkenscythe.blood_altar.removeByOutput(item('harkenscythe:bloodweave_cloth'))
	mods.harkenscythe.blood_altar.removeAll()
	```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.harkenscythe.blood_altar.streamRecipes()
    ```
