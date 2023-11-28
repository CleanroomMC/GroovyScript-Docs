---
title: "Dust Trigger"
description: "Converts a block in-world into an item, when interacting with it with Salis Mundus, potentially requiring a specific research to be completed."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/thaumcraft/DustTrigger.java"
---

# Dust Trigger (Thaumcraft)

## Description

Converts a block in-world into an item, when interacting with it with Salis Mundus, potentially requiring a specific research to be completed.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="10"
mods.thaum.DustTrigger
mods.thaum.dusttrigger
mods.thaum.dustTrigger
mods.thaum.dust_trigger
mods.tc.DustTrigger
mods.tc.dusttrigger
mods.tc.dustTrigger
mods.tc.dust_trigger
mods.thaumcraft.DustTrigger
mods.thaumcraft.dusttrigger/*(1)!*/
mods.thaumcraft.dustTrigger
mods.thaumcraft.dust_trigger
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Dust Trigger also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.thaumcraft.dusttrigger.triggerBuilder()"
    - `#!groovy String`. Sets the input as an ore. Requires either ore or target must be defined, but not both.

        ```groovy
        target(String)
        target(OreDictIngredient)
        ```

    - `#!groovy ItemStack`. Sets the output item, which will be dropped on the ground.

        ```groovy
        output(ItemStack)
        ```

    - `#!groovy Block`. Sets the input as a block. Requires either ore or target must be defined, but not both.

        ```groovy
        target(Block)
        ```

    - `#!groovy String`. Sets the research required to craft the recipe.

        ```groovy
        researchKey(String)
        ```

    - First validates the builder, outputting errors to the log file if the validation failed, then registers the builder.

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.thaumcraft.dusttrigger.triggerBuilder()
            .researchKey('UNLOCKALCHEMY@3')
            .target(block('minecraft:obsidian'))
            .output(item('minecraft:enchanting_table'))
            .register()

        mods.thaumcraft.dusttrigger.triggerBuilder()
            .researchKey('UNLOCKALCHEMY@3')
            .target(ore('cropPumpkin'))
            .output(item('minecraft:lit_pumpkin'))
            .register()
        ```



## Removing Recipes

- Removes all recipes that match the given output:

    ```groovy
    mods.thaumcraft.dusttrigger.removeByOutput(ItemStack)
    ```

???+ Example
    ```groovy
    mods.thaumcraft.dusttrigger.removeByOutput(item('thaumcraft:arcane_workbench'))
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.thaumcraft.dusttrigger.streamRecipes()
    ```
