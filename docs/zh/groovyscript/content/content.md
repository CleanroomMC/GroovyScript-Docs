# 内容

GroovyScript 的这一部分允许创建游戏内容，如物品和方块。它相当于 CraftTweaker 的 ContentTweaker，但对于 GroovyScript，它不需要另一个模组。

!!! 注意
    需要版本 0.4.0+。<br>
    在开始添加内容之前，请确保在 [runConfig](../../getting_started.md#run-config) 中指定包的名称和 id。<br>
    还要确保阅读 [pack name and id](../../getting_started.md#pack-name-and-id)。

目前，GroovyScript 添加了创建以下辅助函数：

- [物品](item.md)
- [方块](block.md)
- [创造模式标签](creative_tab.md)
- [流体](fluid.md)

将来将推出：

- Mekanism 气体

## 创造模式标签
您可以设置一个默认的创造模式标签，如果没有另行指定，注册的物品和方块将使用该标签。
```groovy
content.setDefaultCreativeTab(CreativeTabs tab)
```

!!! 示例

    使用 [这个](creative_tab.md)，我们可以这样做
    ```groovy
    def creativeTab = content.createCreativeTab("nomifactory.creative_tab", item("nomifactory:heart_of_the_universe"))
    content.setDefaultCreativeTab(creativeTab)
    ```