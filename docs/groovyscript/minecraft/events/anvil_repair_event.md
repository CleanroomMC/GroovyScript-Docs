# AnvilRepairEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.entity.player.AnvilRepairEvent
```

## Sub-Classes

This event extends the following events and can use all their methods and fields: <br>
[PlayerEvent](player_event.md), [LivingEvent](living_event.md), [EntityEvent](entity_event.md)

## Methods
```groovy
net.minecraft.item.ItemStack getOutput()
```
```groovy
net.minecraft.item.ItemStack getRight()
```
```groovy
net.minecraft.item.ItemStack getLeft()
```
```groovy
net.minecraft.item.ItemStack getItemResult()
```
```groovy
void setBreakChance(float arg0)
```
```groovy
net.minecraft.item.ItemStack getItemInput()
```
```groovy
net.minecraft.item.ItemStack getIngredientInput()
```
```groovy
float getBreakChance()
```
