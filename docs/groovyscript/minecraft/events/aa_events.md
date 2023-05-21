# Events

GroovyScript allows you to listen to any event which uses the forge event system.
Here are listed all minecraft and forge events there are.

!!! Note
    Events can be reloaded if they are registered in `postInit`

!!! example "Let's see an example:"

    ```groovy
    import net.minecraftforge.event.world.BlockEvent.BreakEvent

    event_manager.listen { BreakEvent event ->
        log.info('Block broken: {}', event.getState())
    }
    ```

What is happening?

- `event_manager` is a global variable where event listeners are registered (alternative name `eventManager`)
- `listen` is a method which accepts a [closure](../../../groovy/closure.md) with the event class as the first parameter
- `BreakEvent event` is the event being listened to. The type must be specified and imported here. (
  See [BreakEvent](block_event._break_event.md))
- Inside the closure you can do what you want. Here the broken block state is printed to the log.

## Other listen methods

```groovy
event_manager.listen(EventPriority eventPriority, EventBusType eventBusType, Closure<?> eventListener)
event_manager.listen(EventBusType eventPriority, EventPriority eventBusType, Closure<?> eventListener)
event_manager.listen(EventBusType eventPriority, Closure<?> eventListener)
event_manager.listen(EventPriority eventPriority, Closure<?> eventListener)
```

### Explanation

- `EventPriority` is the priority this listener takes compared to other listeners (from all mods). Valid values are
  - `EventPriority.HIGHEST` (executed first)
  - `EventPriority.HIGH`
  - `EventPriority.NORMAL` (default)
  - `EventPriority.LOW`
  - `EventPriority.LOWEST` (executed last)

- `EventBusType` is the event bus where you want to register your listener. Valid values are
  - `EventBusType.MAIN` (default)
  - `EventBusType.FORGE` (currently unused)
  - `EventBusType.ORE_GENERATION`
  - `EventBusType.TERRAIN_GENERATION`

- `Closure<?> eventListener` is the method executed when the event is invoked.

Normally you don't need to chane any of those values. <br>

!!! example "Let's see an example using `EventPriority`:"

    ```groovy
    import net.minecraftforge.event.world.BlockEvent.BreakEvent

    event_manager.listen(EventPriority.HIGHEST) { BreakEvent event ->
        log.info('Block broken: {}', event.getState())
    }
    ```

Now it is very likely that our listener is executed before all other (not guaranteed).
Note that we don't need to import `EventPriority`. It is auto imported.
