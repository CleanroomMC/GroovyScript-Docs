---
title: "Fusion"
description: "Consumes items and power from up to 54 pedestals of at least a given tier pointing towards a Fusion Crafting Core containing a catalyst to produce an output item."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/draconicevolution/Fusion.java"
---

# Fusion (Draconic Evolution)

## Description

Consumes items and power from up to 54 pedestals of at least a given tier pointing towards a Fusion Crafting Core containing a catalyst to produce an output item.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="3"
mods.de.fusion
mods.de.Fusion
mods.draconicevolution.fusion/*(1)!*/
mods.draconicevolution.Fusion
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Fusion also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.draconicevolution.fusion.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to 54.

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

    - `#!groovy int`. Sets the minimum tier of Fusion Crafting Injector. Requires greater than or equal to 0 and less than or equal to 3. (Default `0`).

        ```groovy
        tier(int)
        tierBasic()
        tierNormal()
        tierWyvern()
        tierChaotic()
        tierDraconic()
        ```

    - `#!groovy long`. Sets the power required per item input. Requires greater than 0. (Default `1000000`).

        ```groovy
        energy(long)
        ```

    - `#!groovy ItemStack`. Sets the item used in the center Fusion Crafting Controller block. Requires not null.

        ```groovy
        catalyst(ItemStack)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.brandon3055.draconicevolution.api.fusioncrafting.IFusionRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.draconicevolution.fusion.recipeBuilder()
            .catalyst(item('minecraft:diamond'))
            .input(ore('ingotIron'), ore('ingotIron'), item('minecraft:dirt'), item('minecraft:grass'), item('minecraft:grass'), item('minecraft:dirt'), ore('ingotGold'), ore('ingotGold'))
            .output(item('minecraft:nether_star'))
            .energy(10)
            .tier(1)
            .register()

        mods.draconicevolution.fusion.recipeBuilder()
            .catalyst(item('minecraft:diamond'))
            .input(item('minecraft:clay'), item('minecraft:clay'), item('minecraft:clay'), item('minecraft:clay'))
            .output(item('minecraft:nether_star'))
            .energy(100000)
            .tierChaotic()
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given catalyst:

    ```groovy
    mods.draconicevolution.fusion.removeByCatalyst(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.draconicevolution.fusion.removeAll()
    ```

???+ Example
    ```groovy
    mods.draconicevolution.fusion.removeByCatalyst(item('draconicevolution:chaos_shard'))
    mods.draconicevolution.fusion.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.draconicevolution.fusion.streamRecipes()
    ```
