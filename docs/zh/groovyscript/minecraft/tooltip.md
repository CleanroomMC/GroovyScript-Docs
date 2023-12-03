# 物品提示信息

添加提示信息并不是一种简单的方法。然而，您可以使用事件系统以任何您想要的方式修改任何提示信息。 <br>
参见[ItemTooltipEvent](events/item_tooltip_event.md)。

## 添加行

这是向特定物品添加提示信息的最简单方法。请注意，这将忽略NBT数据。此外，您可以在事件中为多个物品添加提示信息。您无需多次调用相同事件进行侦听。

!!! 示例

    ```groovy
    import net.minecraftforge.event.entity.player.ItemTooltipEvent

    event_manager.listen { ItemTooltipEvent event ->
        if (ItemStack.areItemsEqual(event.getItemStack(), item('minecraft:diamond'))) {
            event.getToolTip().add('史诗钻石提示信息')
        }
    }
    ```

如果您熟悉[列表](../../groovy/lists.md)，您可以按照自己的喜好修改提示信息行，因为`event.getToolTip()`返回一个`List<String>`。