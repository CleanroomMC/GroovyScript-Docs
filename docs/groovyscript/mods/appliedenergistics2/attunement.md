---
title: "P2P Attunement"
description: "Controls using specific items, any items from a mod, or any items with a Capability to convert a P2P into a specific tunnel type."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/appliedenergistics2/Attunement.java"
---

# P2P Attunement (Applied Energistics 2)

## Description

Controls using specific items, any items from a mod, or any items with a Capability to convert a P2P into a specific tunnel type.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="3"
mods.ae2.attunement
mods.ae2.Attunement
mods.appliedenergistics2.attunement/*(1)!*/
mods.appliedenergistics2.Attunement
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds tunnel attunement for all items with the given capability in the format `capability`, `tunnel`:

    ```groovy
    mods.appliedenergistics2.attunement.add(Capability<?>, TunnelType)
    ```

- Adds tunnel attunement for the given item in the format `item`, `tunnel`:

    ```groovy
    mods.appliedenergistics2.attunement.add(ItemStack, TunnelType)
    ```

- Adds tunnel attunement for all items in the given mod in the format `mod`, `tunnel`:

    ```groovy
    mods.appliedenergistics2.attunement.add(String, TunnelType)
    ```

???+ Example
    ```groovy
    mods.appliedenergistics2.attunement.add(Capabilities.FORGE_ENERGY, tunnel('item'))
    mods.appliedenergistics2.attunement.add(item('minecraft:clay'), tunnel('item'))
    mods.appliedenergistics2.attunement.add('thermaldynamics', tunnel('redstone'))
    ```

## Removing Recipes

- Removes tunnel attunement for the given capability in the format `capability`, `tunnel`:

    ```groovy
    mods.appliedenergistics2.attunement.remove(Capability<?>, TunnelType)
    ```

- Removes tunnel attunement for the given item in the format `item`, `tunnel`:

    ```groovy
    mods.appliedenergistics2.attunement.remove(ItemStack, TunnelType)
    ```

- Removes tunnel attunement for the given mod in the format `mod`, `tunnel`:

    ```groovy
    mods.appliedenergistics2.attunement.remove(String, TunnelType)
    ```

- Removes the given Capability from creating any tunnel:

    ```groovy
    mods.appliedenergistics2.attunement.removeByCapability(Capability<?>)
    ```

- Removes the item from creating any tunnel:

    ```groovy
    mods.appliedenergistics2.attunement.removeByItem(ItemStack)
    ```

- Removes the modid from creating any tunnel:

    ```groovy
    mods.appliedenergistics2.attunement.removeByMod(String)
    ```

- Remove all ways to create the given tunnel:

    ```groovy
    mods.appliedenergistics2.attunement.removeByTunnel(TunnelType)
    ```

- Removes all registered recipes:

    ```groovy
    mods.appliedenergistics2.attunement.removeAll()
    ```

???+ Example
    ```groovy
    mods.appliedenergistics2.attunement.remove(Capabilities.FORGE_ENERGY, tunnel('fe_power'))
    mods.appliedenergistics2.attunement.remove(item('minecraft:lever'), tunnel('redstone'))
    mods.appliedenergistics2.attunement.remove('thermaldynamics', tunnel('fe_power'))
    mods.appliedenergistics2.attunement.removeByTunnel(tunnel('item'))
    mods.appliedenergistics2.attunement.removeAll()
    ```
