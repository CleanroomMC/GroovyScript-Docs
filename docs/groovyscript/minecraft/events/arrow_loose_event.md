# ArrowLooseEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.player.ArrowLooseEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[PlayerEvent](player_event.md), [LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraft.world.World getWorld()
```

```groovy
boolean hasAmmo()
```

```groovy
int getCharge()
```

```groovy
net.minecraft.item.ItemStack getBow()
```

```groovy
void setCharge(int arg0)
```

