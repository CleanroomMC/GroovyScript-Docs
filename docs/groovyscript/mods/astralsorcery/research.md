---
title: "Research Pages"
description: "Add custom Research Pages to the Astral Sorcery Book."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/Research.java"
---

# Research Pages (Astral Sorcery)

## Description

Add custom Research Pages to the Astral Sorcery Book.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="8"
mods.astral.Research
mods.astral.research
mods.astral_sorcery.Research
mods.astral_sorcery.research
mods.as.Research
mods.as.research
mods.astralsorcery.Research
mods.astralsorcery.research/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds a new node to the given category in the format `category`, `node`:

    ```groovy
    mods.astralsorcery.research.addNode(ResearchProgression, ResearchNode)
    ```

- Adds a connection between two nodes:

    ```groovy
    mods.astralsorcery.research.connectNodes(String, String)
    ```

- Moves the node with the given name to the x and y co-ords specified in the format `name`, `x`, `z`:

    ```groovy
    mods.astralsorcery.research.moveNode(String, int, int)
    ```

???+ Example
    ```groovy
    mods.astralsorcery.research.connectNodes('MY_TEST_RESEARCH2', 'ENHANCED_COLLECTOR')
    mods.astralsorcery.research.moveNode('SOOTYMARBLE', 5, 6)
    ```

### Recipe Builder

Just like other recipe types, the Research Pages also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.astralsorcery.research.researchBuilder()"
    - `#!groovy String`. Sets the unlocalized name of the node. Requires not null.

        ```groovy
        name(String)
        ```

    - `#!groovy ItemStack`. Sets the itemstack representing the node in the category. Requires not null.

        ```groovy
        icon(ItemStack)
        ```

    - `#!groovy ArrayList<IJournalPage>`. Sets the pages visible within the node.

        ```groovy
        page(IJournalPage)
        ```

    - `#!groovy ResearchProgression`. Sets the page the node is located on. Requires not null.

        ```groovy
        radiance()
        discovery()
        attunement()
        brilliance()
        exploration()
        constellation()
        ```

    - `#!groovy Point`. Sets the location of the node. Requires not null.

        ```groovy
        point(int, int)
        ```

    - `#!groovy ArrayList<ResearchNode>`. Sets what other nodes this node is connected to.

        ```groovy
        connectionFrom(String)
        connectionFrom(ResearchNode)
        ```

    - First validates the builder, outputting errors to the log file if the validation failed, then registers the builder.

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.research.researchBuilder()
            .name('MY_TEST_RESEARCH')
            .point(5,5)
            .icon(item('minecraft:pumpkin'))
            .discovery()
            .page(mods.astralsorcery.research.pageBuilder().textPage('GROOVYSCRIPT.RESEARCH.PAGE.TEST'))
            .page(mods.astralsorcery.research.pageBuilder().emptyPage())
            .connectionFrom('ALTAR1')
            .register()

        mods.astralsorcery.research.researchBuilder()
            .name('MY_TEST_RESEARCH2')
            .point(5,5)
            .icon(item('minecraft:pumpkin'))
            .constellation()
            .page(mods.astralsorcery.research.pageBuilder().textPage('GROOVYSCRIPT.RESEARCH.PAGE.TEST2'))
            .page(mods.astralsorcery.research.pageBuilder().constellationRecipePage(item('minecraft:pumpkin')))
            .register()
        ```



## Removing Entries

- Removes a connection between two nodes:

    ```groovy
    mods.astralsorcery.research.disconnectNodes(String, String)
    ```

- Removes the node with the given name:

    ```groovy
    mods.astralsorcery.research.removeNode(String)
    ```

???+ Example
    ```groovy
    mods.astralsorcery.research.disconnectNodes('MY_TEST_RESEARCH', 'ALTAR1')
    mods.astralsorcery.research.removeNode('CPAPER')
    ```

## Getting the value of entries

- Returns the node with the given name:

    ```groovy
    mods.astralsorcery.research.getNode(String)
    ```
