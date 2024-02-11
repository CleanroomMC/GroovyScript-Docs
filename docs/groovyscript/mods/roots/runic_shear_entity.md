---
title: "Runic Shear Entity"
description: "Right clicking a Runic Shear on an entity. The entity will have a cooldown, preventing spamming."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/RunicShearEntity.java"
---

# Runic Shear Entity (Roots 3)

## Description

Right clicking a Runic Shear on an entity. The entity will have a cooldown, preventing spamming.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.roots.runic_shear_entity/*(1)!*/
mods.roots.runicshearentity
mods.roots.runicShearEntity
mods.roots.RunicShearEntity
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Runic Shear Entity also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.runic_shear_entity.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires greater than or equal to 1.

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy Class<? extends EntityLivingBase>`. Sets the target entity. Requires not null.

        ```groovy
        entity(EntityEntry)
        ```

    - `#!groovy int`. Sets the time in ticks before the entity can be sheared again. Requires not null. (Default `0`).

        ```groovy
        cooldown(int)
        ```

    - `#!groovy Function<EntityLivingBase, ItemStack>`. Sets a function that takes an EntityLivingBase and returns an itemstack drop based on the entities properties.

        ```groovy
        functionMap(Function<EntityLivingBase, ItemStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.recipe.RunicShearEntityRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.runic_shear_entity.recipeBuilder()
            .name('clay_from_wither_skeletons')
            .entity(entity('minecraft:wither_skeleton'))
            .output(item('minecraft:clay'))
            .cooldown(1000)
            .register()

        mods.roots.runic_shear_entity.recipeBuilder()
            .name('creeper_at_the_last_moment')
            .entity(entity('minecraft:creeper'))
            .output(item('minecraft:diamond'), item('minecraft:nether_star'))
            .functionMap({ entityLivingBase -> entityLivingBase.hasIgnited() ? item('minecraft:nether_star') : item('minecraft:dirt') })
            .register()

        mods.roots.runic_shear_entity.recipeBuilder()
            .entity(entity('minecraft:witch'))
            .output(item('minecraft:clay'))
            .register()
        ```



## Removing Recipes

- Removes the Runic Shear Entity recipe for the given Entity:

    ```groovy
    mods.roots.runic_shear_entity.removeByEntity(Class<? extends EntityLivingBase>)
    ```

- Removes the Runic Shear Entity recipe for the given Entity:

    ```groovy
    mods.roots.runic_shear_entity.removeByEntity(EntityEntry)
    ```

- Removes the Runic Shear Entity recipe with the given name:

    ```groovy
    mods.roots.runic_shear_entity.removeByName(ResourceLocation)
    ```

- Removes the Runic Shear Entity recipe for the given output itemstack:

    ```groovy
    mods.roots.runic_shear_entity.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.roots.runic_shear_entity.removeAll()
    ```

???+ Example
    ```groovy
    mods.roots.runic_shear_entity.removeByEntity(entity('minecraft:chicken'))
    mods.roots.runic_shear_entity.removeByName(resource('roots:slime_strange_ooze'))
    mods.roots.runic_shear_entity.removeByOutput(item('roots:fey_leather'))
    mods.roots.runic_shear_entity.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.runic_shear_entity.streamRecipes()
    ```
