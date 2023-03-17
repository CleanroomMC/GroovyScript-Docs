# BlockEvent.FluidPlaceBlockEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.world.BlockEvent.FluidPlaceBlockEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[BlockEvent](block_event.md)

## Methods
```groovy
net.minecraft.block.state.IBlockState getNewState()
```

```groovy
net.minecraft.util.math.BlockPos getLiquidPos()
```

```groovy
void setNewState(net.minecraft.block.state.IBlockState arg0)
```

```groovy
net.minecraft.block.state.IBlockState getOriginalState()
```

