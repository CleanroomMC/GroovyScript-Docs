---
title: "Anvil"
description: "When using hammer or pickaxe it can convert items"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/pyrotech/Anvil.java"
---

# Anvil (Pyrotech)

## Description

When using hammer or pickaxe it can convert items

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.pyrotech.anvil/*(1)!*/
mods.pyrotech.Anvil
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `name`, `input`, `output`, `hits`, `tier`, `type`:

    ```groovy
    mods.pyrotech.anvil.add(String, IIngredient, ItemStack, int, String, String)
    ```

???+ Example
    ```groovy
    mods.pyrotech.anvil.add('iron_to_clay', ore('ingotIron') * 5, item('minecraft:clay_ball') * 20, 9, 'granite', 'hammer')
    ```

### Recipe Builder

Just like other recipe types, the Anvil also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.pyrotech.anvil.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

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

    - `#!groovy int`. Sets how often the item needs to be hit. Requires greater than 0. (Default `0`).

        ```groovy
        hits(int)
        ```

    - `#!groovy AnvilRecipe.EnumTier`. Sets the tier of the required anvil (Granite, Ironclad, Obsidian).

        ```groovy
        tier(AnvilRecipe.EnumTier)
        tierGranite()
        tierIronclad()
        tierObsidian()
        ```

    - `#!groovy AnvilRecipe.EnumType`. Sets the type of tool required (Hammer, Pickaxe).

        ```groovy
        type(AnvilRecipe.EnumType)
        typeHammer()
        typePickaxe()
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `com.codetaylor.mc.pyrotech.modules.tech.basic.recipe.AnvilRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.pyrotech.anvil.recipeBuilder()
            .input(item('minecraft:diamond') * 4)
            .output(item('minecraft:emerald') * 2)
            .hits(5)
            .typeHammer()
            .tierGranite()
            .name('diamond_to_emerald_granite_anvil')
            .register()

        mods.pyrotech.anvil.recipeBuilder()
            .input(item('minecraft:diamond') * 8)
            .output(item('minecraft:nether_star') * 1)
            .hits(10)
            .typePickaxe()
            .tierIronclad()
            .name('diamond_to_nether_star_ironclad_anvil')
            .register()

        mods.pyrotech.anvil.recipeBuilder()
            .input(item('minecraft:diamond') * 4)
            .output(item('minecraft:gold_ingot') * 16)
            .hits(5)
            .typePickaxe()
            .tierObsidian()
            .name('diamond_to_gold_obsidian_anvil')
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.pyrotech.anvil.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.pyrotech.anvil.removeAll()
    ```

???+ Example
    ```groovy
    mods.pyrotech.anvil.removeByOutput(item('minecraft:stone_slab', 3))
    mods.pyrotech.anvil.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.pyrotech.anvil.streamRecipes()
    ```
