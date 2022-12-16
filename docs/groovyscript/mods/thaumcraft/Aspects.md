# Aspects

### GroovyScript syntax

To help with aspects in thaumcraft the following bracket handlers have been added:
- ``aspect('<latin aspect name>') * <amount>`` returns AspectStack (a vis - amount pairing)
- ``crystal('<latin aspect name>')`` returns ItemStack containing vis crystal of the specified aspect

Note: ``aspect('<latin aspect name>')`` when no <amount> is specified the default value is 1

### AspectStack

An Aspect wrapper with the following methods:
- ``AspectStack().getCrystal()`` same as ``crystal('<latin aspect name>')``
- ``AspectStack().getPhial()`` returns ItemStack containing a phial of the specified aspect

### Create a new Aspect

```groovy
mods.thaumcraft.Aspect.aspectBuilder()
        .tag('humor')
        .chatColor(14013676)
        .component(aspect('cognito'))
        .component(aspect('perditio'))
        .image(new ResourceLocation('thaumcraft', 'textures/aspects/humor.png'))
        .register()
```

Note: Requires ``import net.minecraft.util.ResourceLocation``.  ResourceLocation must point to the aspect's item sprite. Component are the two aspects which combine to create the new aspect.

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
