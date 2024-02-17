---
title: "Animal Harvest"
description: "Animal Harvest is a ritual that drops items from nearby mob's based on that mobs loottable without harming the mob. Only applies to allowed mobs."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/AnimalHarvest.java"
---

# Animal Harvest (Roots 3)

## Description

Animal Harvest is a ritual that drops items from nearby mob's based on that mobs loottable without harming the mob. Only applies to allowed mobs.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.roots.animal_harvest/*(1)!*/
mods.roots.animalharvest
mods.roots.animalHarvest
mods.roots.AnimalHarvest
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Animal Harvest also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.animal_harvest.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy Class<? extends EntityLivingBase>`. Sets the target entity. Requires not null.

        ```groovy
        entity(EntityEntry)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.recipe.AnimalHarvestRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.animal_harvest.recipeBuilder()
            .name('wither_skeleton_harvest')
            .entity(entity('minecraft:wither_skeleton'))
            .register()

        mods.roots.animal_harvest.recipeBuilder()
            .entity(entity('minecraft:enderman'))
            .register()
        ```



## Removing Recipes

- Removes any Animal Harvest recipe with the given entity:

    ```groovy
    mods.roots.animal_harvest.removeByEntity(EntityEntry)
    ```

- Removes the Animal Harvest recipe with the given name:

    ```groovy
    mods.roots.animal_harvest.removeByName(ResourceLocation)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.animal_harvest.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.animal_harvest.removeByEntity(entity('minecraft:pig'))
    mods.roots.animal_harvest.removeByName(resource('roots:chicken'))
    mods.roots.animal_harvest.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.animal_harvest.streamRecipes()
    ```
