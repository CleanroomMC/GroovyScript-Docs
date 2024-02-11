---
title: "Lexicon Entry"
description: "Entry creates a new entry in a given category."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/Lexicon.java"
---

# Lexicon Entry (Botania)

## Description

Entry creates a new entry in a given category.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.botania.entry/*(1)!*/
mods.botania.Entry
```

1. This identifier will be used as the default for examples on this page

## Editing Values

- Sets the Knowledge type of the given entry in the format `entry`, `type`:

    ```groovy
    mods.botania.entry.setKnowledgeType(String, KnowledgeType)
    ```

- Sets the Knowledge type of the given entry in the format `entry`, `type`:

    ```groovy
    mods.botania.entry.setKnowledgeType(String, String)
    ```


## Adding Entries

- Adds a new Lexica Botania entry to the given Category in the format `name`, `category`:

    ```groovy
    mods.botania.entry.add(String, LexiconCategory)
    ```

- Adds a new Lexica Botania entry to the given Category in the format `name`, `category`:

    ```groovy
    mods.botania.entry.add(String, String)
    ```


### Recipe Builder

Just like other recipe types, the Lexicon Entry also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.botania.entry.entryBuilder()"
    - `#!groovy ItemStack`. Sets the default icon of the Entry. (Default `ItemStack.EMPTY`).

        ```groovy
        icon(IIngredient)
        ```

    - `#!groovy String`. Sets the unlocalized name of the Entry. Requires not null.

        ```groovy
        name(String)
        ```

    - `#!groovy KnowledgeType`. Sets the Knowledge Type required to view the Entry. Also determines the color. (Default `BotaniaAPI.basicKnowledge`).

        ```groovy
        knowledgeType(KnowledgeType)
        ```

    - `#!groovy List<LexiconPage>`. Sets the Pages attached to the Entry. Requires greater than or equal to 1.

        ```groovy
        page(LexiconPage)
        page(LexiconPage...)
        page(Collection<LexiconPage>)
        ```

    - `#!groovy LexiconCategory`. Sets the Category the Entry is attached to. Requires not null.

        ```groovy
        category(String)
        category(LexiconCategory)
        ```

    - `#!groovy boolean`. Sets if the Entry always appears at the top of the list in a Category. (Default `false`).

        ```groovy
        isPriority()
        ```

    - `#!groovy List<ItemStack>`. Sets additional items displayed as if they were crafted by a page within the Entry.

        ```groovy
        extraRecipe(IIngredient)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `vazkii.botania.api.lexicon.LexiconEntry`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.botania.entry.entryBuilder()
            .name('test_entry')
            .icon(ore('blockIron'))
            .category('test')
            .knowledgeType(newType)
            .page(mods.botania.lexicon.page.createTextPage('groovy.exampleTextPage'))
            .register()
        ```



## Removing Entries

- Removes the given Entry from the Lexica Botania:

    ```groovy
    mods.botania.entry.remove(String)
    ```

- Removes all entries in the given Lexica Botania Category:

    ```groovy
    mods.botania.entry.removeByCategory(LexiconCategory)
    ```

- Removes all entries in the given Lexica Botania Category:

    ```groovy
    mods.botania.entry.removeByCategory(String)
    ```

- Removes the given Entry from the Lexica Botania:

    ```groovy
    mods.botania.entry.removeEntry(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.entry.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.entry.remove('botania.entry.flowers')
    mods.botania.entry.removeEntry('botania.entry.apothecary')
    mods.botania.entry.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.entry.streamEntries()
    ```
