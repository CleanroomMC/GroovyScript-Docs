# PlayerSleepInBedEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.player.PlayerSleepInBedEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[PlayerEvent](player_event.md), [LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
void setResult(net.minecraft.entity.player.EntityPlayer$SleepResult arg0)
```

```groovy
net.minecraft.util.math.BlockPos getPos()
```

```groovy
net.minecraft.entity.player.EntityPlayer$SleepResult getResultStatus()
```

