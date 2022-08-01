# Mekanism Crusher

Add recipe 
```groovy
mods.mekanism.crusher.add(IIngredient input, ItemStack output)
```

!!! example
    ```
    mods.mekanism.crusher.add('<ore:ingotIron>', '<minecraft:nether_star>')
    ```

Remove recipe 
```groovy
mods.mekanism.crusher.remove(ItemStack output)
```