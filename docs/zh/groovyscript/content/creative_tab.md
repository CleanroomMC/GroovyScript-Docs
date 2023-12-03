# Creating creative tabs

```groovy
content.createCreativeTab(String name, ItemStack icon) // returns the creative tab
```

!!! example

    ```groovy
    def creativeTab = content.createCreativeTab("nomifactory.creative_tab", item("nomifactory:heart_of_the_universe"))
    ```

## Other

You can get a creative tab by using

```groovy
creativeTab(String tabName)
```

A list of existing creative tab names can be obtained by running the `/gs creativeTabs` command.
