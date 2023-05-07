# Blood Magic Meteor Ritual

Package:

```groovy
mods.bloodmagic.Meteor
```

!!! Note
    Meteors are created via activating a `Mark of the Falling Tower` Ritual, tossing a catalyst item onto the Master
    Ritual Stone, and having enough Life Essence within the activator's Blood Network to pay the cost.

## Adding Meteors

Just like other recipe types, the Meteor also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.bloodmagic.Meteor.recipeBuilder()
```

Adding the catalyst: (requires exactly 1)

```groovy
.catalystStack(ItemStack)
.catalyst(ItemStack)
```

Adding meteor components: (requires one or more)

```groovy
.component(int weight, String ore) // The string name of the oredict.
.component(String ore, int weight) // weight and ore can be in either order.
.component(int weight, OreDictIngredient ore)
.component(OreDictIngredient ore, int weight)
```

Setting Explosion Strength: (optional (default is 0))

```groovy
.explosionStrength(float)
```

Setting Life Essence cost: (optional (default is 1000000))

```groovy
.cost(int)
```

Setting radius: (requires a radius greater than 0)

```groovy
.radius(int)
```

Register the meteor: (returns `WayofTime.bloodmagic.meteor.Meteor`)

```groovy
.register()
```

!!! example

    ```groovy
    mods.bloodmagic.Meteor.recipeBuilder()
        .catalyst(item("minecraft:gold_ingot"))
        .component(ore("oreIron"), 20) // 10% iron ore
        .component(ore("oreDiamond"), 10) // 10% diamond ore
        .component(ore("stone"), 70) // 70% stone
        .radius(7)
        .explosionStrength(10)
        .cost(1000)
        .register()

    mods.bloodmagic.Meteor.recipeBuilder()
        .catalyst(item("minecraft:clay"))
        .component("blockClay", 10) // (1)
        .radius(20)
        .explosionStrength(20)
        .register() // Has the default Life Essence cost of 1000000
    ```

    1. Since there is only one component, it will be 100% clay blocks regardless of weight.

## Removing Meteors

Removes the Meteor that matches the given catalyst item:

```groovy
mods.bloodmagic.Meteor.remove(ItemStack)
mods.bloodmagic.Meteor.removeByInput(ItemStack)
mods.bloodmagic.Meteor.removeByCatalyst(ItemStack)
```

Removes all registed Meteors:

```groovy
mods.bloodmagic.Meteor.removeAll()
```

!!! example

    ```groovy
    // Removes the default Meteor with a catalyst of an Diamond Block.
    mods.bloodmagic.Meteor.remove(item("minecraft:diamond_block"))
    ```
