# Warp

## Adding Warp

```groovy
mods.thaumcraft.Warp.addWarp(ItemStack, int) // int must be non-negative
```

!!! example

    ```groovy
    mods.thaumcraft.Warp.addWarp(item('minecraft:pumpkin'), 3)
    ```

### Removing Warp

```groovy
mods.thaumcraft.Warp.removeWarp(ItemStack)
```

!!! example

    ```groovy
    mods.thaumcraft.Warp.removeWarp(item('thaumcraft:void_hoe'))
    ```