# Minecraft Furnace

## Adding Recipes

Unlike other recipe types, furnace smelting does not use a recipe builder.

```groovy
furnace.add(IIngredient input, ItemStack output) // applies a default exp of 0.1
furnace.add(IIngredient input, ItemStack output, float exp)
```

!!! example

    ```groovy
    // smelt 1 dirt to produce one cobblestone and 0.5 exp
    furnace.add(item('minecraft:dirt'), item('minecraft:cobblestone'), 0.5f)
    ```

## Removing Recipes

```groovy
furnace.removeByInput(ItemStack input)
```

!!! example

    ```groovy
    // removes all recipes that input iron ore
    furnace.removeByInput(item('minecraft:iron_ore'))
    ```
