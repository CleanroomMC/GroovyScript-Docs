# Smelting Bonus

Add or remove bonus outputs from the infernal furnace

### Adding a smelting bonus

```groovy
mods.thaumcraft.SmeltingBonus.recipeBuilder()
        .input(item('minecraft:cobblestone'))
        .output(item('minecraft:stone_button'))
        .chance(0.2F)
        .register()
```

Note: input also accepts oreDicts ``ore('oreIron')``. chance is the percentage chance of getting the given bonus ouput as a float [0-1] (defaults to 33%). 

### Removing a smelting bonus

```groovy
mods.thaumcraft.SmeltingBonus.removeByOutput(item('minecraft:gold_nugget'))
```
