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

```groovy hl_lines="1"
mods.enderio.fluid_fuel/*(1)!*/
mods.enderio.fluidfuel
mods.enderio.fluidFuel
mods.enderio.FluidFuel
mods.enderio.combustion_fuel
mods.enderio.combustionfuel
mods.enderio.combustionFuel
mods.enderio.CombustionFuel
mods.eio.fluid_fuel
mods.eio.fluidfuel
mods.eio.fluidFuel
mods.eio.FluidFuel
mods.eio.combustion_fuel
mods.eio.combustionfuel
mods.eio.combustionFuel
mods.eio.CombustionFuel
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

- Adds recipes in the format `fluid`, `rfPerCycle`, `totalBurnTime`:

    ```groovy
    mods.enderio.fluid_fuel.addFuel(Fluid, int, int)
    ```

- Adds recipes in the format `fluid`, `rfPerCycle`, `totalBurnTime`:

    ```groovy
    mods.enderio.fluid_fuel.addFuel(FluidStack, int, int)
    ```

???+ Example
    ```groovy
    mods.enderio.fluid_fuel.addFuel(fluid('lava'), 500, 1000)
    ```

## Removing Recipes

- Removes recipes matching the target fluid:

    ```groovy
    mods.enderio.fluid_fuel.remove(Fluid)
    ```

- Removes recipes matching the target fluid:

    ```groovy
    mods.enderio.fluid_fuel.remove(FluidStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.enderio.fluid_fuel.removeAll()
    ```

???+ Example
    ```groovy
    mods.enderio.fluid_fuel.remove(fluid('fire_water'))
    mods.enderio.fluid_fuel.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.enderio.fluid_fuel.streamRecipes()
    ```
