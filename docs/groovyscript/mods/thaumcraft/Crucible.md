# Crucible

### Add a recipe

```groovy
mods.thaumcraft.Crucible.recipeBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .catalyst(item('minecraft:rotten_flesh'))
        .output(item('minecraft:gold_ingot'))
        .aspect(aspect('metallum') * 10)
        .register()
```

Note: catalyst also accepts oreDicts ``.catalyst(ore('cropPumpkin'))``

### Remove a recipe

```groovy
mods.thaumcraft.Crucible.removeByOutput(item('minecraft:gunpowder'))
```

Note: removeByOutput also accepts oreDicts ``.removeByOutput(ore('cropPumpkin'))``