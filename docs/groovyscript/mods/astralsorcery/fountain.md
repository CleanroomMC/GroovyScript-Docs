---
title: "Fountain"
description: "Adds virtual aquifers that can be accessed via the Evershifting Fountain's Necromantic Prime."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/Fountain.java"
---

# Fountain (Astral Sorcery)

## Description

Adds virtual aquifers that can be accessed via the Evershifting Fountain's Necromantic Prime.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="8"
mods.astral.Fountain
mods.astral.fountain
mods.astral_sorcery.Fountain
mods.astral_sorcery.fountain
mods.as.Fountain
mods.as.fountain
mods.astralsorcery.Fountain
mods.astralsorcery.fountain/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `fluid`, `rarity`, `guaranteedAmt`, `addRand`:

    ```groovy
    mods.astralsorcery.fountain.add(Fluid, int, int, int)
    ```

- Adds an existing `FluidRarityEntry` to the registry:

    ```groovy
    mods.astralsorcery.fountain.add(FluidRarityRegistry.FluidRarityEntry)
    ```

- Adds recipes in the format `fluid`, `rarity`, `guaranteedAmt`, `addRand`:

    ```groovy
    mods.astralsorcery.fountain.add(FluidStack, int, int, int)
    ```


### Recipe Builder

Just like other recipe types, the Fountain also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.astralsorcery.fountain.chanceHelper()"
    - `#!groovy Fluid`. Sets the fluid being generated. Requires not null. (Default `null`).

        ```groovy
        fluid(Fluid)
        fluid(FluidStack)
        ```

    - `#!groovy int`. Sets the frequency the fluid generates in a chunk. Requires greater than or equal to 0.

        ```groovy
        rarity(int)
        ```

    - `#!groovy int`. Sets the maximum amount of additional fluid that can be generated in a chunk. Requires greater than or equal to 0.

        ```groovy
        variance(int)
        ```

    - `#!groovy int`. Sets the minimum amount of fluid in a chunk. Requires greater than or equal to 0.

        ```groovy
        minimumAmount(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `hellfirepvp.astralsorcery.common.base.FluidRarityRegistry$FluidRarityEntry`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.fountain.chanceHelper()
            .fluid(fluid('astralsorcery.liquidstarlight'))
            .rarity(10000000)
            .minimumAmount(4000000)
            .variance(1000000)
            .register()
        ```



## Removing Recipes

- Removes an entry matching the given `FluidStack`:

    ```groovy
    mods.astralsorcery.fountain.remove(FluidStack)
    ```

- Removes an entry matching the given `Fluid`:

    ```groovy
    mods.astralsorcery.fountain.remove(Fluid)
    ```

- Removes an existing `FluidRarityEntry`:

    ```groovy
    mods.astralsorcery.fountain.remove(FluidRarityRegistry.FluidRarityEntry)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.fountain.removeAll()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.fountain.remove(fluid('lava'))
    mods.astralsorcery.fountain.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.astralsorcery.fountain.streamRecipes()
    ```
