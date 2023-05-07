# Just Enough Items

!!! Note
    Requires GroovyScript 0.3.1+

In all methods you can replace `jei` with `hei`.

## Hiding

```groovy
mods.jei.hide(IIngredient)
```

## Remove and Hiding

```groovy
mods.jei.removeAndHide(IIngredient)
// is exactly the same but with a cooler name
mods.jei.yeet(IIngredient)
```

## Hiding categories

A list of categories can be obtained by running /gs jeiCategories in game.

```groovy
mods.jei.hideCategory(String)
```

!!! example "Examples"

    ```groovy
    // hides nether star in jei
    mods.jei.hide(item('minecraft:nether_star'))

    // hides and removes all iron ingots and its crafting recipes
    mods.jei.removeAndHide(ore('ingotIron'))

    // hides all smelting recipes
    mods.jei.hideCategory('minecraft.smelting')
    ```
