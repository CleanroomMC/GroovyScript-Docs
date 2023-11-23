---
title: "Modifiers"
description: "Controls what spell modifiers are enabled and can be used."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/roots/Modifiers.java"
---

# Modifiers (Roots 3)

## Description

Controls what spell modifiers are enabled and can be used.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.roots.Modifiers
mods.roots.modifiers/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Enable any disabled modifiers with the given string as a resource location, defaulting to a namespace of `roots` if not provided:

    ```groovy
    mods.roots.modifiers.enable(String)
    ```

- Enable any disabled modifiers with the given resource location:

    ```groovy
    mods.roots.modifiers.enable(ResourceLocation)
    ```

- Enable the disabled modifier:

    ```groovy
    mods.roots.modifiers.enable(Modifier)
    ```

- Enable all disabled modifiers for the given spell:

    ```groovy
    mods.roots.modifiers.enable(SpellBase)
    ```

- Enable all disabled modifiers:

    ```groovy
    mods.roots.modifiers.enableAll()
    ```

???+ Example
    ```groovy
    mods.roots.modifiers.enable('extended_geas')
    mods.roots.modifiers.enable(resource('roots:animal_savior'))
    mods.roots.modifiers.enable(modifier('roots:weakened_response'))
    mods.roots.modifiers.enableAll()
    ```

## Removing Entries

- Disable any enabled modifiers with the given string as a resource location, defaulting to a namespace of `roots` if not provided:

    ```groovy
    mods.roots.modifiers.disable(String)
    ```

- Disable any enabled modifiers with the given resource location:

    ```groovy
    mods.roots.modifiers.disable(ResourceLocation)
    ```

- Disable the enabled modifier:

    ```groovy
    mods.roots.modifiers.disable(Modifier)
    ```

- Disable all enabled modifiers for the given spell:

    ```groovy
    mods.roots.modifiers.disable(SpellBase)
    ```

- Disable all enabled modifiers:

    ```groovy
    mods.roots.modifiers.disableAll()
    ```

???+ Example
    ```groovy
    mods.roots.modifiers.disable(spell('spell_geas'))
    mods.roots.modifiers.disableAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.roots.modifiers.streamRecipes()
    ```
