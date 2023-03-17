# LivingDropsEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.living.LivingDropsEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraft.util.DamageSource getSource()
```

```groovy
java.util.List getDrops()
```

```groovy
boolean isRecentlyHit()
```

```groovy
int getLootingLevel()
```

