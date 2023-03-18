# UseHoeEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.player.UseHoeEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[PlayerEvent](player_event.md), [LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
boolean hasResult()
```

```groovy
net.minecraft.util.math.BlockPos getPos()
```

```groovy
net.minecraft.world.World getWorld()
```

```groovy
net.minecraft.item.ItemStack getCurrent()
```

