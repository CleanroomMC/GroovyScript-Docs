# Dust Trigger (Salis Mundus)

The following builder is for creating new Dust Triggers. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

## Add a trigger

```groovy
mods.thaumcraft.DustTrigger.triggerBuilder()
```

Adding target: (requires exactly 1)

```groovy
.target(Block)
.target(String) // for oreDict triggers
```

Adding outputs: (requires exactly 1)

```groovy
.output(ItemStack)
```

Adding research requirement: (optional (default is ""))

```groovy
.researchKey(String/*(1)!*/)
```

1. The Research Key is the required research to craft the item, research is unlocked via the Thaumonomicon. Obtain a list of all research keys by doing `/tc research list`.

Register recipe: (returns nothing)

```groovy
.register()
```

!!! example

    ```groovy
    mods.thaumcraft.DustTrigger.triggerBuilder()
            .researchKey('UNLOCKALCHEMY@3')
            .target(block('minecraft:obsidian'))
            .output(item('minecraft:enchanting_table'))
            .register()
    ```

### Remove a trigger

```groovy
mods.thaumcraft.DustTrigger.removeByOutput(ItemStack)
```

!!! example

    ```groovy
    mods.thaumcraft.DustTrigger.removeByOutput(item('thaumcraft:arcane_workbench'))
    ```
