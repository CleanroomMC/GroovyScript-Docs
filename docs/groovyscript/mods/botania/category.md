---
title: "Lexicon Category"
description: "Category creates a new entry on the front page of the Lexica Botania."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/Lexicon.java"
---

# Lexicon Category (Botania)

## Description

Category creates a new entry on the front page of the Lexica Botania.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.Category
mods.botania.category/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds a Category to the Lexica Botania in the format `name`, `icon` and a priority of 5:

    ```groovy
    mods.botania.category.add(String, ResourceLocation)
    ```

- Adds a Category to the Lexica Botania in the format `name`, `icon`, `priority`:

    ```groovy
    mods.botania.category.add(String, ResourceLocation, int)
    ```

???+ Example
    ```groovy
    mods.botania.category.add('test', resource('minecraft:textures/items/apple.png'))
    mods.botania.category.add('first', resource('minecraft:textures/items/clay_ball.png'), 100)
    ```

## Removing Entries

- Removes a Category matching the given name:

    ```groovy
    mods.botania.category.remove(String)
    ```

- Removes a Category matching the given name:

    ```groovy
    mods.botania.category.removeCategory(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.category.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.category.remove('botania.category.alfhomancy')
    mods.botania.category.removeCategory('botania.category.misc')
    mods.botania.category.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.category.streamCategories()
    ```
