# Crafting Table

## Adding Recipes
There are 6 similar methods to add shaped and shapeless recipes.

- Adds a shaped recipe in the format `output`, `input`. (Name is generated). The input is an up to 3x3 matrix of ingredients.

    ```groovy
    crafting.addShaped(ItemStack, List<List<IIngredient>>)
    ```
  
- Adds a shaped recipe in the format `name`, `output`, `input`

    ```groovy
    crafting.addShaped(String, ItemStack, List<List<IIngredient>>)
    ```
  
- Adds a shaped recipe in the format `name`, `output`, `input`

    ```groovy
    crafting.addShaped(ResourceLocation, ItemStack, List<List<IIngredient>>)
    ```
  
- Adds a shapeless recipe in the format `output`, `input` (Name is generated). The input is a list of up to 9 ingredients.

    ```groovy
    crafting.addShapeless(ItemStack, List<IIngredient>)
    ```
  
- Adds a shapeless recipe in the format `name`, `output`, `input`

    ```groovy
    crafting.addShapeless(String, ItemStack, List<IIngredient>)
    ```
  
- Adds a shapeless recipe in the format `name`, `output`, `input`

    ```groovy
    crafting.addShapeless(ResourceLocation, ItemStack, List<IIngredient>)
    ```

???+ Example
    ```groovy
    crafting.addShaped(item('minecraft:nether_star'), [
        [item('minecraft:clay_ball'), item('minecraft:gold_block'), item('minecraft:clay_ball')],
        [item('minecraft:gold_block'), item('minecraft:diamond_block'), item('minecraft:gold_block')],
        [item('minecraft:clay_ball'), item('minecraft:gold_block'), item('minecraft:clay_ball')]
    ])
    crafting.addShaped('custom_diamond', [
        [item('minecraft:clay_ball'), item('minecraft:gold_ingot')], 
        [item('minecraft:gold_ingot'), item('minecraft:clay_ball')]
    ])
    crafting.addShapeless('custom_netherstar', [item('minecraft:diamond'), item('minecraft:emerald'), item('minecraft:lapis')])
    ```

## Replace recipes
There are 6 similar methods that can replace existing recipes with a new one.
All of these methods have the same syntax as the addition methods, just with a different method name.

???+ Tip
    You can view recipe names in JEI/HEI by hovering over the output with `F3+h` mode enabled.

- Adds a shaped recipe in the format `output`, `input` and removes any existing recipe that matches the output (Name is generated). The input is an up to 3x3 matrix of ingredients.

    ```groovy
    crafting.replaceShaped(ItemStack, List<List<IIngredient>>)
    ```

- Adds a shaped recipe in the format `name`, `output`, `input` and removes any existing recipe that matches the name.

    ```groovy
    crafting.replaceShaped(String, ItemStack, List<List<IIngredient>>)
    ```

- Adds a shaped recipe in the format `name`, `output`, `input` and removes any existing recipe that matches the name.

    ```groovy
    crafting.replaceShaped(ResourceLocation, ItemStack, List<List<IIngredient>>)
    ```

- Adds a shapeless recipe in the format `output`, `input` and removes any existing recipe that matches the output (Name is generated). The input is a list of up to 9 ingredients.

    ```groovy
    crafting.replaceShapeless(ItemStack, List<IIngredient>)
    ```

- Adds a shapeless recipe in the format `name`, `output`, `input` and removes any existing recipe that matches the name.

    ```groovy
    crafting.replaceShapeless(String, ItemStack, List<IIngredient>)
    ```

- Adds a shapeless recipe in the format `name`, `output`, `input` and removes any existing recipe that matches the name.

    ```groovy
    crafting.replaceShapeless(ResourceLocation, ItemStack, List<IIngredient>)
    ```

## Removing Recipes
???+ Tip
    You can view recipe names in JEI/HEI by hovering over the output with `F3+h` mode enabled.

- Removes recipes in the format `mod:name`.

    ```groovy
    crafting.remove(String)
    ```

- Removes recipes in the format `name`.

    ```groovy
    crafting.remove(ResourceLocation)
    ```
  
- Removes recipes in the format `output`. Any recipe that matches the output will be removed.

    ```groovy
    crafting.removeByOutput(IIngredient)
    ```
  
- Removes recipes in the format `output`, `doLogFailure`. Any recipe that matches the output will be removed. If 
  `doLogFailure` is true, errors will not be logged. Only use this method if you know what you are doing.

    ```groovy
    crafting.removeByOutput(IIngredient, boolean)
    ```

- Removes recipes in the format `input`. Any recipe that matches any of its inputs with the given input gets removed

    ```groovy
    crafting.removeByInput(IIngredient)
    ```

- Removes recipes in the format `input`, `doLogFailure`. Any recipe that matches any of its inputs with the given input gets removed.
  If `doLogFailure` is true, errors will not be logged. Only use this method if you know what you are doing.          

    ```groovy
    crafting.removeByInput(IIngredient, boolean)
    ```

- Removes all existing crafting recipes.

    ```groovy
    crafting.removeAll()
    ```

???+ Example
    ```groovy
    crafting.remove('minecraft:tnt')
    crafting.removeByOutput(item('minecraft:tnt'))
    ```

## Getting the value of recipes

- Iterates through every entry in the registry, with the ability to call remove on any element to remove it:

    ```groovy
    crafting.streamRecipes()
    ```