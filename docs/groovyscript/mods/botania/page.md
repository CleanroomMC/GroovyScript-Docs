---
title: "Lexicon Page"
description: "Page creates a new page to be used in entries."
source_code_link: "https://github.com/CleanroomMC/GroovyScript/blob/master/src/main/java/com/cleanroommc/groovyscript/compat/mods/botania/Lexicon.java"
---

# Lexicon Page (Botania)

## Description

Page creates a new page to be used in entries.

## Identifier

Refer to this via any of the following:

```groovy hl_lines="2"
mods.botania.Page
mods.botania.page/*(1)!*/
```

1. This identifier will be used as the default for examples on this page

## Adding Entries

- Adds a page to the given LexiconEntry, in the format `entry`, `page`, `index`:

    ```groovy
    mods.botania.page.add(LexiconEntry, LexiconPage, int)
    ```

- Returns a `PageBrew` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createBrewingPage(String, String, RecipeBrew)
    ```

- Returns a `PageCraftingRecipe` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createCraftingPage(String, String...)
    ```

- Returns a `PageElvenRecipe` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createElvenTradePage(String, RecipeElvenTrade...)
    ```

- Returns a `PageEntity` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createEntityPage(String, int, EntityEntry)
    ```

- Returns a `PageEntity` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createEntityPage(String, int, String)
    ```

- Returns a `PageImage` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createImagePage(String, String)
    ```

- Returns a `PageManaInfusionRecipe` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createInfusionPage(String, RecipeManaInfusion...)
    ```

- Returns a `PageLoreText` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createLoreTextPage(String)
    ```

- Returns a `PagePetalRecipe` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createPetalPage(String, RecipePetals...)
    ```

- Returns a `PageRuneRecipe` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createRunePage(String, RecipeRuneAltar...)
    ```

- Returns a `PageText` for use in adding to a LexiconEntry:

    ```groovy
    mods.botania.page.createTextPage(String)
    ```

???+ Example
    ```groovy
    mods.botania.page.createBrewingPage('groovy.exampleBrewingPage', 'bottomText', 'bottomText', mods.botania.brewrecipe.recipeBuilder().input(item('minecraft:clay'), ore('ingotGold'), ore('gemDiamond')).brew(brew('absorption')).register())
    mods.botania.page.createCraftingPage('groovy.exampleCraftingPage', 'minecraft:clay')
    mods.botania.page.createElvenTradePage('groovy.exampleElvenTradePage', mods.botania.elventrade.recipeBuilder().input(ore('ingotGold'), ore('ingotIron')).output(item('botania:manaresource:7')).register())
    mods.botania.page.createEntityPage('groovy.exampleEntityPage', 5, entity('minecraft:wither_skeleton'))
    mods.botania.page.createEntityPage('groovy.exampleEntityPage', 100, 'minecraft:wither_skeleton')
    mods.botania.page.createImagePage('groovy.exampleImagePage', 'minecraft:textures/items/apple.png')
    mods.botania.page.createInfusionPage('groovy.exampleInfusionPage', mods.botania.manainfusion.recipeBuilder().input(ore('ingotGold')).output(item('botania:manaresource', 1)).mana(500).catalyst(blockstate('minecraft:stone')).register())
    mods.botania.page.createLoreTextPage('groovy.exampleLoreTextPage')
    mods.botania.page.createPetalPage('groovy.examplePetalPage', mods.botania.apothecary.recipeBuilder().input(ore('blockGold'), ore('ingotIron'), item('minecraft:apple')).output(item('minecraft:golden_apple')).register())
    mods.botania.page.createRunePage('groovy.exampleRunePage', mods.botania.runealtar.recipeBuilder().input(ore('gemEmerald'), item('minecraft:apple')).output(item('minecraft:diamond')).mana(500).register())
    mods.botania.page.createTextPage('groovy.exampleTextPage')
    ```

## Removing Entries

- Removes a page from the given LexiconEntry, in the format `entry`, `index`:

    ```groovy
    mods.botania.page.remove(LexiconEntry, int)
    ```

- Removes all pages from the given LexiconEntry:

    ```groovy
    mods.botania.page.removeByEntry(LexiconEntry)
    ```

- Removes all pages from the given LexiconEntry:

    ```groovy
    mods.botania.page.removeByEntry(String)
    ```

- Removes all registered recipes:

    ```groovy
    mods.botania.page.removeAll()
    ```

???+ Example
    ```groovy
    mods.botania.page.removeByEntry('botania.entry.runeAltar')
    mods.botania.page.removeAll()
    ```

## Getting the value of entries

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    mods.botania.page.streamPages(LexiconEntry)
    ```
