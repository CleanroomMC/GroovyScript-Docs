# Creating fluids

!!! Note
    This requires at least version 0.7.0 of GroovyScript.

## The simplest way

```groovy
content.createFluid(String name).register()
```

Simple right?
Let's break it up:

- `content` is a global variable.
- `createFluid(String name)` creates a fluid builder object and returns it. The name is the registry name and must only
  consist of lower case letters and `_`.
- `register()` registers the item. Without this the item will not appear in game.

This will create a bucket item and a fluid block with a white water texture.

## Setters

- `setStill(ResourceLocation)` sets the still fluid texture
- `setFlowing(ResourceLocation)` sets the flowing fluid texture
- `setOverlay(ResourceLocation)` sets the overlay fluid texture (usually null)
- `setTexture(ResourceLocation still, ResourceLocation flowing)` sets the still and flowing fluid texture
- `setTexture(ResourceLocation still, ResourceLocation flowing, ResourceLocation overlay)` sets the still, flowing and overlay fluid texture
- `setDefaultTexture()` sets the still and flowing texture to the default texture (white water)
- `setMetalTexture()` sets the still and flowing texture to the tinkers molten metal texture
- `setColor(int)` sets fluid color. The texture is usually white. The color is applied on top of the texture
- `setSound(SoundEvent fillSound, SoundEvent emptySound)` sets the sounds for emptying and filling a bucket (default is from the fluids material)
- `setLuminosity(int)` sets the luminosity. The light level of the fluid from 0 to 15 (default is 0).
- `setDensity(int)` sets the density. Completely arbitrary value. Negative values imply that fluid is lighter than air. Default is 1000.
- `setTemperature(int)` sets the temperature. Completely arbitrary value. Default is 300 (room temperature in Kelvin).
- `setViscosity(int)` sets the viscosity. Completely arbitrary value Higher value makes the fluid flow slower. Default is 1000.
- `setGaseous(boolean)` sets if the fluid is a gas. Generally this is associated with negative density fluids. Default is false.
- `setRarity(EnumRarity)` sets the fluid rarity. This is only used for tooltip colors (afaik). Default is `EnumRarity.COMMON`.
- `setWaterMaterial()` sets the fluid material to water. This makes the fluid blocks to behave like water. This is used by default.
- `setLavaMaterial()` sets the fluid material to lava. This makes the fluid blocks to behave like lava. (No custom materials currently)
- `noBlock()` disables the fluid block from generating. Buckets will not be able to place the fluid in the world.

??? Example
    ````groovy
    content.createFluid('molten_iron')
        .setMetalTexture()
        .setColor(0xFF0000)
        .setLuminosity(4)
        .setDensity(1700)
        .setTemperature(1300)
        .setViscosity(1500)
        .setLavaMaterial()
        .register()
    ````

## Registering a fluid

The example above creates a simple fluid for you, but you can also create fluids yourself.
Use the following methods to register custom fluids.

```groovy
content.registerFluid(Fluis)
```

!!! Warning
    This is not recommended since using `createFluid(name).register()` does a lot of work for you.

## Texture

We recommend to use the default textures. But you can add other yourself.
If a fluid has a block the block state json is automatically generated,

## Translating the fluids name

Add `fluid.[pack id].[fluid name]=Fluid Name` to your lang file

Example for molten iron:
```mclang
fluid.placeholdername.molten_iron=Molten Iron
```
