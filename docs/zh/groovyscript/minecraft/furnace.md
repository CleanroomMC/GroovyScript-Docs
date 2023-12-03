# Minecraft 熔炉

## 添加配方

与其他类型的配方不同，熔炉熔炼不使用配方生成器。

```groovy
furnace.add(IIngredient input, ItemStack output) // 应用默认的经验值 0.1
furnace.add(IIngredient input, ItemStack output, float exp)
```

!!! 例子

    ```groovy
    // 将 1 块泥土熔炼成一块圆石并获得 0.5 经验值
    furnace.add(item('minecraft:dirt'), item('minecraft:cobblestone'), 0.5f)
    ```

## 移除配方

```groovy
furnace.removeByInput(ItemStack input)
```

!!! 例子

    ```groovy
    // 移除所有熔炉中输入铁矿石的配方
    furnace.removeByInput(item('minecraft:iron_ore'))
    ```
