# EnderIO Combustion Generator

GroovyScript allows you to add and remove custom fuels and coolants for the Combustion Generator.

## Adding fuels

```groovy
mods.enderio.CombustionGen.addFuel(FluidStack fuel, int rfPerCycle, int burnTime)
```

!!! example

    ```groovy
    mods.enderio.CombustionGen.addFuel(fluid('water'), 100, 100)
    ```

## Removing fuels

```groovy
mods.enderio.CombustionGen.removeFuel(FluidStack fuel)
```

!!! example

    ```groovy
    mods.enderio.CombustionGen.removeFuel(fluid('rocket_fuel'))
    ```

## Adding coolants

```groovy
mods.enderio.CombustionGen.addCoolant(FluidStack fuel, float degreesCoolingPerMb)
```

!!! example

    ```groovy
    mods.enderio.CombustionGen.addCoolant(fluid('lava'), 20f)
    ```

## Removing coolants

```groovy
mods.enderio.CombustionGen.removeCoolant(FluidStack fuel)
```

!!! example

    ```groovy
    mods.enderio.CombustionGen.removeCoolant(fluid('ender_distillation'))
    ```
