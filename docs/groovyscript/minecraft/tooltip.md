# Item Tooltips

There is not a simple way to add tooltips. However, you can use the event system to modify any tooltip in any way you
want. <br>
See [ItemTooltipEvent](events/item_tooltip_event.md).

## Adding lines

This is the simplest way to add tooltips to a specific item. Note that this would ignore nbt data. Also, you can add
tooltips for multiple items inside the event. You don't need to call listen for the same event multiple times.

!!! example

    ```groovy
    import net.minecraftforge.event.entity.player.ItemTooltipEvent

    event_manager.listen { ItemTooltipEvent event ->
        if (event.getItemStack() in item('minecraft:diamond')) {
            event.getToolTip() << 'Epic diamond tooltip'
        }
    }
    ```

If you are familiar with [lists](../../groovy/lists.md), you can modify the tooltip lines as you like
since `event.getToolTip()` returns a `List<String>`.

## Writing your own addTooltip method
The code shown above is somewhat complicated for beginners. You can write a helper method for that.
However, this way is somewhat inefficient, and you might run into problems with large amounts of tooltips.

```groovy
import net.minecraftforge.event.entity.player.ItemTooltipEvent

def tooltipMap = [:]

event_manager.listen { ItemTooltipEvent event ->
    for (def entry in tooltipMap) { // iterate tooltip map
        if (event.getItemStack() in entry.key) { // if the item in the event matches the map entry
            event.getTooltip() << entry.value    // add the line of the map entry
        }
    }
}

def addTooltip(ItemStack itemStack, String line) {
    tooltipMap[itemStack] = line // store item and line in map
}
```

Now you can simply call `addTooltip` to add tooltips.
```groovy
addTooltip(item('minecraft:apple'), 'Hey, I am an apple.')
```
