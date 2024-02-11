---
title: "Constellation"
description: "Create a custom Constellation."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/astralsorcery/Constellation.java"
---

# Constellation (Astral Sorcery)

## Description

Create a custom Constellation.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="3"
mods.astral_sorcery.constellation
mods.astral_sorcery.Constellation
mods.astralsorcery.constellation/*(1)!*/
mods.astralsorcery.Constellation
mods.astral.constellation
mods.astral.Constellation
mods.as.constellation
mods.as.Constellation
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds to the constellations signature items, which control the Constellation Paper and Mantle of Stars recipes. Only the first 4 will be used.:

    ```groovy
    mods.astralsorcery.constellation.addSignatureItem(IConstellation, Collection<IIngredient>)
    ```

- Adds to the constellations signature items, which control the Constellation Paper and Mantle of Stars recipes. Only the first 4 will be used.:

    ```groovy
    mods.astralsorcery.constellation.addSignatureItem(IConstellation, IIngredient)
    ```

- Adds to the constellations signature items, which control the Constellation Paper and Mantle of Stars recipes. Only the first 4 will be used.:

    ```groovy
    mods.astralsorcery.constellation.addSignatureItem(IConstellation, IIngredient...)
    ```


### Recipe Builder

Just like other recipe types, the Constellation also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.astralsorcery.constellation.constellationBuilder()"
    - `#!groovy String`. Sets the name of the Constellation. Requires not null.

        ```groovy
        name(String)
        ```

    - `#!groovy Constellation.ConstellationBuilder.Type`. Sets the type of Constellation.

        ```groovy
        weak()
        major()
        minor()
        ```

    - `#!groovy Color`. Sets the color of the Constellation. (Default `Major: #2843CC, Weak: #432CB0, Minor: #5D197F`).

        ```groovy
        color(int)
        ```

    - `#!groovy ArrayList<MoonPhase>`. Sets what phase of the moon the Constellation appears in. Only applies if the Constellation type is Minor. Requires greater than or equal to 0.

        ```groovy
        phase(MoonPhase)
        phase(MoonPhase...)
        phase(Collection<MoonPhase>)
        ```

    - `#!groovy ArrayList<Constellation.Point2PointConnection>`. Sets the stars and connections between stars that map the Constellation. Requires greater than or equal to 0.

        ```groovy
        connection(int, int, int, int)
        ```

    - First validates the builder, outputting errors to the log file if the validation failed, then registers the builder.

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.constellation.constellationBuilder()
            .major()
            .name('square')
            .color(0xE01903)
            .connection(12, 2, 2, 2)
            .connection(12, 12, 12, 2)
            .connection(2, 12, 12, 12)
            .connection(2, 2, 2, 12)
            .register()

        mods.astralsorcery.constellation.constellationBuilder()
            .minor()
            .name('slow')
            .connection(10, 5, 5, 5)
            .connection(5, 10, 5, 5)
            .connection(3, 3, 3, 3)
            .phase(MoonPhase.FULL)
            .register()
        ```

???+ Abstract "mods.astralsorcery.constellation.constellationMapEffectBuilder()"
    - `#!groovy List<ConstellationMapEffectRegistry.PotionMapEffect>`. Sets the potion effects and strength available via the Stellar Refraction Table. Requires greater than or equal to 0.

        ```groovy
        potionEffect(Potion, int, int)
        ```

    - `#!groovy IConstellation`. Sets the Constellation being modified. Requires not null.

        ```groovy
        constellation(IConstellation)
        ```

    - `#!groovy List<ConstellationMapEffectRegistry.EnchantmentMapEffect>`. Sets the enchantments and enchantment levels available via the Stellar Refraction Table. Requires greater than or equal to 0.

        ```groovy
        enchantmentEffect(Enchantment, int, int)
        ```

    - First validates the builder, outputting errors to the log file if the validation failed, then registers the builder.

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.constellation.constellationMapEffectBuilder()
            .constellation(constellation('square'))
            .enchantmentEffect(enchantment('minecraft:luck_of_the_sea'), 1, 3)
            .potionEffect(potion('minecraft:luck'), 1, 2)
            .register()
        ```

???+ Abstract "mods.astralsorcery.constellation.signatureItems()"
    - `#!groovy ArrayList<IIngredient>`. Sets the signature items of the Constellation.

        ```groovy
        addItem(IIngredient)
        ```

    - `#!groovy boolean`. Sets if the default signature items of the Constellation will be removed before adding new ones. (Default `false`).

        ```groovy
        stripItems()
        ```

    - `#!groovy IConstellation`. Sets the Constellation being modified. Requires not null.

        ```groovy
        constellation(IConstellation)
        ```

    - First validates the builder, outputting errors to the log file if the validation failed, then registers the builder.

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.astralsorcery.constellation.signatureItems()
            .constellation(constellation('square'))
            .addItem(ore('gemDiamond'))
            .addItem(item('minecraft:water_bucket'))
            .addItem(item('minecraft:rabbit_foot'))
            .addItem(item('minecraft:fish'))
            .register()
        ```



## Removing Entries

- Removes the given Constellation and all associated attributes:

    ```groovy
    mods.astralsorcery.constellation.remove(IConstellation)
    ```

- Removes a Constellation's potion and enchantment effects applied via the Stellar Refraction Table:

    ```groovy
    mods.astralsorcery.constellation.removeConstellationMapEffect(IConstellation)
    ```

- Removes a Constellation's signature items, to be re-added via `addSignatureItem`:

    ```groovy
    mods.astralsorcery.constellation.removeSignatureItems(IConstellation)
    ```

- Removes all registered recipes:

    ```groovy
    mods.astralsorcery.constellation.removeAll()
    ```

- Removes all potion and enchantment effects applied via the Stellar Refraction Table for all Constellations:

    ```groovy
    mods.astralsorcery.constellation.removeAllConstellationMapEffect()
    ```

- Removes all signature items for all Constellations, to be re-added via `addSignatureItem`:

    ```groovy
    mods.astralsorcery.constellation.removeAllSignatureItems()
    ```

???+ Example
    ```groovy
    mods.astralsorcery.constellation.remove(constellation('bootes'))
    mods.astralsorcery.constellation.removeConstellationMapEffect(constellation('discidia'))
    mods.astralsorcery.constellation.removeSignatureItems(constellation('discidia'))
    mods.astralsorcery.constellation.removeAll()
    mods.astralsorcery.constellation.removeAllConstellationMapEffect()
    mods.astralsorcery.constellation.removeAllSignatureItems()
    ```

## Getting the value of entries

- Iterates through every Constellation registered, with the ability to call remove on any element to remove it from the game:

    ```groovy
    mods.astralsorcery.constellation.streamConstellations()
    ```
