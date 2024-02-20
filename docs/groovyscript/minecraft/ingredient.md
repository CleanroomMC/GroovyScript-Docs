# IIngredient
In recipes, you often see `IIngredient` as input. The following things are `IIngredient`'s:

- `ItemStack` (f.e. `item('minecraft:apple')`)
- ore dict (f.e. `ore('ingotIron')`)
- Or ingredient (f.e. `item('minecraft:apple') | item('minecraft:iron_ingot)`)
- `FluidStack` (f.e. `fluid('water')`)
- `GasStack` (f.e. `gas('oxygen')`) (Mekanism required)

So any time you see `IIngredient` you can technically insert any of these. However, fluids and gases might not give the expected result.
In crafting recipes they are turned into any item that contains that specific fluid liker buckets or tanks.
In other recipes it might be turned into a bucket.
