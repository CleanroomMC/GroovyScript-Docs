# Blood Magic Tranquility Amount

Package:

```groovy
mods.bloodmagic.Tranquility
```

!!! Note
    Tranquility is used to improve the effect of an Incense Altar, which increases the amount of Life Essenced gained when using a Dagger of Self-Sacrifice.
    The Incense Altar recives diminishing effects from additional sources of a type.

## Adding Tranquility to blocks

Just like other recipe types, Tranquility also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.bloodmagic.Tranquility.recipeBuilder()
```

Setting the target block: (set either the exact blockstate, or all blockstates of a block)

```groovy
.blockstate(IBlockState)
.block(Block)
```

Tranquility types are one of the following: PLANT, CROP, TREE, EARTHEN, WATER, FIRE, LAVA.

Set the Tranquility type:

```groovy
.tranquility(EnumTranquilityType)
.tranquility(String/*(1)!*/)
```

1. Must be one of the following: PLANT, CROP, TREE, EARTHEN, WATER, FIRE, LAVA.

Set value provided to the given Tranquility type:

```groovy
.value(double)
```

Register recipe:

```groovy
.register()
```

!!! example

    ```groovy
    mods.bloodmagic.tranquility.recipeBuilder()
        .block(blockstate("minecraft:obsidian").getBlock())
        .tranquility("LAVA")
        .value(10)
        .register()

    mods.bloodmagic.tranquility.recipeBuilder()
        .block(blockstate("minecraft:obsidian").getBlock())
        .tranquility("WATER")
        .value(10)
        .register()

    mods.bloodmagic.tranquility.recipeBuilder()
        .blockstate(blockstate("minecraft:obsidian"))
        .tranquility("LAVA")
        .value(500)
        .register()
    ```

## Removing Recipes

Removes the given Blockstate or all blockstates of a given Block from the target Tranquility type:

```groovy
mods.bloodmagic.Tranquility.remove(Block, String/*(1)!*/)
mods.bloodmagic.Tranquility.remove(IBlockState, String/*(2)!*/)
mods.bloodmagic.Tranquility.remove(Block, EnumTranquilityType)
mods.bloodmagic.Tranquility.remove(IBlockState, EnumTranquilityType)
```

1. Must be one of the following: PLANT, CROP, TREE, EARTHEN, WATER, FIRE, LAVA.
2. Must be one of the following: PLANT, CROP, TREE, EARTHEN, WATER, FIRE, LAVA.

Removes all registed Tranquility blockstates:

```groovy
mods.bloodmagic.Tranquility.removeAll()
```

!!! example

    ```groovy
    // Removes the target blockstate of netherrack from the FIRE Tranquility type.
    mods.bloodmagic.tranquility.remove(blockstate("minecraft:netherrack"), "FIRE")

    // Removes all blockstates of dirt from the EARTHEN Tranquility type.
    mods.bloodmagic.tranquility.remove(blockstate("minecraft:dirt").getBlock(), "EARTHEN")
    ```
