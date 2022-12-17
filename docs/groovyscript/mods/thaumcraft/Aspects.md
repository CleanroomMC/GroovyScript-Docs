# Aspects

### GroovyScript syntax

To help with aspects in thaumcraft the following bracket handlers have been added:
- `aspect('<latin aspect name>') * <amount>` returns `AspectStack` (a vis - amount pairing)
- `crystal('<latin aspect name>')` returns ItemStack containing vis crystal of the specified aspect

!!! Note 
    `aspect('<latin aspect name>')` when no <amount> is specified the default value is 1

### AspectStack

An Aspect wrapper with the following methods: <br>

- `AspectStack#getCrystal()` same as `crystal('<latin aspect name>')`
- `AspectStack#getPhial()` returns ItemStack containing a phial of the specified aspect

### Create a new Aspect

```groovy
mods.thaumcraft.Aspect.aspectBuilder()
        .tag('humor')
        .chatColor(14013676)
        .component(aspect('cognito'))
        .component(aspect('perditio'))
        .image('thaumcraft', 'textures/aspects/humor.png')
        .register()
```

!!! Note
    `image()` requires a mod id as first parameter and a image path relative to `assets/`.
    `image('thaumcraft:textures/aspects/humor.png')` is equivalent to the example above.

### Remove aspects from an item

```groovy
mods.thaumcraft.AspectHelper.aspectBuilder()
        .object(ore('cropPumpkin'))
        .stripAspects()
        .register()
```

### Add an existing aspect to item

```groovy
mods.thaumcraft.AspectHelper.aspectBuilder()
        .object(item('minecraft:stone'))
        .stripAspects()
        .aspect(aspect('ignis') * 20)
        .register()
```

### Add an existing aspect to entity

```groovy
mods.thaumcraft.AspectHelper.aspectBuilder()
        .entity(entity('minecraft:chicken'))
        .stripAspects()
        .aspect(aspect('bestia') * 20)
        .register()
```
