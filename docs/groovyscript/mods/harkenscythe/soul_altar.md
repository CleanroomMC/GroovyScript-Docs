---
title: "Altar of Souls"
titleTemplate: "Harken Scythe: Resharpened | Elite Modding Team"
description: "Converts an item into another item by using soul essence as fuel."
source_code_link: "https://github.com/Elite-Modding-Team/HarkenScytheResharpened/blob/main/src/main/java/mod/emt/harkenscythe/compat/groovyscript/HSGroovyScriptSoulAltarRecipes.java"
---

# Altar of Souls (Harken Scythe: Resharpened)

## Description

Converts an item into another item by using soul essence as fuel.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="3"
mods.harkenscythe.soul_altar
mods.harkenscythe.soulaltar
mods.harkenscythe.soulAltar
mods.harkenscythe.SoulAltar
```

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Altar of Souls also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../getting_started/builder.md) out.

???+ Abstract "mods.harkenscythe.soul_altar.recipeBuilder()"
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

	- `#!groovy int`. Required souls. Requires greater than or equal to 1.

		```groovy
		requiredSouls(int)
		```

	- First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mod.emt.harkenscythe.recipe.HSRecipeSoulAltar`).

		```groovy
		register()
		```

	???+ Example
		```groovy
		mods.harkenscythe.soul_altar.recipeBuilder()
			.input(item('minecraft:gravel'))
			.output(item('minecraft:sand'))
			.requiredSouls(69)
			.register()
		```

## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.harkenscythe.soul_altar.removeByInput(IIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.harkenscythe.soul_altar.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.harkenscythe.soul_altar.removeAll()
    ```

???+ Example
	```groovy
	mods.harkenscythe.soul_altar.removeByInput(item('minecraft:cookie'))
	mods.harkenscythe.soul_altar.removeByOutput(item('harkenscythe:soul_cake'))
	mods.harkenscythe.soul_altar.removeAll()
	```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.harkenscythe.soul_altar.streamRecipes()
    ```
