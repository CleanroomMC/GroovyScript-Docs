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

### Remove a recipe

```groovy
mods.thaumcraft.Crucible.removeByOutput(item('minecraft:gunpowder'))
```
