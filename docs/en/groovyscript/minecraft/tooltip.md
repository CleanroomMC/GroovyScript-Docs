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
        if (ItemStack.areItemsEqual(event.getItemStack(), item('minecraft:diamond'))) {
            event.getToolTip().add('Epic diamond tooltip')
        }
    }
    ```

If you are familiar with [lists](../../groovy/lists.md), you can modify the tooltip lines as you like
since `event.getToolTip()` returns a `List<String>`.
