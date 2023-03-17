# MinecartInteractEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.minecart.MinecartInteractEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[MinecartEvent](minecart_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraft.item.ItemStack getItem()
```

```groovy
net.minecraft.entity.player.EntityPlayer getPlayer()
```

```groovy
net.minecraft.util.EnumHand getHand()
```

