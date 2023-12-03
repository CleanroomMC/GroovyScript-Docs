# 事件

通过监听事件，您可以在发生特定情况时运行一段代码，例如方块破裂或玩家受到伤害时。

!!! 示例

    ```groovy
    eventManager.listen {
        Event event ->
        // 在这里编写您的代码
        print('你好')
    }
    ```

将 `Event` 替换为所需的事件类。