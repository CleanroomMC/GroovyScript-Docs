---
title: "Inscriber"
description: "Converts an item into another item, requiring either one or two additional items as either catalysts or ingredients."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/appliedenergistics2/Inscriber.java"
---

# Inscriber (Applied Energistics 2)

## Description

Converts an item into another item, requiring either one or two additional items as either catalysts or ingredients.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.appliedenergistics2.Inscriber
mods.appliedenergistics2.inscriber/*(1)!*/
mods.ae2.Inscriber
mods.ae2.inscriber
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Inscriber also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.appliedenergistics2.inscriber.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy ItemStack`. Sets the top item of the inscriber recipe. Requires either top or bottom to be non-empty.

        ```groovy
        top(ItemStack)
        ```

    - `#!groovy InscriberProcessType`. Sets the type of recipe, determining if the top/bottom items function as catalysts. Requires not null.

        ```groovy
        type(String)
        type(InscriberProcessType)
        press()
        inscribe()
        ```

    - `#!groovy ItemStack`. Sets the bottom item of the inscriber recipe. Requires either top or bottom to be non-empty.

        ```groovy
        bottom(ItemStack)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `appeng.api.features.IInscriberRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.appliedenergistics2.inscriber.recipeBuilder()
            .input(ore('blockGlass'))
            .output(item('minecraft:diamond'))
            .top(item('minecraft:diamond'))
            .bottom(item('minecraft:diamond'))
            .inscribe()
            .register()

        mods.appliedenergistics2.inscriber.recipeBuilder()
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:diamond'))
            .top(item('minecraft:diamond'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.appliedenergistics2.inscriber.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.appliedenergistics2.inscriber.removeAll()
    ```

???+ Example
    ```groovy
    mods.appliedenergistics2.inscriber.removeByOutput(item('appliedenergistics2:material:59'))
    mods.appliedenergistics2.inscriber.removeAll()
    ```
