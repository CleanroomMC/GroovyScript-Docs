---
title: "Rituals"
description: "Set the Pyre Ritual recipe and control all stats. Dump the modifiable stats into `roots.log` by running `/roots rituals`."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/Rituals.java"
---

# Rituals (Roots 3)

## Description

Set the Pyre Ritual recipe and control all stats. Dump the modifiable stats into `roots.log` by running `/roots rituals`.

???+ Warning
    This compat is not fully documented. Some or all of its features are not present on the wiki. View the source code to gain an accurate understanding of the compat.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.roots.Rituals
mods.roots.rituals/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Rituals also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.rituals.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe. (Default `null`).

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 5. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy RitualBase`. Sets the ritual being modified. Requires not null. (Default `null`).

        ```groovy
        ritual(RitualBase)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.ritual.RitualBase$RitualRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.rituals.recipeBuilder()
            .ritual(ritual('ritual_healing_aura'))
            .input(item('minecraft:clay'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'),item('minecraft:gold_ingot'))
            .register()
        ```
