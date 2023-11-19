Here you'll learn about adding external mod compat for GroovyScript.

!!! Note
    You need at least version 0.7.0.

!!! Note
    Please read the javadoc for the interface and methods.

The plugin must implement `GroovyPlugin`. GroovyScript will automatically find the class and instantiate it. If the 
instance field is non-null the class will not be instantiated by GroovyScript, but instead the value of the field will 
be used.

The field `TestReg test` represents a machine that can have recipes.

In `onCompatLoaded()` the compat can be initialised. `container.getVirtualizedRegistrar().addFieldsOf(this)` 
automatically register fields of this class which are `VirtualRegistries` including the `TestReg test` field.

````java
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
        GroovyScript.LOGGER.info("ExampleMod container loaded");
        container.getVirtualizedRegistrar().addRegistry(VanillaModule.furnace);
        container.getVirtualizedRegistrar().addFieldsOf(this);
    }
}
````