---
title: "Chemical Oxidizer"
description: "Converts an input itemstack into an output gasstack."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/ChemicalOxidizer.java"
---

# Chemical Oxidizer (Mekanism)

## Description

Converts an input itemstack into an output gasstack.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.mekanism.chemical_oxidizer/*(1)!*/
mods.mekanism.chemicaloxidizer
mods.mekanism.chemicalOxidizer
mods.mekanism.ChemicalOxidizer
mods.mekanism.oxidizer
mods.mekanism.Oxidizer
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `ingredient`, `output`:

    ```groovy
    mods.mekanism.chemical_oxidizer.add(IIngredient, GasStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.chemical_oxidizer.add(ore('dustGold'), gas('gold'))
    ```

### Recipe Builder

Just like other recipe types, the Chemical Oxidizer also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.chemical_oxidizer.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy GasStackList`. Sets the gas outputs of the recipe. Requires exactly 1.

        ```groovy
        gasOutput(GasStack)
        gasOutput(GasStack...)
        gasOutput(Collection<GasStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.OxidationRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.chemical_oxidizer.recipeBuilder()
            .input(ore('dustGold'))
            .gasOutput(gas('gold'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.chemical_oxidizer.removeByInput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.chemical_oxidizer.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.chemical_oxidizer.removeByInput(ore('dustSulfur'))
    mods.mekanism.chemical_oxidizer.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.chemical_oxidizer.streamRecipes()
    ```
