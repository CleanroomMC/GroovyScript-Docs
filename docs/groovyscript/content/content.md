# Content

This part of GroovyScript allows the creation of game content like items and blocks. It's equivalent to ContentTweaker
for CraftTweaker, but for GroovyScript it doesn't require another mod.

!!! Note
    Requires version 0.4.0+. <br>
    Before you start adding content make sure to specify the pack name and id in
    your [runConfig](../../getting_started.md#run-config). <br>
    Also make sure to read [pack name and id](../../getting_started.md#pack-name-and-id)

Currently, GroovyScript adds helpers to create

- [items](item.md)
- blocks
- creative tabs

Coming in the future:

- fluids
- Mekanism gases

## Creative tabs
You can set a default creative tab which registered items and blocks will use if not specified otherwise
```groovy
content.setDefaultCreativeTab(CreativeTabs tab)
```

!!! example

    With [that](creative_tab.md) we can do this
    ```groovy
    def creativeTab = content.createCreativeTab("nomifactory.creative_tab", item("nomifactory:heart_of_the_universe"))
    content.setDefaultCreativeTab(creativeTab)
    ```
