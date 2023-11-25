---
title: "Excavator"
description: "Adds a Mineral Mix with the given name, weight, fail chance, ores, and allowed dimensions. A Mineral Mix can be mined by an Excavator Multiblock and scanned via a Core Sample Drill."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/immersiveengineering/Excavator.java"
---

# Excavator (Immersive Engineering)

## Description

Adds a Mineral Mix with the given name, weight, fail chance, ores, and allowed dimensions. A Mineral Mix can be mined by an Excavator Multiblock and scanned via a Core Sample Drill.

!!! Warning
    Reloading will not change chunks already 'discovered'

## Identifier

Refer to this via any of the following:

```groovy hl_lines="4"
mods.ie.Excavator
mods.ie.excavator
mods.immersiveengineering.Excavator
mods.immersiveengineering.excavator/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds entries in the format `name`, `mineralWeight`, `failChance`, `ores`, `chances`:

    ```groovy
    mods.immersiveengineering.excavator.add(String, int, float, String[], float[])
    ```


### Recipe Builder

Just like other recipe types, the Excavator also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.immersiveengineering.excavator.recipeBuilder()"
    - `#!groovy float`. Sets the chance that a given mining attempt with output nothing instead of an ore. Requires greater than or equal to 0 and less than or equal to 1.

        ```groovy
        fail(float)
        ```

    - `#!groovy String`. Sets the unique name of the vein.

        ```groovy
        name(String)
        ```

    - `#!groovy List<String>`. Sets the valid oredicts output. Requires exactly chances. (Default `null`).

        ```groovy
        ore(String, float)
        ore(OreDictIngredient, float)
        ```

    - `#!groovy int`. Sets the weight the Mineral Mix has to spawn in its allowed dimensions.

        ```groovy
        weight(int)
        ```

    - `#!groovy List<Float>`. Sets the chance a given block output will contain the corresponding entry in ores. Requires exactly ores. (Default `null`).

        ```groovy
        ore(String, float)
        ore(OreDictIngredient, float)
        ```

    - `#!groovy boolean`. Sets if the `dimensions` property indicates allowed dimensions (false) or blocked dimensions (true).

        ```groovy
        blacklist()
        blacklist(boolean)
        ```

    - `#!groovy List<Integer>`. Sets the list of dimension ids the vein can generate in (if `blacklist` is false) or are prevented from generating in (if `blacklist` is true). (Default `null`).

        ```groovy
        dimension(int)
        dimension(int...)
        dimension(Collection<Integer>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `blusunrize.immersiveengineering.api.tool.ExcavatorHandler$MineralMix`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.immersiveengineering.excavator.recipeBuilder()
            .name('demo')
            .weight(20000)
            .fail(0.5)
            .ore(ore('blockDiamond'), 50)
            .ore('blockGold', 10)
            .dimension(0, 1)
            .register()

        mods.immersiveengineering.excavator.recipeBuilder()
            .name('demo')
            .weight(2000)
            .fail(0.1)
            .ore(ore('blockDiamond'), 50)
            .dimension(-1, 1)
            .blacklist()
            .register()
        ```



## Removing Entries

- Removes the Mineral Mix entry with the given name:

    ```groovy
    mods.immersiveengineering.excavator.removeByMineral(String)
    ```

- Removes all Mineral Mix entries containing any of the given ores:

    ```groovy
    mods.immersiveengineering.excavator.removeByOres(OreDictIngredient...)
    ```

- Removes all Mineral Mix entries containing any of the given ores:

    ```groovy
    mods.immersiveengineering.excavator.removeByOres(String...)
    ```

- Removes all registered recipes:

    ```groovy
    mods.immersiveengineering.excavator.removeAll()
    ```

???+ Example
    ```groovy
    mods.immersiveengineering.excavator.removeByMineral('silt')
    mods.immersiveengineering.excavator.removeByOres(ore('oreAluminum'))
    mods.immersiveengineering.excavator.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.immersiveengineering.excavator.streamRecipes()
    ```
