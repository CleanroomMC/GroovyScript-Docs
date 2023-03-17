# PlayerEvent.HarvestCheck

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.player.PlayerEvent.HarvestCheck
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[PlayerEvent](player_event.md), [LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
boolean canHarvest()
```

```groovy
net.minecraft.block.state.IBlockState getTargetBlock()
```

```groovy
void setCanHarvest(boolean arg0)
```

