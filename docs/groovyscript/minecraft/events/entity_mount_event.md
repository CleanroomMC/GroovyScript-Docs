# EntityMountEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.EntityMountEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraft.world.World getWorldObj()
```

```groovy
net.minecraft.entity.Entity getEntityBeingMounted()
```

```groovy
net.minecraft.entity.Entity getEntityMounting()
```

```groovy
boolean isMounting()
```

```groovy
boolean isDismounting()
```

