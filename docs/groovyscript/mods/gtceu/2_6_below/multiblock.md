# GregTech Multiblocks

First of all, there is no special compat for multiblocks. We are simple doing it the java way in groovy, which makes it
complicated, but also highly customizable.

First we need to decide what kind of multiblock we want. For example do you want a multiblock with custom behaviour like
the tesla tower from MechTech or do you want a multiblock which can run recipes. Here we will only focus on the later.

## Making a multiblock class

Let's take the vacuum freezer for example:

```groovy
import gregtech.api.metatileentity.MetaTileEntity
import gregtech.api.metatileentity.interfaces.IGregTechTileEntity
import gregtech.api.metatileentity.multiblock.IMultiblockPart
import gregtech.api.metatileentity.multiblock.RecipeMapMultiblockController
import gregtech.api.pattern.BlockPattern
import gregtech.api.pattern.FactoryBlockPattern
import gregtech.api.recipes.RecipeMaps
import gregtech.client.renderer.ICubeRenderer
import gregtech.client.renderer.texture.Textures
import gregtech.common.blocks.BlockMetalCasing.MetalCasingType
import gregtech.common.blocks.MetaBlocks

class MetaTileEntityVacuumFreezer extends RecipeMapMultiblockController {

    /*(1)!*/
    MetaTileEntityVacuumFreezer(ResourceLocation metaTileEntityId) {
        super(metaTileEntityId, RecipeMaps.VACUUM_RECIPES) /*(2)!*/
    }

    @Override
    MetaTileEntity createMetaTileEntity(IGregTechTileEntity tileEntity) {
        return new MetaTileEntityVacuumFreezer(metaTileEntityId) /*(3)!*/
    }

    @Override
    protected BlockPattern createStructurePattern() {
        return FactoryBlockPattern.start() /*(4)!*/
                .aisle("XXX", "XXX", "XXX")
                .aisle("XXX", "X#X", "XXX")
                .aisle("XXX", "XSX", "XXX")
                .where('S', selfPredicate())
                .where('X', states(getCasingState()).setMinGlobalLimited(14).or(autoAbilities()))
                .where('#', air())
                .build()
    }

    @Override
    ICubeRenderer getBaseTexture(IMultiblockPart sourcePart) {
        return Textures.FROST_PROOF_CASING /*(5)!*/
    }

    /*(6)!*/
    protected IBlockState getCasingState() {
        return MetaBlocks.METAL_CASING.getState(MetalCasingType.ALUMINIUM_FROSTPROOF)
    }

    /*(7)!*/
    @Override
    protected ICubeRenderer getFrontOverlay() {
        return Textures.VACUUM_FREEZER_OVERLAY
    }
}
```

1. This is the constructor.
2. Pass the id and a recipe map to the super constructor.
3. In this method you need to create a new copy of the controller.
4. Here the structure is defined. This part is similar to mbt.
5. This defines what texture busses and hatches will have when the structure is formed.
6. This is a helper method to make the structure code look cleaner.
7. The overlay texture of the controller.

## Registering the multiblock

Now we have a defined a multiblock, but we need to also register it. I recommend to do this in preInit

```groovy
import gregtech.common.metatileentities.MetaTileEntities

MetaTileEntities.register(int id, MetaTileEntity mte) // id is the meta value of the controller. We recommend the range from 32000 - 32766
```

This is how register any `MetaTileEntity`. Yes, our multiblock controller is also a `MetaTileEntity`. Therefore, we can do

```groovy
import gregtech.common.metatileentities.MetaTileEntities

MetaTileEntities.register(32000, new MetaTileEntityVacuumFreezer(new ResourceLocation("gregtech", "vacuum_freezer")))
```

To create the controller we simply call its constructor, which needs a `ResourceLocation`.
If you want to create a recipe for the controller you can get the item form like this

```groovy
metaitem("vacuum_freezer")
```

If the domain of the resource location is not `gregtech`, but for example `nomifactory`, then it will be

```groovy
metaitem("nomifactory:vacuum_freezer")
```

See [resource location](../../rl.md)

## More examples

[WIP]
