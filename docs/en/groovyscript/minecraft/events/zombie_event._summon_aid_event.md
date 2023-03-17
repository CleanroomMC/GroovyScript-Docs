# ZombieEvent.SummonAidEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.living.ZombieEvent.SummonAidEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[ZombieEvent](zombie_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
int getY()
```

```groovy
int getX()
```

```groovy
boolean hasResult()
```

```groovy
void setCustomSummonedAid(net.minecraft.entity.monster.EntityZombie arg0)
```

```groovy
net.minecraft.entity.monster.EntityZombie getCustomSummonedAid()
```

```groovy
int getZ()
```

```groovy
net.minecraft.world.World getWorld()
```

```groovy
double getSummonChance()
```

```groovy
net.minecraft.entity.EntityLivingBase getAttacker()
```

