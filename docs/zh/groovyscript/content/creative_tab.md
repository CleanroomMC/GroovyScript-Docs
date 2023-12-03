# 创建创造模式标签

```groovy
content.createCreativeTab(String name, ItemStack icon) // 返回创造模式标签
```

!!! 示例

    ```groovy
    def creativeTab = content.createCreativeTab("nomifactory.creative_tab", item("nomifactory:heart_of_the_universe"))
    ```

## 其他

您可以通过以下方式获取创造模式标签

```groovy
creativeTab(String tabName)
```

可以通过运行 `/gs creativeTabs` 命令获取现有创造模式标签名称列表。