# PlaySoundAtEntityEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.PlaySoundAtEntityEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[EntityEvent](entity_event.md)

## Methods
```groovy
void setCategory(net.minecraft.util.SoundCategory arg0)
```

```groovy
net.minecraft.util.SoundCategory getCategory()
```

```groovy
float getVolume()
```

```groovy
net.minecraft.util.SoundEvent getSound()
```

```groovy
float getPitch()
```

```groovy
void setPitch(float arg0)
```

```groovy
void setVolume(float arg0)
```

```groovy
float getDefaultPitch()
```

```groovy
void setSound(net.minecraft.util.SoundEvent arg0)
```

```groovy
float getDefaultVolume()
```

