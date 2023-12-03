# 矿石词典

!!! 注意
    需要版本 0.3.0+
 GroovyScript 还允许您删除和添加矿石词典到物品并重新加载它们。

## 获取矿石词典成分
矿石词典成分可用于任何接受 `IIngredient` 的配方。
!!! 例子
    ```groovy
    ore('ingotCopper') // 返回所有铜锭
    ore('ingot*') // 通配符也是有效的（返回所有锭）
    ```

## 添加矿石词典

这三种方法都是完全相同的。

!!! 例子

    ```groovy
    oreDict.add("amogus", item('minecraft:iron_ingot'))

    item('minecraft:iron_ingot').addOreDict(ore('amogus'))

    ore('amogus').add(item('minecraft:iron_ingot'))
    ```

## 删除矿石词典

这三种方法都是完全相同的。

!!! 例子

    ```groovy
    oreDict.remove("ingotIron", item('minecraft:iron_ingot'))

    item('minecraft:iron_ingot').removeOreDict(ore('ingotIron'))

    ore('ingotIron').remove(item('minecraft:iron_ingot'))
    ```

## 其他

您可以从矿石词典获取所有物品。
两种方式都是相同的。

!!! 例子

    ```groovy
    oreDict.getItems('ingotIron')
    oreDict['ingotIron']
    ```

检查物品是否在矿石词典中

!!! 例子

    ```groovy
    item('minecraft:iron_ingot') in ore('ingotIron') // 返回 true
    ```

从矿石词典获取第一个物品

!!! 例子

    ```groovy
    ore('ingotIron').first
    ore('ingotIron')[0]
    ```

遍历矿石词典中的所有物品

!!! 例子

    ```groovy
    for (def ironIngot : ore('ingotIron')) {
        ...
    }
    ```