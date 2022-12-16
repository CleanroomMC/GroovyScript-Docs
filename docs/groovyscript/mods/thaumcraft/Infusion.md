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

Note: input and mainInput also accept oreDicts ``.catalyst(ore('cropPumpkin'))``. input refers to the items placed on pedestal's around the multiblock. mainInput refers to the item placed in the center underneath the runic matrix block. Instability must be a non-negative integer.

### Remove a recipe

```groovy
mods.thaumcraft.InfusionCrafting.removeByOutput(item('thaumcraft:crystal_terra'))
```
