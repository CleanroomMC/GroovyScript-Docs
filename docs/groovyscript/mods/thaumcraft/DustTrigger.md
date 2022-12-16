# Dust Trigger (Salis Mundus)

### Add a trigger

```groovy
mods.thaumcraft.DustTrigger.triggerBuilder()
        .researchKey('UNLOCKALCHEMY@3')
        .target(block('minecraft:obsidian'))
        .output(item('minecraft:enchanting_table'))
        .register()
```

Note: target also accepts oreDicts ``.target(ore('cropPumpkin'))``

### Remove a trigger

```groovy
mods.thaumcraft.DustTrigger.removeByOutput(item('thaumcraft:arcane_workbench'))
```
