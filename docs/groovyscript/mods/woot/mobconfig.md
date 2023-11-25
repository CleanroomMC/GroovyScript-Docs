---
title: "Mob Config"
description: "Control the default values or mob-specific values for a large number of effects, a full list can be found at `ipsis.woot.configuration.EnumConfigKey`. A full list can be viewed on [Github](https://github.com/Ipsis/Woot/blob/55e88f5a15d66cc987e676d665d20f4afbe008b8/src/main/java/ipsis/woot/configuration/EnumConfigKey.java#L14)"
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/woot/MobConfig.java"
---

# Mob Config (Woot)

## Description

Control the default values or mob-specific values for a large number of effects, a full list can be found at `ipsis.woot.configuration.EnumConfigKey`. A full list can be viewed on [Github](https://github.com/Ipsis/Woot/blob/55e88f5a15d66cc987e676d665d20f4afbe008b8/src/main/java/ipsis/woot/configuration/EnumConfigKey.java#L14)

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.woot.MobConfig
mods.woot.mobconfig/*(1)!*/
mods.woot.mobConfig
mods.woot.mob_config
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds configuration to the default map:

    ```groovy
    mods.woot.mobconfig.add(EnumConfigKey, int)
    ```

- Adds configuration to the given entity:

    ```groovy
    mods.woot.mobconfig.add(String, EnumConfigKey, int)
    ```

- Adds configuration to the default map:

    ```groovy
    mods.woot.mobconfig.add(String, int)
    ```

- Adds configuration to the given entity:

    ```groovy
    mods.woot.mobconfig.add(String, String, int)
    ```

- Adds configuration to the given entity:

    ```groovy
    mods.woot.mobconfig.add(WootMobName, EnumConfigKey, int)
    ```

- Adds configuration to the given entity:

    ```groovy
    mods.woot.mobconfig.add(WootMobName, String, int)
    ```

???+ Example
    ```groovy
    mods.woot.mobconfig.add('spawn_ticks', 100)
    mods.woot.mobconfig.add('minecraft:zombie', 'spawn_ticks', 1)
    ```

## Removing Recipes

- Removes all configuration for the given entity:

    ```groovy
    mods.woot.mobconfig.remove(String)
    ```

- Removes configuration from the given entity for the given config:

    ```groovy
    mods.woot.mobconfig.remove(String, EnumConfigKey)
    ```

- Removes configuration from the given entity for the given config:

    ```groovy
    mods.woot.mobconfig.remove(String, String)
    ```

- Removes all configuration for the given entity:

    ```groovy
    mods.woot.mobconfig.remove(WootMobName)
    ```

- Removes configuration from the given entity for the given config:

    ```groovy
    mods.woot.mobconfig.remove(WootMobName, EnumConfigKey)
    ```

- Removes configuration from the given entity for the given config:

    ```groovy
    mods.woot.mobconfig.remove(WootMobName, String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.woot.mobconfig.removeAll()
    ```

???+ Example
    ```groovy
    mods.woot.mobconfig.remove('minecraft:wither_skeleton', 'spawn_units')
    mods.woot.mobconfig.remove('minecraft:wither')
    mods.woot.mobconfig.removeAll()
    ```
