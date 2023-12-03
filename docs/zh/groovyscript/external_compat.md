在这里，您将学习如何为GroovyScript添加外部模组兼容性。

!!! 注意
    您至少需要版本0.7.0。

!!! 注意
    请阅读接口和方法的javadoc。

插件必须实现 `GroovyPlugin` 接口。GroovyScript将自动找到该类并实例化它。如果 `instance` 字段非空，则GroovyScript将不会实例化该类，而是使用字段的值。

字段 `TestReg test` 表示一个可以有配方的机器。

在 `onCompatLoaded()` 中，可以初始化兼容性。`container.getVirtualizedRegistrar().addFieldsOf(this)` 会自动注册该类的 `VirtualRegistries` 字段，包括 `TestReg test` 字段。

```java
public class ExampleModGroovyPlugin implements GroovyPlugin {

    public final TestReg test = new TestReg();

    @Override
    public @NotNull String getModId() {
        return "example_id";
    }

    @Override
    public @NotNull String getModName() {
        return "example_name";
    }

    @Override
    public void onCompatLoaded(GroovyContainer<?> container) {
        GroovyScript.LOGGER.info("ExampleMod容器已加载");
        container.getVirtualizedRegistrar().addRegistry(VanillaModule.furnace);
        container.getVirtualizedRegistrar().addFieldsOf(this);
    }
}
```