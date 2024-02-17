---
title: "Entity/Block Aspects"
description: "Controls what Aspects are attached to entities or items."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/thaumcraft/aspect/AspectHelper.java"
---

# Entity/Block Aspects (Thaumcraft)

## Description

Controls what Aspects are attached to entities or items.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.thaumcraft.aspect_helper/*(1)!*/
mods.thaumcraft.aspecthelper
mods.thaumcraft.aspectHelper
mods.thaumcraft.AspectHelper
mods.tc.aspect_helper
mods.tc.aspecthelper
mods.tc.aspectHelper
mods.tc.AspectHelper
mods.thaum.aspect_helper
mods.thaum.aspecthelper
mods.thaum.aspectHelper
mods.thaum.AspectHelper
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds an Aspect to the given entity in the format `entity`, `aspect`:

    ```groovy
    mods.thaumcraft.aspect_helper.add(EntityEntry, AspectStack)
    ```

- Adds an Aspect to the given itemstack in the format `item`, `aspect`:

    ```groovy
    mods.thaumcraft.aspect_helper.add(ItemStack, AspectStack)
    ```

- Adds an Aspect to the given oredict in the format `oreDict`, `aspect`:

    ```groovy
    mods.thaumcraft.aspect_helper.add(OreDictIngredient, AspectStack)
    ```


### Recipe Builder

Just like other recipe types, the Entity/Block Aspects also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.thaumcraft.aspect_helper.aspectBuilder()"
    - `#!groovy EntityEntry`. Sets the entity being modified. Requires either entity or object must be defined, but not both.

        ```groovy
        entity(EntityEntry)
        ```

    - `#!groovy IIngredient`. Sets the item being modified. Requires either entity or object must be defined, but not both.

        ```groovy
        object(IIngredient)
        ```

    - `#!groovy ArrayList<AspectStack>`. Sets the Aspects of the entity or item.

        ```groovy
        aspect(AspectStack)
        aspect(String, int)
        ```

    - `#!groovy boolean`. Sets if all pre-existing Aspects should be removed from the entity or item before adding Aspects, if any are added. (Default `false`).

        ```groovy
        stripAspects()
        ```

    - First validates the builder, outputting errors to the log file if the validation failed, then registers the builder.

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.thaumcraft.aspect_helper.aspectBuilder()
            .object(item('minecraft:stone'))
            .stripAspects()
            .aspect(aspect('ignis') * 20)
            .aspect('ordo', 5)
            .register()

        mods.thaumcraft.aspect_helper.aspectBuilder()
            .object(ore('cropPumpkin'))
            .stripAspects()
            .aspect(aspect('herba') * 20)
            .register()

        mods.thaumcraft.aspect_helper.aspectBuilder()
            .entity(entity('minecraft:chicken'))
            .stripAspects()
            .aspect('bestia', 20)
            .register()
        ```



## Removing Recipes

- Removes an Aspect from the given entity in the format `entity`, `aspect`:

    ```groovy
    mods.thaumcraft.aspect_helper.remove(EntityEntry, AspectStack)
    ```

- Removes an Aspect from the given itemstack in the format `item`, `aspect`:

    ```groovy
    mods.thaumcraft.aspect_helper.remove(ItemStack, AspectStack)
    ```

- Removes an Aspect from the given oredict in the format `oreDict`, `aspect`:

    ```groovy
    mods.thaumcraft.aspect_helper.remove(OreDictIngredient, AspectStack)
    ```

- Removes all Aspects from the given entity:

    ```groovy
    mods.thaumcraft.aspect_helper.removeAll(EntityEntry)
    ```

- Removes all Aspects from the given itemstack:

    ```groovy
    mods.thaumcraft.aspect_helper.removeAll(ItemStack)
    ```

- Removes all Aspects from the given oredict:

    ```groovy
    mods.thaumcraft.aspect_helper.removeAll(OreDictIngredient)
    ```
