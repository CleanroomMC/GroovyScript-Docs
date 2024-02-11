---
title: "Spells"
description: "Controls the recipe for the given spell, the sound, all properties, the base cost, and each modifier's cost."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/Spells.java"
---

# Spells (Roots 3)

## Description

Controls the recipe for the given spell, the sound, all properties, the base cost, and each modifier's cost.

???+ Warning
    This compat is not fully documented. Some or all of its features are not present on the wiki. View the source code to gain an accurate understanding of the compat.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.roots.spells/*(1)!*/
mods.roots.Spells
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Spells also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.roots.spells.costBuilder()"
    - `#!groovy List<IModifierCost>`. Sets a list of all cost types used to construct a complex Cost object.

        ```groovy
        cost(CostType)
        cost(CostType, double)
        cost(CostType, Herb, double)
        cost(CostType, double, IModifierCore)
        cost(CostType, IModifierCore, double)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `java.util.Map<epicsquid.roots.modifiers.CostType, epicsquid.roots.modifiers.IModifierCost>`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.spells.costBuilder()
            .register()

        mods.roots.spells.costBuilder()
            .cost(cost('additional_cost'), herb('dewgonia'), 0.25)
            .register()

        mods.roots.spells.costBuilder()
            .cost(cost('additional_cost'), herb('spirit_herb'), 0.1)
            .cost(cost('all_cost_multiplier'), null, -0.125)
            .register()
        ```

???+ Abstract "mods.roots.spells.recipeBuilder()"
    - `#!groovy ResourceLocation`. Sets the Resource Location of the recipe.

        ```groovy
        name(String)
        name(ResourceLocation)
        ```

    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires greater than or equal to 1 and less than or equal to 5.

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy SpellBase`. Sets the spell being modified. Requires not null.

        ```groovy
        spell(SpellBase)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `epicsquid.roots.spell.SpellBase$SpellRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.roots.spells.recipeBuilder()
            .spell(spell('spell_fey_light'))
            .input(item('minecraft:clay'), item('minecraft:diamond'), item('minecraft:gold_ingot'))
            .register()
        ```
