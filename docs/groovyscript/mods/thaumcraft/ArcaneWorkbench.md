# Arcane Workbench

### Add a shapeless recipe

```groovy
mods.thaumcraft.ArcaneWorkbench.shapelessBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .input(item('minecraft:pumpkin'))
        .input(item('minecraft:stick'))
        .input(item('minecraft:stick'))
        .output(item('thaumcraft:void_hoe'))
        .vis(0)
        .register()
```

Note: input also accepts oreDicts ``.input(ore('cropPumpkin'))``. vis consumes a non-negative integer and refers to the amount of specified aspects required to execute the craft.

### Add a shaped recipe

```groovy
mods.thaumcraft.ArcaneWorkbench.shapedBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .output(item('minecraft:pumpkin'))
        .row('SS ')
        .row('   ')
        .row('   ')
        .key('S', item('minecraft:pumpkin_seeds'))
        .aspect(aspect('terra'))
        .vis(5)
        .register()
        
mods.thaumcraft.ArcaneWorkbench.shapedBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .output(item('minecraft:pumpkin'))
        .matrix('SS ',
                '   ',
                '   ')
        .key('S', item('minecraft:pumpkin_seeds'))
        .aspect(aspect('terra'))
        .vis(5)
        .register()
```

Note: key also accepts oreDicts ``.key('S', ore('cropPumpkin'))``. Both shaped recipe examples above are equivalent. vis consumes a non-negative integer and refers to the amount of specified aspects required to execute the craft.

### Remove a recipe

```groovy
mods.thaumcraft.Crucible.removeByOutput(item('minecraft:gunpowder'))
```

Note: removeByOutput also accepts oreDicts ``.removeByOutput(ore('cropPumpkin'))``
