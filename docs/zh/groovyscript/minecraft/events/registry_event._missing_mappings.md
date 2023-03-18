# RegistryEvent.MissingMappings

To use this event use the following import:
```groovy
import net.minecraftforge.event.RegistryEvent.MissingMappings
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[RegistryEvent](registry_event.md), [GenericEvent](generic_event.md)

## Methods
```groovy
net.minecraft.util.ResourceLocation getName()
```

```groovy
net.minecraftforge.registries.IForgeRegistry getRegistry()
```

```groovy
void setModContainer(net.minecraftforge.fml.common.ModContainer arg0)
```

```groovy
com.google.common.collect.ImmutableList getAllMappings()
```

```groovy
com.google.common.collect.ImmutableList getMappings()
```

