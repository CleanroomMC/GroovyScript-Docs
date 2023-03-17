# LivingEquipmentChangeEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.living.LivingEquipmentChangeEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraft.inventory.EntityEquipmentSlot getSlot()
```

```groovy
net.minecraft.item.ItemStack getTo()
```

```groovy
net.minecraft.item.ItemStack getFrom()
```

