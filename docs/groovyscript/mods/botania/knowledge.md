---
title: "Lexicon Knowledge"
description: "Creates a new type of knowledge that Lexica Botania entries may be gated with. Can only be created."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/Knowledge.java"
---

# Lexicon Knowledge (Botania)

## Description

Creates a new type of knowledge that Lexica Botania entries may be gated with. Can only be created.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.Knowledge
mods.botania.knowledge/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds entries in the format `id`, `formatting`:

    ```groovy
    mods.botania.knowledge.add(String, TextFormatting)
    ```

- Adds entries in the format `id`, `formatting`, `autoUnlock`:

    ```groovy
    mods.botania.knowledge.add(String, TextFormatting, boolean)
    ```

???+ Example
    ```groovy
    mods.botania.knowledge.add('newType', TextFormatting.RED, true)
    ```

## Getting the value of entries

- Iterates through every entry in the registry:

    ```groovy
    mods.botania.knowledge.streamKnowledgeTypes()
    ```
