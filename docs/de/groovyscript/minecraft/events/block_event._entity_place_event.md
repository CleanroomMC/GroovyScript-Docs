# BlockEvent.EntityPlaceEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.world.BlockEvent.EntityPlaceEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[BlockEvent](block_event.md)

## Methods
```groovy
net.minecraft.entity.Entity getEntity()
```

```groovy
net.minecraftforge.common.util.BlockSnapshot getBlockSnapshot()
```

```groovy
net.minecraft.block.state.IBlockState getPlacedBlock()
```

```groovy
net.minecraft.block.state.IBlockState getPlacedAgainst()
```

