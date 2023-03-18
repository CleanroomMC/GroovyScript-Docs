# FillBucketEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.player.FillBucketEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[PlayerEvent](player_event.md), [LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraft.util.math.RayTraceResult getTarget()
```

```groovy
boolean hasResult()
```

```groovy
net.minecraft.world.World getWorld()
```

```groovy
net.minecraft.item.ItemStack getFilledBucket()
```

```groovy
void setFilledBucket(net.minecraft.item.ItemStack arg0)
```

```groovy
net.minecraft.item.ItemStack getEmptyBucket()
```

