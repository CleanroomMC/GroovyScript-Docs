---
title: "Cauldron"
description: "Converts up to 1 itemstack and up to 1 fluid into up to 1 itemstack or up to 1 fluid, with a boiling boolean and variable amount of fluid consumed or produced."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/inspirations/Cauldron.java"
---

# Cauldron (Inspirations)

## Description

Converts up to 1 itemstack and up to 1 fluid into up to 1 itemstack or up to 1 fluid, with a boiling boolean and variable amount of fluid consumed or produced.

???+ Note
    Cauldrons have a cap of either 3 or 4 levels, depending on the config.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.inspirations.Cauldron
mods.inspirations.cauldron/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Recipes

### Recipe Builder

Just like other recipe types, the Cauldron also uses a recipe builder.

Don't know what a builder is? Check [the builder info page](../../../groovy/builder.md) out.

???+ Abstract "mods.inspirations.cauldron.recipeBuilder()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        fluidOutput(FluidStack)
        fluidOutput(FluidStack...)
        fluidOutput(Collection<FluidStack>)
        ```

    - `#!groovy EnumDyeColor`. Sets the dye color fluid required for the input. Requires not null. (Default `null`).

        ```groovy
        dye(String)
        dye(EnumDyeColor)
        ```

    - `#!groovy Cauldron.RecipeBuilder.RecipeType`. Sets what type of recipe is being processed. (Default `null`).

        ```groovy
        dye()
        mix()
        fill()
        type(String)
        type(Cauldron.RecipeBuilder.RecipeType)
        potion()
        brewing()
        standard()
        transform()
        ```

    - `#!groovy SoundEvent`. Sets the sound played when the recipe is crafted. Requires not null. (Default `null`).

        ```groovy
        sound(String)
        sound(SoundEvent)
        ```

    - `#!groovy int`. Sets the level of fluid in the cauldron, where each bottle is a single level. Requires greater than or equal to 0 and less than or equal to `InspirationsRegistry.getCauldronMax()`.

        ```groovy
        levels(int)
        ```

    - `#!groovy Boolean`. Sets if the cauldon must be boiling, requiring fire or another heat source beneath.

        ```groovy
        boiling()
        boiling(Boolean)
        ```

    - `#!groovy PotionType`. Sets the input potion type. Requires not null. (Default `null`).

        ```groovy
        inputPotion(PotionType)
        ```

    - `#!groovy PotionType`. Sets the output potion type. Requires not null. (Default `null`).

        ```groovy
        outputPotion(PotionType)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `knightminer.inspirations.library.recipe.cauldron.ICauldronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.cauldron.recipeBuilder()
            .standard()
            .input(item('minecraft:gold_ingot'))
            .fluidInput(fluid('lava'))
            .output(item('minecraft:clay'))
            .boiling()
            .sound(sound('minecraft:block.anvil.destroy'))
            .levels(3)
            .register()
        ```

???+ Abstract "mods.inspirations.cauldron.recipeBuilderBrewing()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy PotionType`. Sets the input potion type. Requires not null. (Default `null`).

        ```groovy
        inputPotion(PotionType)
        ```

    - `#!groovy PotionType`. Sets the output potion type. Requires not null. (Default `null`).

        ```groovy
        outputPotion(PotionType)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `knightminer.inspirations.library.recipe.cauldron.ICauldronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.cauldron.recipeBuilderBrewing()
            .input(item('minecraft:diamond_block'))
            .inputPotion(potionType('minecraft:fire_resistance'))
            .outputPotion(potionType('minecraft:strength'))
            .register()
        ```

???+ Abstract "mods.inspirations.cauldron.recipeBuilderDye()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy EnumDyeColor`. Sets the dye color fluid required for the input. Requires not null. (Default `null`).

        ```groovy
        dye(String)
        dye(EnumDyeColor)
        ```

    - `#!groovy int`. Sets the level of fluid in the cauldron, where each bottle is a single level. Requires greater than or equal to 0 and less than or equal to `InspirationsRegistry.getCauldronMax()`.

        ```groovy
        levels(int)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `knightminer.inspirations.library.recipe.cauldron.ICauldronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.cauldron.recipeBuilderDye()
            .input(item('minecraft:gold_block'))
            .output(item('minecraft:diamond_block'))
            .dye('blue')
            .levels(2)
            .register()
        ```

???+ Abstract "mods.inspirations.cauldron.recipeBuilderFill()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy SoundEvent`. Sets the sound played when the recipe is crafted. Requires not null. (Default `null`).

        ```groovy
        sound(String)
        sound(SoundEvent)
        ```

    - `#!groovy Boolean`. Sets if the cauldon must be boiling, requiring fire or another heat source beneath.

        ```groovy
        boiling()
        boiling(Boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `knightminer.inspirations.library.recipe.cauldron.ICauldronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.cauldron.recipeBuilderFill()
            .input(item('minecraft:gold_ingot'))
            .output(item('minecraft:clay'))
            .fluidInput(fluid('milk'))
            .sound(sound('minecraft:block.anvil.destroy'))
            .register()
        ```

???+ Abstract "mods.inspirations.cauldron.recipeBuilderMix()"
    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 2. (Default `null`).

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `knightminer.inspirations.library.recipe.cauldron.ICauldronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.cauldron.recipeBuilderMix()
            .output(item('minecraft:clay'))
            .fluidInput(fluid('milk'), fluid('lava'))
            .register()
        ```

???+ Abstract "mods.inspirations.cauldron.recipeBuilderPotion()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy int`. Sets the level of fluid in the cauldron, where each bottle is a single level. Requires greater than or equal to 0 and less than or equal to `InspirationsRegistry.getCauldronMax()`.

        ```groovy
        levels(int)
        ```

    - `#!groovy Boolean`. Sets if the cauldon must be boiling, requiring fire or another heat source beneath.

        ```groovy
        boiling()
        boiling(Boolean)
        ```

    - `#!groovy PotionType`. Sets the input potion type. Requires exactly 0 and exactly 1. (Default `null`).

        ```groovy
        inputPotion(PotionType)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `knightminer.inspirations.library.recipe.cauldron.ICauldronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.cauldron.recipeBuilderPotion()
            .input(item('minecraft:gold_block'))
            .output(item('minecraft:diamond_block'))
            .inputPotion(potionType('minecraft:fire_resistance'))
            .levels(2)
            .register()
        ```

???+ Abstract "mods.inspirations.cauldron.recipeBuilderStandard()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy ItemStackList`. Sets the item outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        output(ItemStack)
        output(ItemStack...)
        output(Collection<ItemStack>)
        ```

    - `#!groovy SoundEvent`. Sets the sound played when the recipe is crafted. Requires not null. (Default `null`).

        ```groovy
        sound(String)
        sound(SoundEvent)
        ```

    - `#!groovy int`. Sets the level of fluid in the cauldron, where each bottle is a single level. Requires greater than or equal to 0 and less than or equal to `InspirationsRegistry.getCauldronMax()`.

        ```groovy
        levels(int)
        ```

    - `#!groovy Boolean`. Sets if the cauldon must be boiling, requiring fire or another heat source beneath.

        ```groovy
        boiling()
        boiling(Boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `knightminer.inspirations.library.recipe.cauldron.ICauldronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.cauldron.recipeBuilderStandard()
            .input(item('minecraft:diamond'))
            .output(item('minecraft:clay'))
            .fluidInput(fluid('lava'))
            .levels(3)
            .sound(sound('minecraft:block.anvil.destroy'))
            .register()
        ```

???+ Abstract "mods.inspirations.cauldron.recipeBuilderTransform()"
    - `#!groovy IngredientList<IIngredient>`. Sets the item inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        input(IIngredient)
        input(IIngredient...)
        input(Collection<IIngredient>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid inputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        fluidInput(FluidStack)
        fluidInput(FluidStack...)
        fluidInput(Collection<FluidStack>)
        ```

    - `#!groovy FluidStackList`. Sets the fluid outputs of the recipe. Requires exactly 1. (Default `null`).

        ```groovy
        fluidOutput(FluidStack)
        fluidOutput(FluidStack...)
        fluidOutput(Collection<FluidStack>)
        ```

    - `#!groovy SoundEvent`. Sets the sound played when the recipe is crafted. Requires not null. (Default `null`).

        ```groovy
        sound(String)
        sound(SoundEvent)
        ```

    - `#!groovy int`. Sets the level of fluid in the cauldron, where each bottle is a single level. Requires greater than or equal to 0 and less than or equal to `InspirationsRegistry.getCauldronMax()`.

        ```groovy
        levels(int)
        ```

    - `#!groovy Boolean`. Sets if the cauldon must be boiling, requiring fire or another heat source beneath.

        ```groovy
        boiling()
        boiling(Boolean)
        ```

    - First validates the builder, returning `null` and outputting errors to the log file if the validation failed, then registers the builder and returns the registered object. (returns `null` or `knightminer.inspirations.library.recipe.cauldron.ICauldronRecipe`).

        ```groovy
        register()
        ```

    ???+ Example
        ```groovy
        mods.inspirations.cauldron.recipeBuilderTransform()
            .input(item('minecraft:stone:3'))
            .fluidInput(fluid('water'))
            .fluidOutput(fluid('milk'))
            .levels(2)
            .register()
        ```



## Removing Recipes

- Removes all recipes with the given fluid input:

    ```groovy
    mods.inspirations.cauldron.removeByFluidInput(FluidStack)
    ```

- Removes all recipes with the given fluid input:

    ```groovy
    mods.inspirations.cauldron.removeByFluidInput(Fluid)
    ```

- Removes all recipes with the given fluid output:

    ```groovy
    mods.inspirations.cauldron.removeByFluidOutput(Fluid)
    ```

- Removes all recipes with the given fluid output:

    ```groovy
    mods.inspirations.cauldron.removeByFluidOutput(FluidStack)
    ```

- Removes all recipes with the given item input:

    ```groovy
    mods.inspirations.cauldron.removeByInput(IIngredient)
    ```

- Removes all recipes with the given item output:

    ```groovy
    mods.inspirations.cauldron.removeByOutput(ItemStack)
    ```

- Removes all registered recipes:

    ```groovy
    mods.inspirations.cauldron.removeAll()
    ```

???+ Example
    ```groovy
    mods.inspirations.cauldron.removeByFluidInput(fluid('mushroom_stew'))
    mods.inspirations.cauldron.removeByFluidOutput(fluid('beetroot_soup'))
    mods.inspirations.cauldron.removeByInput(item('minecraft:ghast_tear'))
    mods.inspirations.cauldron.removeByOutput(item('minecraft:piston'))
    mods.inspirations.cauldron.removeAll()
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.inspirations.cauldron.streamRecipes()
    ```
