---
title: "Infusion Crafting"
description: "Combines any number of items and aspects together in the Infusion Altar, potentially requiring a specific research to be completed."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/thaumcraft/InfusionCrafting.java"
---

# Infusion Crafting (Thaumcraft)

## Description

Combines any number of items and aspects together in the Infusion Altar, potentially requiring a specific research to be completed.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.thaumcraft.infusion_crafting/*(1)!*/
mods.thaumcraft.infusioncrafting
mods.thaumcraft.infusionCrafting
mods.thaumcraft.InfusionCrafting
mods.tc.infusion_crafting
mods.tc.infusioncrafting
mods.tc.infusionCrafting
mods.tc.InfusionCrafting
mods.thaum.infusion_crafting
mods.thaum.infusioncrafting
mods.thaum.infusionCrafting
mods.thaum.InfusionCrafting
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `research`, `outputResult`, `inst`, `aspects`, `centralItem`, `input`:

    ```groovy
    mods.thaumcraft.infusion_crafting.add(String, ItemStack, int, Collection<AspectStack>, IIngredient, IIngredient...)
    ```


### Recipe Builder

Just like other recipe types, the Infusion Crafting also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.thaumcraft.infusion_crafting.recipeBuilder()"
    - `#!groovy AspectList`. Sets the Aspects and amounts required to complete the craft.

        ```groovy
        aspect(AspectStack)
        aspect(String, int)
        ```

    - `#!groovy IIngredient`. Sets the item on the center pedestal. Requires not null.

        ```groovy
        mainInput(IIngredient)
        ```

    - `#!groovy int`. Sets the instability of the recipe. (Default `0`).

        ```groovy
        instability(int)
        ```

    - `#!groovy String`. Sets the research required to craft the recipe.

        ```groovy
        researchKey(String)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `thaumcraft.api.crafting.InfusionRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.thaumcraft.infusion_crafting.recipeBuilder()
            .researchKey('UNLOCKALCHEMY@3')
            .mainInput(item('minecraft:gunpowder'))
            .output(item('minecraft:gold_ingot'))
            .aspect(aspect('terra') * 20)
            .aspect('ignis', 30)
            .input(crystal('aer'))
            .input(crystal('ignis'))
            .input(crystal('aqua'))
            .input(crystal('terra'))
            .input(crystal('ordo'))
            .instability(10)
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.thaumcraft.infusion_crafting.removeByOutput(IIngredient)
    ```

- Removes all registered recipes:

    ```groovy
    mods.thaumcraft.infusion_crafting.removeAll()
    ```

???+ Example
    ```groovy
    mods.thaumcraft.infusion_crafting.removeByOutput(item('thaumcraft:crystal_terra'))
    mods.thaumcraft.infusion_crafting.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.thaumcraft.infusion_crafting.streamRecipes()
    ```
