# Aspects

## GroovyScript syntax

To help with aspects in Thaumcraft the following bracket handlers have been added: <br>

- `aspect('<latin aspect name>') * <amount>` returns `AspectStack` (a vis - amount pairing)
- `crystal('<latin aspect name>')` returns ItemStack containing vis crystal of the specified aspect

`aspect('<latin aspect name>')` when no `<amount>` is specified the default value is 1

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
.tag(String/*(1)!*/)
```

1. Name of the new aspect.

Adding component aspects: (requires exactly 0 or exactly 2)

```groovy
.component(AspectStack/*(1)!*/)
```

1. Aspects which make up the new aspect.

Adding sprite image: (required) <br>
This is a [resource location](../../rl.md).

```groovy
.image(String)/*(1)!*/
.image(String mod, String path)/*(2)!*/
```

1. Path to the new aspect's target sprite in the Thaumcraft assets folder.
2. Path to the new aspect's target sprite in the "mod" assets folder.

Adding chat color: (required)

```groovy
.chatColor(int/*(1)!*/)
```

1. int should be in hexadecimal RGB format (example: 0x00FF00).

Register aspect: (returns nothing)

```groovy
.register()
```

!!! example

    ```groovy
    mods.thaumcraft.Aspect.aspectBuilder()
            .tag('humor')
            .chatColor(0xD5D4EC)
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
.object(IIngredient) // if object() is called entity() may not be
```

Set target entity: (required, entity only)

```groovy
.entity(EntityEntry) // if entity() is called object() may not be
```

Clear existing aspects: (optional)

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

!!! example

    ```groovy
    // How to remove all aspects for an item
    mods.thaumcraft.AspectHelper.aspectBuilder()
            .object(item('minecraft:dirt'))
            .stripAspects()
            .register()

    // Set chickens to have 20 Bestia Essentia
    mods.thaumcraft.AspectHelper.aspectBuilder()
            .entity(entity('minecraft:chicken'))
            .stripAspects()
            .aspect(aspect('bestia') * 20)
            .register()

    // Set Stone blocks to have 20 Ignis Essentia
    mods.thaumcraft.AspectHelper.aspectBuilder()
            .object(ore('stone'))
            .stripAspects()
            .aspect(aspect('ignis') * 20)
            .register()
    ```
