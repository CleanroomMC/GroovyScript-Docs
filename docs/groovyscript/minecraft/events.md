# Events

By listening to an event you can run a block of code when something special happens, for example when a block breaks or the player takes damage.

!!! example

    ```groovy
    eventManager.listen {
        Event event ->
        // Your code here
        print('Hello')
    }
    ```

Replace `Event` with the desired event class.
