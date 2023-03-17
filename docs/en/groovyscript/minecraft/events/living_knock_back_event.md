# LivingKnockBackEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.living.LivingKnockBackEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraft.entity.Entity getOriginalAttacker()
```

```groovy
double getOriginalRatioX()
```

```groovy
double getOriginalRatioZ()
```

```groovy
float getOriginalStrength()
```

```groovy
net.minecraft.entity.Entity getAttacker()
```

```groovy
float getStrength()
```

```groovy
double getRatioX()
```

```groovy
double getRatioZ()
```

```groovy
void setStrength(float arg0)
```

```groovy
void setAttacker(net.minecraft.entity.Entity arg0)
```

```groovy
void setRatioZ(double arg0)
```

```groovy
void setRatioX(double arg0)
```

