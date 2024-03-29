---
title: "Flower Generation"
description: "When running the Flower Growth Ritual, allowed flowers will generate in the area. Additionally, using the spell Growth Infusion's Floral Reproduction modifier will duplicate the flower."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/FlowerGeneration.java"
---

# Flower Generation (Roots 3)

## Description

When running the Flower Growth Ritual, allowed flowers will generate in the area. Additionally, using the spell Growth Infusion's Floral Reproduction modifier will duplicate the flower.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.roots.flower_generation/*(1)!*/
mods.roots.flowergeneration
mods.roots.flowerGeneration
mods.roots.FlowerGeneration
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

### Recipe Builder

Just like other recipe types, the Flower Generation also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.flower_generation.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy IBlockState`. Sets the flower blockstate. Requires not null.

        ```groovy
        flower(Block, int)
        flower(IBlockState)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.recipe.FlowerRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.flower_generation.recipeBuilder()
            .name('clay_flower')
            .flower(blockstate('minecraft:clay'))
            .register()
        ```



## Removing Entries

- Removes all Flower Generation entries with the given Block:

    ```groovy
    mods.roots.flower_generation.removeByFlower(Block)
    ```

- Removes the Flower Generation entry with the given Block and int metadata:

    ```groovy
    mods.roots.flower_generation.removeByFlower(Block, int)
    ```

- Removes the Flower Generation entry with the given IBlockState:

    ```groovy
    mods.roots.flower_generation.removeByFlower(IBlockState)
    ```

- Removes the Flower Generation entry with the given ItemStack converted into an IBlockState:

    ```groovy
    mods.roots.flower_generation.removeByFlower(ItemStack)
    ```

- Removes the Flower Generation entry with the given name:

    ```groovy
    mods.roots.flower_generation.removeByName(ResourceLocation)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.flower_generation.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.flower_generation.removeByFlower(block('minecraft:red_flower'))
    mods.roots.flower_generation.removeByFlower(block('minecraft:red_flower'), 1)
    mods.roots.flower_generation.removeByFlower(blockstate('minecraft:red_flower:2'))
    mods.roots.flower_generation.removeByFlower(item('minecraft:red_flower:3'))
    mods.roots.flower_generation.removeByName(resource('roots:dandelion'))
    mods.roots.flower_generation.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.flower_generation.streamRecipes()
    ```
