---
title: "Solar Neutron Activator"
description: "Converts an input gasstack into an output gasstack while exposed to the sun."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/mekanism/SolarNeutronActivator.java"
---

# Solar Neutron Activator (Mekanism)

## Description

Converts an input gasstack into an output gasstack while exposed to the sun.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="1"
mods.mekanism.solar_neutron_activator/*(1)!*/
mods.mekanism.solarneutronactivator
mods.mekanism.solarNeutronActivator
mods.mekanism.SolarNeutronActivator
mods.mekanism.SNA
mods.mekanism.sna
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `input`, `output`:

    ```groovy
    mods.mekanism.solar_neutron_activator.add(GasStack, GasStack)
    ```

???+ Example
    ```groovy
    mods.mekanism.solar_neutron_activator.add(gas('water'), gas('hydrogen'))
    ```

### Recipe Builder

Just like other recipe types, the Solar Neutron Activator also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.mekanism.solar_neutron_activator.recipeBuilder()"
    - `#!groovy GasStackList`. Sets the gas inputs of the recipe. Requires exactly 1.

        ```groovy
        gasInput(GasStack)
        gasInput(GasStack...)
        gasInput(Collection<GasStack>)
        ```

    - `#!groovy GasStackList`. Sets the gas outputs of the recipe. Requires exactly 1.

        ```groovy
        gasOutput(GasStack)
        gasOutput(GasStack...)
        gasOutput(Collection<GasStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `mekanism.common.recipe.machines.SolarNeutronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.mekanism.solar_neutron_activator.recipeBuilder()
            .gasInput(gas('water'))
            .gasOutput(gas('hydrogen'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given input:

    ```groovy
    mods.mekanism.solar_neutron_activator.removeByInput(GasStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.mekanism.solar_neutron_activator.removeAll()
    ```

???+ Example
    ```groovy
    mods.mekanism.solar_neutron_activator.removeByInput(gas('lithium'))
    mods.mekanism.solar_neutron_activator.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.mekanism.solar_neutron_activator.streamRecipes()
    ```
