# Aspects

### GroovyScript syntax

To help with aspects in thaumcraft the following bracket handlers have been added: <br>

- `aspect('<latin aspect name>') * <amount>` returns `AspectStack` (a vis - amount pairing)
- `crystal('<latin aspect name>')` returns ItemStack containing vis crystal of the specified aspect

`aspect('<latin aspect name>')` when no <amount> is specified the default value is 1

### AspectStack

An Aspect wrapper with the following methods: <br>

- `AspectStack#getCrystal()` same as `crystal('<latin aspect name>')`
- `AspectStack#getPhial()` returns ItemStack containing a phial of the specified aspect

### Creating Aspects

The following builder is for creating new Aspects. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.thaumcraft.Aspect.aspectBuilder()
```

Adding name: (required)

```groovy
.tag(String) // name of the new aspect
```

Adding component aspects: (2 required)

```groovy
.component(AspectStack) // name of the new aspect
```

Adding sprite image: (required)

```groovy
.image(String) // (1)
.image(String mod, String path) // (2)
```

1. Both methods are for specifying the path to the new aspect's target sprite
2. Please see the examples below to better understand how this works

Adding chat color: (required)

```groovy
.chatColor(int)
```

Register aspect: (returns nothing)

```groovy
.register()
```

### Example

```groovy
mods.thaumcraft.Aspect.aspectBuilder()
        .tag('humor')
        .chatColor(14013676)
        .component(aspect('cognito'))
        .component(aspect('perditio'))
        .image('textures/aspects/humor.png')
        .register()
```

### Item/Entity Aspects

```groovy
mods.thaumcraft.AspectHelper.aspectBuilder()
```

Set target item: (required, item only)

```groovy
.object(IIngredient)
```

Set target entity: (required, entity only)

```groovy
.entity(EntityEntry)
```

Clear exisiting aspects: (optional)

```groovy
.stripAspects()
```

Add new aspect: (optional)

```groovy
.aspect(AspectStack)
```

Register aspects: (returns nothing)

```groovy
.register()
```

### Example

```groovy
// how to remove all aspects for an item
mods.thaumcraft.AspectHelper.aspectBuilder()
        .object(item('minecraft:dirt'))
        .stripAspects()
        .register()

// set chicken's to have 20 bestia essentia
mods.thaumcraft.AspectHelper.aspectBuilder()
        .entity(entity('minecraft:chicken'))
        .stripAspects()
        .aspect(aspect('bestia') * 20)
        .register()

// set all stone blocks to have 20 ignis essentia
mods.thaumcraft.AspectHelper.aspectBuilder()
        .object(ore('stone'))
        .stripAspects()
        .aspect(aspect('ignis') * 20)
        .register()
```
