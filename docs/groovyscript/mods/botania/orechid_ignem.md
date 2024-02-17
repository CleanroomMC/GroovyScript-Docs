---
title: "Orechid Ignem"
description: "Converts netherrack blocks into one of a few ore blocks at the cost of mana."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/OrechidIgnem.java"
---

# Orechid Ignem (Botania)

## Description

Converts netherrack blocks into one of a few ore blocks at the cost of mana.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.botania.orechid_ignem/*(1)!*/
mods.botania.orechidignem
mods.botania.orechidIgnem
mods.botania.OrechidIgnem
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `output`, `weight`:

    ```groovy
    mods.botania.orechid_ignem.add(OreDictIngredient, int)
    ```

- Adds recipes in the format `output`, `weight`:

    ```groovy
    mods.botania.orechid_ignem.add(String, int)
    ```

???+ Example
    ```groovy
    mods.botania.orechid_ignem.add(ore('oreEmerald'), 1350)
    mods.botania.orechid_ignem.add(ore('blockGold'), 1800)
    ```

## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.orechid_ignem.removeByOutput(OreDictIngredient)
    ```

- Removes all recipes that match the given output:

    ```groovy
    mods.botania.orechid_ignem.removeByOutput(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.orechid_ignem.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.orechid_ignem.removeByOutput(ore('oreEmerald'))
    mods.botania.orechid_ignem.removeByOutput(ore('oreQuartz'))
    mods.botania.orechid_ignem.removeByOutput('oreQuartz')
    mods.botania.orechid_ignem.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.orechid_ignem.streamRecipes()
    ```
