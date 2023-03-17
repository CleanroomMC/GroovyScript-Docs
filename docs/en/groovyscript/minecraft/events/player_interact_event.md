# PlayerInteractEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.player.PlayerInteractEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[PlayerEvent](player_event.md), [LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraftforge.fml.relauncher.Side getSide()
```

```groovy
net.minecraft.util.EnumHand getHand()
```

```groovy
net.minecraft.util.math.BlockPos getPos()
```

```groovy
net.minecraft.world.World getWorld()
```

```groovy
net.minecraft.util.EnumActionResult getCancellationResult()
```

```groovy
void setCancellationResult(net.minecraft.util.EnumActionResult arg0)
```

```groovy
net.minecraft.item.ItemStack getItemStack()
```

```groovy
net.minecraft.util.EnumFacing getFace()
```

