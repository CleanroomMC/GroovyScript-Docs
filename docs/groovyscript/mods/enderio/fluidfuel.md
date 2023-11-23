---
title: "Fluid Fuel"
description: "Create a Fuel with a given power per tick and total burn time that produces power with a Coolant while in a Combustion Generator."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/enderio/FluidFuel.java"
---

# Fluid Fuel (Ender IO)

## Description

Create a Fuel with a given power per tick and total burn time that produces power with a Coolant while in a Combustion Generator.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.enderio.FluidFuel
mods.enderio.fluidfuel/*(1)!*/
mods.enderio.fluidFuel
mods.enderio.fluid_fuel
mods.enderio.CombustionFuel
mods.enderio.combustionfuel
mods.enderio.combustionFuel
mods.enderio.combustion_fuel
mods.eio.FluidFuel
mods.eio.fluidfuel
mods.eio.fluidFuel
mods.eio.fluid_fuel
mods.eio.CombustionFuel
mods.eio.combustionfuel
mods.eio.combustionFuel
mods.eio.combustion_fuel
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `fluid`, `rfPerCycle`, `totalBurnTime`:

    ```groovy
    mods.enderio.fluidfuel.addFuel(FluidStack, int, int)
    ```

- Adds recipes in the format `fluid`, `rfPerCycle`, `totalBurnTime`:

    ```groovy
    mods.enderio.fluidfuel.addFuel(Fluid, int, int)
    ```

???+ Example
    ```groovy
    mods.enderio.fluidfuel.addFuel(fluid('lava'), 500, 1000)
    ```

## Removing Recipes

- Removes recipes matching the target fluid:

    ```groovy
    mods.enderio.fluidfuel.remove(FluidStack)
    ```

- Removes recipes matching the target fluid:

    ```groovy
    mods.enderio.fluidfuel.remove(Fluid)
    ```

- Removes all registered recipes:

    ```groovy
    mods.enderio.fluidfuel.removeAll()
    ```

???+ Example
    ```groovy
    mods.enderio.fluidfuel.remove(fluid('fire_water'))
    mods.enderio.fluidfuel.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.enderio.fluidfuel.streamRecipes()
    ```
