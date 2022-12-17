# Infusion Crafting

### Add a recipe

```groovy
mods.thaumcraft.InfusionCrafting.recipeBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .mainInput(item('minecraft:gunpowder'))
        .output(item('minecraft:gold_ingot'))
        .aspect(aspect('terra') * 20)
        .aspect(aspect('ignis') * 30)
        .input(crystal('aer'))
        .input(crystal('ignis'))
        .input(crystal('aqua'))
        .input(crystal('terra'))
        .input(crystal('ordo'))
        .instability(10)
        .register()
```

### Remove a recipe

```groovy
mods.thaumcraft.InfusionCrafting.removeByOutput(item('thaumcraft:crystal_terra'))
```
