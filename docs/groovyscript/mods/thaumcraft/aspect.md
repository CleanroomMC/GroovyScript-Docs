---
title: "Aspect Creator"
description: "Creates a custom Aspect."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/thaumcraft/aspect/Aspect.java"
---

# Aspect Creator (Thaumcraft)

## Description

Creates a custom Aspect.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.thaumcraft.aspect/*(1)!*/
mods.thaumcraft.Aspect
mods.tc.aspect
mods.tc.Aspect
mods.thaum.aspect
mods.thaum.Aspect
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Aspect Creator also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.thaumcraft.aspect.aspectBuilder()"
    - `#!groovy String`. Sets the name of the new Aspect. Requires not null. Requires the name must be a unique string.

        ```groovy
        tag(String)
        ```

    - `#!groovy int`. Sets the blend value of the Aspect. (Default `1`).

        ```groovy
        blend(int)
        ```

    - `#!groovy ResourceLocation`. Sets the resource location of the image used to represent the Aspect.

        ```groovy
        image(String)
        image(String, String)
        image(ResourceLocation)
        ```

    - `#!groovy int`. Sets the color formatting code used. (Default `0`).

        ```groovy
        chatColor(int)
        ```

    - `#!groovy AspectList`. Sets the other Aspects that make up this Aspect. Requires greater than or equal to 0 and less than or equal to 2.

        ```groovy
        component(String)
        component(AspectStack)
        component(String, int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `thaumcraft.api.aspects.Aspect`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.thaumcraft.aspect.aspectBuilder()
            .tag('humor')
            .chatColor(14013676)
            .component(aspect('cognitio'))
            .component('perditio')
            .image(resource('thaumcraft:textures/aspects/humor.png'))
            .register()
        ```



## Removing Recipes

- Removes all registered recipes:

    ```groovy
    mods.thaumcraft.aspect.removeAll()
    ```

???+ Example
    ```groovy
    mods.thaumcraft.aspect.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.thaumcraft.aspect.streamRecipes()
    ```
