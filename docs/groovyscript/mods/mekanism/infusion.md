---
title: "Infusion"
description: "Add new infusion types and itemstacks to those types."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/Infusion.java"
---

# Infusion (Mekanism)

## Description

Add new infusion types and itemstacks to those types.

!!! Danger ""
    To register a texture to be used by an Infusion Type, you have to add the following event listener to a PreInit file. `event_manager.listen { TextureStitchEvent.Pre event -> event.getMap().registerSprite(resource('placeholdername:blocks/example')) }`, where 'assets/placeholdername/textures/blocks/example.png' is the location of the desired texture.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.mekanism.Infusion
mods.mekanism.infusion/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Creates an Infusion Type with the given name and texture:

    ```groovy
    mods.mekanism.infusion.addType(String, ResourceLocation)
    ```

- Creates an Infusion Type with the given name and texture:

    ```groovy
    mods.mekanism.infusion.addType(String, String)
    ```

- Adds IIngredients to the provided Infusion Type:

    ```groovy
    mods.mekanism.infusion.add(InfuseType, int, Collection<IIngredient>)
    ```

- Adds IIngredients to the provided Infusion Type:

    ```groovy
    mods.mekanism.infusion.add(InfuseType, int, IIngredient...)
    ```

- Adds IIngredients to the provided Infusion Type:

    ```groovy
    mods.mekanism.infusion.add(InfuseType, int, ItemStack)
    ```

- Adds IIngredients to the provided Infusion Type:

    ```groovy
    mods.mekanism.infusion.add(String, int, Collection<IIngredient>)
    ```

- Adds IIngredients to the provided Infusion Type:

    ```groovy
    mods.mekanism.infusion.add(String, int, IIngredient...)
    ```

???+ Example
    ```groovy
    mods.mekanism.infusion.addType('groovy_example', resource('placeholdername:blocks/example'))
    mods.mekanism.infusion.add(infusion('diamond'), 100, item('minecraft:clay'))
    mods.mekanism.infusion.add(infusion('carbon'), 100, item('minecraft:gold_ingot'))
    mods.mekanism.infusion.add('groovy_example', 10, item('minecraft:ice'))
    mods.mekanism.infusion.add('groovy_example', 20, item('minecraft:packed_ice'))
    ```

## Removing Entries

- Removes IIngredients from any Infusion Type:

    ```groovy
    mods.mekanism.infusion.remove(Collection<IIngredient>)
    ```

- Removes IIngredients from any Infusion Type:

    ```groovy
    mods.mekanism.infusion.remove(IIngredient)
    ```

- Removes IIngredients from any Infusion Type:

    ```groovy
    mods.mekanism.infusion.remove(IIngredient...)
    ```

- Removes any Infusion Type that matches the given type:

    ```groovy
    mods.mekanism.infusion.removeByType(InfuseType)
    ```

- Removes any Infusion Type that matches the given type:

    ```groovy
    mods.mekanism.infusion.removeByType(String)
    ```

- Removes an Infusion Type and all corresponding items:

    ```groovy
    mods.mekanism.infusion.removeType(String)
    ```

- Removes all Infusion Types:

    ```groovy
    mods.mekanism.infusion.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.infusion.remove(ore('dustDiamond'))
    mods.mekanism.infusion.removeByType(infusion('carbon'))
    mods.mekanism.infusion.removeByType(infusion('diamond'))
    mods.mekanism.infusion.removeAll()
    ```
