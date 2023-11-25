---
title: "Mortar And Pestle"
description: "When right clicking a mortar containing the input items with a pestle, it will display a few colored sparkles, consume the inputs, and drop the item output."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/Mortar.java"
---

# Mortar And Pestle (Roots 3)

## Description

When right clicking a mortar containing the input items with a pestle, it will display a few colored sparkles, consume the inputs, and drop the item output.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.roots.Mortar
mods.roots.mortar/*(1)!*/
mods.roots.MortarAndPestle
mods.roots.mortarandpestle
mods.roots.mortarAndPestle
mods.roots.mortar_and_pestle
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Mortar And Pestle also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.mortar.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe. (Default `null`).

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to 5. (Default `null`).

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

    - `#!groovy float`. Sets the red color value of the first version of the particle spawned. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        red(float)
        red(float, float)
        red1(float)
        color(float, float, float)
        color(float, float, float, float, float, float)
        ```

    - `#!groovy float`. Sets the red color value of the second version of the particle spawned. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        red(float)
        red(float, float)
        red2(float)
        color(float, float, float)
        color(float, float, float, float, float, float)
        ```

    - `#!groovy float`. Sets the blue color value of the first version of the particle spawned. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        blue(float)
        blue(float, float)
        blue1(float)
        color(float, float, float)
        color(float, float, float, float, float, float)
        ```

    - `#!groovy float`. Sets the blue color value of the second version of the particle spawned. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        blue(float)
        blue(float, float)
        blue2(float)
        color(float, float, float)
        color(float, float, float, float, float, float)
        ```

    - `#!groovy float`. Sets the green color value of the first version of the particle spawned. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        color(float, float, float)
        color(float, float, float, float, float, float)
        green(float)
        green(float, float)
        green1(float)
        ```

    - `#!groovy float`. Sets the green color value of the second version of the particle spawned. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        color(float, float, float)
        color(float, float, float, float, float, float)
        green(float)
        green(float, float)
        green2(float)
        ```

    - `#!groovy boolean`. Sets if, when input has a single IIngredient, a recipe will be generated for each input amount.

        ```groovy
        generate()
        generate(boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.recipe.MortarRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.mortar.recipeBuilder()
            .name('clay_mortar')
            .input(item('minecraft:stone'),item('minecraft:gold_ingot'),item('minecraft:stone'),item('minecraft:gold_ingot'),item('minecraft:stone'))
            .generate(false)
            .output(item('minecraft:clay'))
            .color(1, 0, 0.1, 1, 0, 0.1)
            .register()

        mods.roots.mortar.recipeBuilder()
            .input(item('minecraft:clay'))
            .output(item('minecraft:diamond'))
            .color(0, 0, 0.1)
            .register()

        mods.roots.mortar.recipeBuilder()
            .input(item('minecraft:diamond'), item('minecraft:diamond'))
            .output(item('minecraft:gold_ingot') * 16)
            .red(0)
            .green1(0.5)
            .green2(1)
            .register()
        ```



## Removing Recipes

- Removes the Mortar recipe with the given name:

    ```groovy
    mods.roots.mortar.removeByName(ResourceLocation)
    ```

- Removes the Mortar recipe with the given output itemstack:

    ```groovy
    mods.roots.mortar.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.mortar.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.mortar.removeByName(resource('roots:wheat_flour'))
    mods.roots.mortar.removeByOutput(item('minecraft:string'))
    mods.roots.mortar.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.mortar.streamRecipes()
    ```
