# Materials

First of all, the best docs is the source
itself: [Source](https://github.com/GregTechCEu/GregTech/blob/master/src/main/java/gregtech/api/unification/material/Material.java)

!!! Note
    This docs goes of GroovyScript version 0.4.0 and GTCEu 2.5.4

## Introduction

### Firstly, you should know what a **Material** actually is

Material is the basis of CEu. It defines a substance and its properties. It usually takes the form of an **element** (
i.e. Oxygen) or a **compound** (i.e. Water), but it can also take the form of something weird like the **Eye of Ender**.

### Which Properties are defined?

The **Material** specifies whether it has a **Fluid** property, **plasma** property, **dust** property, **gem** property
or **ingot** property. When it has a specific property, GTCEu will register the corresponding item or fluid
automatically. Some properties will require others, like **Ingot** requiring **Dust**.

### What else does it define?

You can additionally define **Colors**, **Flags** (indicators for specific attributes), **MaterialIconSet** (textures),
**CableProperties**, **Element**, **Formula** (tooltips), **Components** and more. Don't worry, they are not
complicated, and will be introduced in detail below.

***

### Retrieving Existing Materials

There are two good ways to do this: the simple way and the not simple way.

#### The Simple Way

This method requires the Material to first exist. This method goes off of the material's **Unlocalized Name**, which is
the name used before it is translated in a lang file. You can use the `/gs hand` command to retrieve the material of
items.

```groovy
// assigns the variable my_material to a Material called Steel.
def my_material = material('steel')
```

#### The Not Simple Way

This method also works exactly the same as before, but the former is much easier and more convenient. It is **strongly**
recommended to use the **Simple Way**.

```groovy
// import the Material class to use Materials
import gregtech.api.unification.material.Materials

// assigns the variable my_material to a Material called Steel.
var my_material = Materials.Steel
```

***

## Creating a New Material

GregTech materials must be created in the `preInit` loader. Additionaly they need to be registered (or modified) inside
an event.

```groovy
// import the material event
import gregtech.api.GregTechAPI.MaterialEvent

// register an event listener
event_manager.listen { MaterialEvent event ->
    // create materials here
}
```

Note that when the event runs GregTech materials are already created, but addon materials might not. To modify addon
materials (but don't register) use `PostMaterialEvent` instead of `MaterialEvent`.

Materials are created using a system called `MaterialBuilder`. If you've used GregTech CE and CEu's system for adding
machine recipes, this will feel very similar.

All Materials need a number `id` and a `name`. The `id` must be from 0-32767, however, Ids 32000+ are reserved for pack
makers. No add-on developer is supposed to use ids in that range, so there should be no worry about conflicts. 700+
materials is more than all of CEu uses by itself too! The `name` must be all lowercase, contain no spaces, and not have
special characters (@, %, etc).

```groovy
import gregtech.api.GregTechAPI.MaterialEvent
import gregtech.api.unification.material.Material

// import the Material class for making new materials

event_manager.listen { MaterialEvent event ->
    /*
     * This does not do much on its own.
     * It assigns a variable to a new MaterialBuilder, with an id of 32000, and a name of "my_material".
     */
    def my_material_builder = new Material.Builder(32000, "my_material")
}
```

```groovy
import gregtech.api.GregTechAPI.MaterialEvent
import gregtech.api.unification.material.Material

event_manager.listen { MaterialEvent event ->
    /*
     * This will not work quite yet. Read on to learn what else this needs!
     * It would assign a variable to a new Material, with an id of 32001, and a name of "my_real_material".
     *
     * Use .build() to finish building a material. This is what actually creates it.
     */
    def my_material = new Material.Builder(32001, "my_real_material").build()
}
```

### Adding Material Properties

This is where materials really start to take shape. All of the following methods are called on
a `new Material.Builder()`.
Scroll down to the first example to see how to do this. Each method can be chained together, one after the other, until
the desired material is all specified. It is then built and the end and returns a finished Material.

**fluid**: _`fluid(@Optional String type, @Optional boolean hasBlock)`_

Adds a `FluidProperty` to this Material, which generates a fluid.
The following two parameters are optional. If you want to modify a later optional parameter, you must specify a value
for every preceding one. Note that you do not need to specify anything when using `fluid()`.

* `@Optional type` - The Material.FluidType of this Material, either `"fluid"` or `"gas"`.
* `@Optional hasBlock` - If `true`, create a Fluid Block for this Material, which can be placed in the world.

**plasma**: _`plasma()`_

Adds a `PlasmaProperty` to this Material, which generates a plasma.
It does not require a `FluidProperty`, but can be used in conjunction with it.

**dust**: _`dust(@Optional int harvestLevel, @Optional int burnTime)`_

Adds a `DustProperty` to this Material, which generates a Dust, Small Dust, and Tiny Dust.
**Is automatically applied by `IngotProperty` and `GemProperty`**.

* `@Optional harvestLevel` - The Harvest Level of the Material's block when mining it. If the Material also has
  a `ToolProperty`, this value will also be used to determine the tool's Mining Level.
* `@Optional burnTime` - The Burn Time (in ticks) of this Material as a Furnace Fuel. If not specified, the material *
  _cannot_* be used as a furnace fuel.

**ingot**: _`ingot(@Optional int harvestLevel, @Optional int burnTime)`_

Adds an `IngotProperty` to this Material, which generates an Ingot. It automatically adds a `DustProperty`. **This is
INCOMPATIBLE with `GemProperty`.**

* `@Optional harvestLevel` - The Harvest Level of the Material's block when mining it. If the Material also has
  a `ToolProperty`, this value will also be used to determine the tool's Mining Level. If this Material already had a
  Harvest Level defined, it will be overridden.
* `@Optional burnTime` - The Burn Time (in ticks) of this Material as a Furnace Fuel. If not specified, the material *
  _cannot_* be used as a furnace fuel. If this Material already had a Burn Time defined, it will be overridden.

**gem**: _`gem(@Optional int harvestLevel, @Optional int burnTime)`_

Adds a `GemProperty` to this Material, which generates all types of GregTech Gems. It automatically adds
a `DustProperty`. **This is INCOMPATIBLE with `IngotProperty`.**

* `@Optional harvestLevel` - The Harvest Level of the Material's block when mining it. If the Material also has
  a `ToolProperty`, this value will also be used to determine the tool's Mining Level. If this Material already had a
  Harvest Level defined, it will be overridden.
* `@Optional burnTime` - The Burn Time (in ticks) of this Material as a Furnace Fuel. If not specified, the material *
  _cannot_* be used as a furnace fuel. If this Material already had a Burn Time defined, it will be overridden.

**polymer**: _`polymer(@Optional int harvestLevel)`_

Adds a `PolymerProperty` to this material, which determines if special lang entries should be used for its items: such
as "Sheet" instead of "Plate." This requires a `FluidProperty`.

* `@Optional harvestLevel` - The Harvest Level of the Material's block when mining it. If the Material also has
  a `ToolProperty`, this value will also be used to determine the tool's Mining Level. If this Material already had a
  Harvest Level defined, it will be overridden.

**color**: _`color(int color)`_

Set the Color of this Material. Defaults to 0xFFFFFF unless `colorAverage()` is used. Colors can be supplied in either
of the following formats: the integer value, such as `16777215` or as `0xFFFFFF`. This is RGB, with no alpha channel.

* `color` - The RGB color to use for the Material.

**colorAverage**: _`colorAverage()`_

The Material's Color will be a weighted average of all of the Components' colors in the Material.

**rotorStats**: _`rotorStats(float speed, float damage, int durability)`_

Set the stats for turbine rotors which are made from this Material. Speed and Damage are used according to a formula,
and do not reflect those two user-facing properties directly.

* `speed` - Speed of the rotor.
* `damage` - Damage of the rotor.
* `durability` - Durability of the rotor.

**blastTemp**:
_`blastTemp(int temp, @Optional String gasTier, @Optional int eutOverride, @Optional int durationOverride)`_

Sets the Blast Furnace Temperature of this Material. If below 1000 Kelvin, Primitive Blast Furnace recipes will be also
added. If above 1750 Kelvin, a Hot Ingot and its appropriate Vacuum Freezer recipe will be also added. If a Material
with this Property has a Fluid, its temperature will be set to this if it is currently using the default Fluid
temperature.

* `temp` - Blast Furnace Temperature in Kelvin required to heat up the material. Just like in real life, this value *
  _cannot_* be less than `0`.
* `@Optional gasTier` - The tier of gas used to smelt in the Electric Blast Furnace. Available options
  are: `"LOW"`, `"MID"`, `"HIGH"`, `"HIGHER"`, `"HIGHEST`.
* `@Optional eutOverride` - Sets the EU/t of autogenerated Electric Blast Furnace recipes to the specified value.
* `@Optional durationOverride` - Sets the base duration in ticks of autogenerated Electric Blast Furnace recipes to the
  specified value.

**ore**: _`ore(@Optional int oreMultiplier, @Optional int byproductMultiplier, @Optional boolean emissive)`_

Adds Ore Blocks, Crushed, Crushed Purified, Crushed Centrifuged, Impure Dust, and Purified Dust for this Material.

* `@Optional oreMultiplier` - Crushed Ore output amount multiplier for Ore -> Crushed Ore Maceration. Default: 1 (no
  multiplier).
* `@Optional byproductMultiplier` - Byproduct output amount multiplier for Crushed Ore processing of any kind. Default:
  1 (no multiplier).
* `@Optional emissive` - Should ore block use emissive texturing (see below image). Default: false.

![](https://user-images.githubusercontent.com/18493855/143446969-80de6354-ad12-4170-81f5-071d6c0bb7cd.png)

**washedIn**: _`washedIn(Material material, @Optional int washedAmount)`_

Sets what the material's crushed ore is washed in using the Chemical Bath. Requires `OreProperty` to be set.

* `material` - The Material in which this material is to be washed. The parameter's Material requires `FluidProperty` to
  be set.
* `@Optional washedAmount` - The amount of fluid the crushed ore will be washed in. Default: 100mB.

**separatedInto**: _`separatedInto(Material... materials)`_

Sets the products of processing this Material's Purified Dust in an Electromagnetic Separator. Requires `OreProperty` to
be set.

* `materials` - An array of materials which is output in the magnetic separator. This already includes the Material
  itself automatically.

**addOreByproducts**: _`addOreByproducts(Material... materials)`_

Sets the Ore Byproducts of this Material. Requires `OreProperty` to be set.

* `materials` - An array of materials which are used for various ore processing byproduct outputs.

**oreSmeltInto**: _`oreSmeltInto(Material material)`_

Sets the Direct Smelting product in a vanilla furnace of this Material's ore related forms. Requires `OreProperty` to be
set.

* `material` - The material to output in the furnace. Can have `IngotProperty`, `GemProperty`, or `DustProperty`.

**polarizesInto**: _`polarizesInto(Material material)`_

Sets the Polarizer product of this Material. Requires `IngotProperty` to be set.

* `material` - The material to output when polarized.

**arcSmeltInto**: _`arcSmeltInto(Material material)`_

Sets the Arc Furnace product of this Material. Requires `IngotProperty` to be set.

* `material` - The material to output when arc furnaced. By default, the material will output itself.

**macerateInto**: _`macerateInto(Material material)`_

Sets the Macerator product of this Material. Requires `IngotProperty` to be set.

* `material` - The material to output when macerated. By default, the material will output itself.

**fluidTemp**: _`fluidTemp(int temp)`_

Sets the temperature of the fluid of this Material. Requires `FluidProperty` to be set.

* `temp` - The temperature in Kelvin to set. Like in real life, this value **cannot** be less than `0`.

**cableProperties**: _`cableProperties(long voltage, int amperage, int loss, @Optional boolean isSuperCon)`_

Adds cables and wires of this Material. Requires `IngotProperty` to be set.

* `voltage` - The voltage amount a 1x wire/cable can transfer.
* `amperage` - The amperage amount a 1x wire/cable can handle.
* `loss` - The loss per block a 1x **wire** will have. Cables have this value divided by 2, but will never be lossless
  unless set to `0`.
* `@Optional isSuperCon` - Whether this is a superconductor. This will prevent cables from generating, and have a loss
  of `0`.

**fluidPipeProperties**: _`fluidPipeProperties(int maxTemp, int throughput, boolean gasProof)`_

Adds Fluid Pipes of this Material. Requires `IngotProperty` to be set.

* `maxTemp` - Sets the maximum allowed fluid temperature in the pipe. Pipes burn/vanish when fluid is too hot.
* `throughput` - Sets the maximum flowrate through the pipes. This value multiplied by `20` is the maximum rate for the
  Tiny Pipe. Each subsequent pipe is further multiplied by `2` over the previous.
* `gasProof` - If `true`, the pipe is able to transfer fluids with the Gas state. Else, they will vaporize.

**fluidPipeProperties**:
_`fluidPipeProperties(int maxTemp, int throughput, boolean gasProof, boolean acidProof, boolean cryoProof, boolean plasmaProof)`_

Adds Fluid Pipes of this Material. Requires `IngotProperty` to be set.

* `maxTemp` - Sets the maximum allowed fluid temperature in the pipe. Pipes burn/vanish when fluid is too hot.
* `throughput` - Sets the maximum flowrate through the pipes. This value multiplied by `20` is the maximum rate for the
  Tiny Pipe. Each subsequent pipe is further multiplied by `2` over the previous.
* `gasProof` - If `true`, the pipe is able to transfer fluids with the Gas state. Else, they will vaporize.
* `acidProof` - If `true`, the pipe is able to transfer fluids with the Acidic attribute. Else, they will destroy the
  pipe.
* `cryoProof` - If `true`, the pipe is able to transfer fluids with the Cryogenic attribute. Else, they will vaporize.
* `plasmaProof` - If `true`, the pipe is able to transfer fluids with the Plasma state, regardless of the fluid pipe's
  maximum temperature. Else, they will destroy the pipe.

**itemPipeProperties**: _`itemPipeProperties(int priority, float stacksPerSec)`_

Adds item pipes of this Material. Requires `IngotProperty` to be set.

* `priority` - Sets the priority for the pipe. Items will take the path with the lowest priority. This value is used for
  the Normal Pipe. The Small Pipe has this value multiplied by `1.5`, and the Large Pipe has this value multiplied
  by `0.75`.
* `stacksPerSec` - Sets the maximum transfer rate in stacks of 64 items per second. This value is used for the Normal
  Pipe. Small Pipes have this value multiplied by `0.5`. Large Pipes have this value multiplied by `2`.

#### Tool stats

Tool stats are slightly more complicated than in CT, but also more configurable. <br>
**toolStats**: _`toolStats(ToolProperty property)`_ <br>
As you can see there is only one method which accepts a ToolProperty. You can create it like this:

```groovy
import gregtech.api.unification.material.properties.ToolProperty

ToolProperty property = ToolProperty.Builder.of(float speed, float damage, int durability, int harvestLevel).build()
```

Before calling `build()` at the end you can call several other methods to further customize your tool stats

```groovy
ToolProperty property = ToolProperty.Builder.of(float speed, float damage, int durability, int harvestLevel)
        .attackSpeed(float attackSpeed) // self explanatory
        .ignoreCraftingTools() /*(1)!*/
        .unbreakable() // self explanatory
        .enchantment(Enchantment enchantment, int level) /*(2)!*/
        .magnetic() /*(3)!*/
        .durabilityMultiplier(int multiplier) /*(4)!*/
        .build()
```

1. There won't be any crafting tools like hammer, saw and wrench
2. Default enchantment that every tool with this material has. `Enchantment` can be obtained with the `enchantment(String name)` method.
3. All mined block will go straight to the players inventory.
4. A multiplier for the property durability.

Set the stats for tools which are made from this Material.

* `speed` - Mining Speed of the tools.
* `damage` - Attack Damage dealt by the tools.
* `durability` - Durability of the tools.
* `harvestLevel` - Harvest Level of the tools.

!!! example

    This is example of a material using everything mentioned so far.

    ```groovy
    import gregtech.api.GregTechAPI.MaterialEvent
    import gregtech.api.unification.material.Material

    event_manager.listen { MaterialEvent event ->
        def specialSteel = new Material.Builder(32002, "special_steel") // name
                .fluid("gas", false) // gas without block
                .ingot() // has ingot (and therefore dust)
                .color(0x0000FF) // pure blue
                .toolStats(10, 3, 256, 21) // tool stats
                .blastTemp(2900) // EBF temperature
                .ore() // has ore blocks
                .addOreByproducts(material('gold'), material('copper')) // add byproducts
                .cableProperties(128, 2, 4, false) // add cables
                .build() // build the actual material
    }
    ```

### Changing Material Appearances

You may have noticed from testing the above example that the material's textures looks like the same style as many
others. This is called the `MaterialIconSet`. This entire next section is dedicated to explaining this system and how to
use it.

Available **MaterialIconsets** and existing material examples which use them.

| MaterialIconset    | Example         |
|--------------------|-----------------|
| `"DULL"`           | Aluminium       |
| `"METALLIC"`       | Steel           |
| `"MAGNETIC"`       | Magnetic Steel  |
| `"SHINY"`          | Copper          |
| `"BRIGHT"`         | Annealed Copper |
| `"DIAMOND"`        | Apatite         |
| `"EMERALD"`        | Cinnabar        |
| `"GEM_HORIZONTAL"` | Blue Topaz      |
| `"GEM_VERTICAL"`   | Sapphire        |
| `"RUBY"`           | Ruby            |
| `"OPAL"`           | Opal            |
| `"GLASS"`          | Glass           |
| `"NETHERSTAR"`     | Nether Star     |
| `"FINE"`           | Rock Salt       |
| `"SAND"`           | Glauconite Sand |
| `"WOOD"`           | Wood            |
| `"ROUGH"`          | Pyrite          |
| `"FLINT"`          | Flint           |
| `"LIGNITE"`        | Coal Coke       |
| `"QUARTZ"`         | Quartzite       |
| `"CERTUS"`         | Certus Quartz   |
| `"LAPIS"`          | Lazurite        |
| `"FLUID"`          | Nitric Acid     |
| `"GAS"`            | Argon           |

For example, the following image shows the appearance of ores with different MaterialIconSets.
![](https://user-images.githubusercontent.com/18493855/143435701-058dcfea-ea35-4976-a7ba-7901fa791e36.png)

The MaterialIconSet of a material, which determines all of its textures, is set with a single method.

`iconSet`: _`iconSet(String iconSet)`_

Sets the `MaterialIconSet` of this Material. Defaults vary depending on if the Material has:

* `GemProperty` - defaults to `"GEM_VERTICAL"`
* `IngotProperty` or `DustProperty` - defaults to `"DULL"`
* `FluidProperty` - defaults to either `"FLUID"` or `"GAS"`, depending on the `FluidType`
* `PlasmaProperty` - defaults to `"FLUID"`, but will receive a special plasma texture regardless.

The default will be determined by the property found first in this order.

!!! example "Example with a MaterialIconSet"

    ```groovy
    import gregtech.api.GregTechAPI.MaterialEvent
    import gregtech.api.unification.material.Material

    event_manager.listen { MaterialEvent event ->
        def specialSteelTextured = new Material.Builder(32003, "special_steel_textured") // name
                .fluid("gas", false) // gas without block
                .ingot() // has ingot (and therefore dust)
                .color(0x0000FF) // pure blue
                .iconSet("shiny") // iconset to the shiny type
                .toolStats(10, 3, 256, 21) // tool stats
                .blastTemp(2900) // EBF temperature
                .ore() // has ore blocks
                .addOreByproducts(material('gold'), material('copper')) // add byproducts
                .cableProperties(128, 2, 4, false) // add cables
                .build() // build the actual material
    }
    ```

### Components

**Components** refers to composition of the Material.

For example, the components of TungstenSteel is `1 Tungsten (W)` and `1 Steel (Fe)`. That makes its chemical formula:
![Screenshot_20211213_191326](https://user-images.githubusercontent.com/37029404/145909670-cfd0e024-ed32-4f4d-9c72-aee5c2e3b064.png)

#### MaterialStack

Components are determined using something called a `MaterialStack`. This is the Material version of an ItemStack which
is an Item with a Count. In our case, MaterialStack is a Material with a Count.

```groovy
// creates a MaterialStack of Material Tin with a Count of 3.
def my_material_stack = material('tin') * 3
```

Simple, isn't it?

#### Setting the Components

**components**: _`components(MaterialStack... components)`_

Sets the components of the material.

* `components` - an array of `MaterialStacks` representing the components of this Material.

!!! example

    ```groovy
    import gregtech.api.GregTechAPI.MaterialEvent
    import gregtech.api.unification.material.Material

    event_manager.listen { MaterialEvent event ->
        def cursed_chemistry_material = new Material.Builder(32004, "cursed_chemistry_material")
                .fluid()
                .color(0x00FF00) // pure red
                .components(material('silver') * 3, material('nitrogen') * 6, material('carbon') * 2) // set the components
                .build() // build the actual material
    }
    ```

### Material Flags

`MaterialFlags` refers to additional mini-attributes about the material. There are a ton of them.

Available MaterialFlags for Every Material:

* `"no_unification"`: Add to material to disable it's unification fully (this means no autogenerated recipes).
* `"decomposition_requires_hydrogen"`: Decomposition recipe requires hydrogen as additional input. Amount is equal to
  input amount. Sets the electrolyzer voltage to EV.
* `"decomposition_by_electrolyzing"`: Enables electrolyzer decomposition recipe generation.
* `"decomposition_by_centrifuging"`: Enables centrifuge decomposition recipe generation.
* `"disable_decomposition"`: Disables decomposition recipe generation for this material and all materials that has it as
  component.
* `"explosive"`: Add to material if it is some kind of explosive.
* `"flammable"`: Add to material if it is some kind of flammable.
* `"generate_plate"`:

Available MaterialFlags for Materials with `DustProperty`:

* `"generate_plate"`: Generate a plate for this material. If it only has a `DustProperty`, a dust compressor recipe will
  be added. If it has an `IngotProperty`, bending machine recipes will be added. If a block is found, cutting machine
  recipes will be generated.
* `"generate_rod"`: Generate a rod for this material.
* `"generate_frame"`: Generate a frame for this material. Requires `"generate_rod"`.
* `"generate_gear"`: Generate a gear for this material. Requires `"generate_plate"` and `"generate_rod"`.
* `"generate_long_rod"`: Generate a long rod for this material. Requires `"generate_rod"`.
* `"exclude_block_crafting_recipes"`: Prevent creating shapeless recipes for dust to block and vice versa. Prevents
  extruding and alloy smelting via the Block Shape/Mold.
* `"exclude_plate_compressor_recipe"`: Prevent creating plates in the compressor from dust. Requires `"generate_plate"`.
* `"exclude_block_crafting_by_hand_recipes"`: Prevent creating shapeless recipes for dust to block and vice versa.
* `"mortar_grindable"`: All the material to be ground into dust when crafting with a mortar.

Available MaterialFlags for Materials with `IngotProperty`:

* `"no_working"`: Add if it cannot be worked by any means other than smashing or smelting. This is used for coated
  Materials.
* `"no_smashing"`: Add to material if it cannot be used for regular Metal working techniques since it is not possible to
  bend it.
* `"no_smelting"`: Add to material if it's impossible to smelt it.
* `"blast_furnace_calcite_double"`: Add this to your Material if you want to have its Ore Calcite heated in a Blast
  Furnace for 2x output.
* `"blast_furnace_calcite_triple"`: Add this to your Material if you want to have its Ore Calcite heated in a Blast
  Furnace for 3x output.
* `"generate_foil"`: Generate a foil for this material. Requires `"generate_plate"`.
* `"generate_bolt_screw"`: Generate a bolt and screw for this material. Requires `"generate_rod"`.
* `"generate_ring"`: Generate a ring for this material. Requires `"generate_rod"`.
* `"generate_spring"`: Generate a spring for this material. Requires `"generate_long_rod"`.
* `"generate_spring_small"`: Generate a small spring for this material. Requires `"generate_rod"`.
* `"generate_small_gear"`: Generate a small gear for this material. Requires `"generate_plate"` and `"generate_rod"`.
* `"generate_fine_wire"`: Generate a fine wire for this material. Requires `"generate_foil"`.
* `"generate_rotor"`: Generate a rotor for this material. Requires `"generate_bolt_screw"`, `"generate_ring"`,
  and `"generate_plate"`.
* `"generate_dense"`: Generate a dense plate for this material. Requires `"generate_plate"`.
* `"generate_round"`: Generate a dense plate for this material.

Available MaterialFlags for Materials with `GemProperty`:

* `"crystallizable"`: If this material can be crystallized in an autoclave.
* `"generate_lens"`: Generate a lens for this material. Requires `"generate_plate"`.

Available MaterialFlags for Materials with `OreProperty`:

* `"high_sifter_output"`: If this material has a higher output when the Crushed Purified Ore is processed in the Sifter.

#### Adding Flags to a Material

`flags`: _`flags(String... names)`_
Add MaterialFlags to this Material.

* `names` - a string array of the names of specific MaterialFlags.

!!! example

    ```groovy
    import gregtech.api.GregTechAPI.MaterialEvent
    import gregtech.api.unification.material.Material

    event_manager.listen { MaterialEvent event ->
        def specialSteelFlagged = new Material.Builder(32004, "special_steel_flagged") // name
                .fluid("gas", false) // gas without block
                .ingot() // has ingot (and therefore dust)
                .color(0x0000FF) // pure blue
                .iconSet("shiny") // iconset to the shiny type
                .flags("generate_plate", "generate_foil") // add flags
                .toolStats(10, 3, 256, 21) // tool stats
                .blastTemp(2900) // EBF temperature
                .ore() // has ore blocks
                .addOreByproducts(material('gold'), material('copper')) // add byproducts
                .cableProperties(128, 2, 4, false) // add cables
                .build() // build the actual material
    }
    ```

### Elements

`Element` is used to specify a material as element. CEu has the periodic table, so you probably won't need it much.

`Elements.add`:
_`Elements.add(long protons, long neutrons, long halfLifeSeconds, String decayTo, String name, String symbol, boolean isIsotope)`_
Add a new element.

* `protons` - Amount of Protons
* `neutrons` - Amount of Neutrons
* `halfLifeSeconds` - Amount of Half Life this Material has in Seconds. `-1` for stable Materials
* `decayTo` - String representing the Elements it decays to. Separated by an '&' character
* `name` - Name of the Element
* `symbol` - Symbol of the Element

`Elements.get`: _`Elements.get(String name)`_

* `name` - the name of the element
  Get the element by name.

 protons | netrons | halfLifeSeconds | decayTo | name               | symbol   | isIsotope
---------|---------|-----------------|---------|--------------------|----------|-----------
 1       | 0       | -1              | null    | "Hydrogen"         | "H"      | false
 1       | 1       | -1              | "H"     | "Deuterium"        | "D"      | true
 1       | 2       | -1              | "D"     | "Tritium"          | "T"      | true
 2       | 2       | -1              | null    | "Helium"           | "He"     | false
 2       | 1       | -1              | "H&D"   | "Helium-3"         | "He-3"   | true
 3       | 4       | -1              | null    | "Lithium"          | "Li"     | false
 4       | 5       | -1              | null    | "Beryllium"        | "Be"     | false
 5       | 5       | -1              | null    | "Boron"            | "B"      | false
 6       | 6       | -1              | null    | "Carbon"           | "C"      | false
 7       | 7       | -1              | null    | "Nitrogen"         | "N"      | false
 8       | 8       | -1              | null    | "Oxygen"           | "O"      | false
 9       | 9       | -1              | null    | "Fluorine"         | "F"      | false
 10      | 10      | -1              | null    | "Neon"             | "Ne"     | false
 11      | 11      | -1              | null    | "Sodium"           | "Na"     | false
 12      | 12      | -1              | null    | "Magnesium"        | "Mg"     | false
 13      | 13      | -1              | null    | "Aluminium"        | "Al"     | false
 14      | 14      | -1              | null    | "Silicon"          | "Si"     | false
 15      | 15      | -1              | null    | "Phosphorus"       | "P"      | false
 16      | 16      | -1              | null    | "Sulfur"           | "S"      | false
 17      | 18      | -1              | null    | "Chlorine"         | "Cl"     | false
 18      | 22      | -1              | null    | "Argon"            | "Ar"     | false
 19      | 20      | -1              | null    | "Potassium"        | "K"      | false
 20      | 20      | -1              | null    | "Calcium"          | "Ca"     | false
 21      | 24      | -1              | null    | "Scandium"         | "Sc"     | false
 22      | 26      | -1              | null    | "Titanium"         | "Ti"     | false
 23      | 28      | -1              | null    | "Vanadium"         | "V"      | false
 24      | 28      | -1              | null    | "Chrome"           | "Cr"     | false
 25      | 30      | -1              | null    | "Manganese"        | "Mn"     | false
 26      | 30      | -1              | null    | "Iron"             | "Fe"     | false
 27      | 32      | -1              | null    | "Cobalt"           | "Co"     | false
 28      | 30      | -1              | null    | "Nickel"           | "Ni"     | false
 29      | 34      | -1              | null    | "Copper"           | "Cu"     | false
 30      | 35      | -1              | null    | "Zinc"             | "Zn"     | false
 31      | 39      | -1              | null    | "Gallium"          | "Ga"     | false
 32      | 40      | -1              | null    | "Germanium"        | "Ge"     | false
 33      | 42      | -1              | null    | "Arsenic"          | "As"     | false
 34      | 45      | -1              | null    | "Selenium"         | "Se"     | false
 35      | 45      | -1              | null    | "Bromine"          | "Br"     | false
 36      | 48      | -1              | null    | "Krypton"          | "Kr"     | false
 37      | 48      | -1              | null    | "Rubidium"         | "Rb"     | false
 38      | 49      | -1              | null    | "Strontium"        | "Sr"     | false
 39      | 50      | -1              | null    | "Yttrium"          | "Y"      | false
 40      | 51      | -1              | null    | "Zirconium"        | "Zr"     | false
 41      | 53      | -1              | null    | "Niobium"          | "Nb"     | false
 42      | 53      | -1              | null    | "Molybdenum"       | "Mo"     | false
 43      | 55      | -1              | null    | "Technetium"       | "Tc"     | false
 44      | 57      | -1              | null    | "Ruthenium"        | "Ru"     | false
 45      | 58      | -1              | null    | "Rhodium"          | "Rh"     | false
 46      | 60      | -1              | null    | "Palladium"        | "Pd"     | false
 47      | 60      | -1              | null    | "Silver"           | "Ag"     | false
 48      | 64      | -1              | null    | "Cadmium"          | "Cd"     | false
 49      | 65      | -1              | null    | "Indium"           | "In"     | false
 50      | 68      | -1              | null    | "Tin"              | "Sn"     | false
 51      | 70      | -1              | null    | "Antimony"         | "Sb"     | false
 52      | 75      | -1              | null    | "Tellurium"        | "Te"     | false
 53      | 74      | -1              | null    | "Iodine"           | "I"      | false
 54      | 77      | -1              | null    | "Xenon"            | "Xe"     | false
 55      | 77      | -1              | null    | "Caesium"          | "Cs"     | false
 56      | 81      | -1              | null    | "Barium"           | "Ba"     | false
 57      | 81      | -1              | null    | "Lanthanum"        | "La"     | false
 58      | 82      | -1              | null    | "Cerium"           | "Ce"     | false
 59      | 81      | -1              | null    | "Praseodymium"     | "Pr"     | false
 60      | 84      | -1              | null    | "Neodymium"        | "Nd"     | false
 61      | 83      | -1              | null    | "Promethium"       | "Pm"     | false
 62      | 88      | -1              | null    | "Samarium"         | "Sm"     | false
 63      | 88      | -1              | null    | "Europium"         | "Eu"     | false
 64      | 93      | -1              | null    | "Gadolinium"       | "Gd"     | false
 65      | 93      | -1              | null    | "Terbium"          | "Tb"     | false
 66      | 96      | -1              | null    | "Dysprosium"       | "Dy"     | false
 67      | 97      | -1              | null    | "Holmium"          | "Ho"     | false
 68      | 99      | -1              | null    | "Erbium"           | "Er"     | false
 69      | 99      | -1              | null    | "Thulium"          | "Tm"     | false
 70      | 103     | -1              | null    | "Ytterbium"        | "Yb"     | false
 71      | 103     | -1              | null    | "Lutetium"         | "Lu"     | false
 72      | 106     | -1              | null    | "Hafnium"          | "Hf"     | false
 73      | 107     | -1              | null    | "Tantalum"         | "Ta"     | false
 74      | 109     | -1              | null    | "Tungsten"         | "W"      | false
 75      | 111     | -1              | null    | "Rhenium"          | "Re"     | false
 76      | 114     | -1              | null    | "Osmium"           | "Os"     | false
 77      | 115     | -1              | null    | "Iridium"          | "Ir"     | false
 78      | 117     | -1              | null    | "Platinum"         | "Pt"     | false
 79      | 117     | -1              | null    | "Gold"             | "Au"     | false
 80      | 120     | -1              | null    | "Mercury"          | "Hg"     | false
 81      | 123     | -1              | null    | "Thallium"         | "Tl"     | false
 82      | 125     | -1              | null    | "Lead"             | "Pb"     | false
 83      | 125     | -1              | null    | "Bismuth"          | "Bi"     | false
 84      | 124     | -1              | null    | "Polonium"         | "Po"     | false
 85      | 124     | -1              | null    | "Astatine"         | "At"     | false
 86      | 134     | -1              | null    | "Radon"            | "Rn"     | false
 87      | 134     | -1              | null    | "Francium"         | "Fr"     | false
 88      | 136     | -1              | null    | "Radium"           | "Ra"     | false
 89      | 136     | -1              | null    | "Actinium"         | "Ac"     | false
 90      | 140     | -1              | null    | "Thorium"          | "Th"     | false
 91      | 138     | -1              | null    | "Protactinium"     | "Pa"     | false
 92      | 146     | -1              | null    | "Uranium"          | "U"      | false
 92      | 146     | -1              | null    | "Uranium-238"      | "U-238"  | false
 92      | 143     | -1              | null    | "Uranium-235"      | "U-235"  | true
 93      | 144     | -1              | null    | "Neptunium"        | "Np"     | false
 94      | 152     | -1              | null    | "Plutonium"        | "Pu"     | false
 94      | 145     | -1              | null    | "Plutonium-239"    | "Pu-239" | false
 94      | 149     | -1              | null    | "Plutonium-241"    | "Pu-241" | true
 95      | 150     | -1              | null    | "Americium"        | "Am"     | false
 96      | 153     | -1              | null    | "Curium"           | "Cm"     | false
 97      | 152     | -1              | null    | "Berkelium"        | "Bk"     | false
 98      | 153     | -1              | null    | "Californium"      | "Cf"     | false
 99      | 153     | -1              | null    | "Einsteinium"      | "Es"     | false
 100     | 157     | -1              | null    | "Fermium"          | "Fm"     | false
 101     | 157     | -1              | null    | "Mendelevium"      | "Md"     | false
 102     | 157     | -1              | null    | "Nobelium"         | "No"     | false
 103     | 159     | -1              | null    | "Lawrencium"       | "Lr"     | false
 104     | 161     | -1              | null    | "Rutherfordium"    | "Rf"     | false
 105     | 163     | -1              | null    | "Dubnium"          | "Db"     | false
 106     | 165     | -1              | null    | "Seaborgium"       | "Sg"     | false
 107     | 163     | -1              | null    | "Bohrium"          | "Bh"     | false
 108     | 169     | -1              | null    | "Hassium"          | "Hs"     | false
 109     | 167     | -1              | null    | "Meitnerium"       | "Mt"     | false
 110     | 171     | -1              | null    | "Darmstadtium"     | "Ds"     | false
 111     | 169     | -1              | null    | "Roentgenium"      | "Rg"     | false
 112     | 173     | -1              | null    | "Copernicium"      | "Cn"     | false
 113     | 171     | -1              | null    | "Nihonium"         | "Nh"     | false
 114     | 175     | -1              | null    | "Flerovium"        | "Fl"     | false
 115     | 173     | -1              | null    | "Moscovium"        | "Mc"     | false
 116     | 177     | -1              | null    | "Livermorium"      | "Lv"     | false
 117     | 177     | -1              | null    | "Tennessine"       | "Ts"     | false
 118     | 176     | -1              | null    | "Oganesson"        | "Og"     | false
 119     | 178     | -1              | null    | "Tritanium"        | "Tr"     | false
 120     | 180     | -1              | null    | "Duranium"         | "Dr"     | false
 125     | 198     | -1              | null    | "Trinium"          | "Ke"     | false
 174     | 352     | 140             | null    | "Naquadah"         | "Nq"     | true
 174     | 354     | 140             | null    | "NaquadahEnriched" | "Nq+"    | true
 174     | 348     | 140             | null    | "Naquadria"        | "Nq"     | true
 0       | 1000    | -1              | null    | "Neutronium"       | "Nt"     | false
 750     | 1000    | -1              | null    | "Adamantium"       | "Ad"     | false
 850     | 900     | -1              | null    | "Vibranium"        | "Vb"     | false
 550     | 670     | -1              | null    | "Taranium"         | "Tn"     | false

!!! example "Elemental Material Example"

    ```groovy
    import gregtech.api.GregTechAPI.MaterialEvent
    import gregtech.api.unification.material.Material
    import gregtech.api.unification.Elements

    // elements can be created outside the event
    def CEu = Elements.add(999, 999, -1, null, "GTCEu", "CEu", false) // create a new element.

    event_manager.listen { MaterialEvent event ->
        def element_material = new Material.Builder(32006, "element_material").element("GTCEu").build()

        def Au = Elements.get("Gold") // get an existing element.

        def element_material = new Material.Builder(32007, "element_material").element("Gold").build()
    }
    ```

***

!!! example "Material Creation Full Examples"

    ```groovy
    import gregtech.api.GregTechAPI.MaterialEvent
    import gregtech.api.unification.material.Material

    event_manager.listen { MaterialEvent event ->

        new Material.Builder(32000, "red_iron")
                .ingot().fluid()
                .color(0xF7B29B)
                .flags("generate_plate", "generate_rod", "generate_gear", "decomposition_by_centrifuging")
                .components(material('iron') * 1, material('redstone') * 1)
                .cableProperties(32, 2, 1)
                .build()

        new Material.Builder(32001, "glowing_redstone")
                .dust()
                .color(0x774D05).iconSet("bright")
                .flags(["decomposition_by_centrifuging"])
                .components([material('glowstone') * 1, material('redstone') * 1])
                .build()

        new Material.Builder(32002, "rare_iron")
                .ingot().fluid()
                .color(0x6AE26E).iconSet("bright")
                .flags("generate_plate", "generate_rod", "generate_gear", "disable_decomposition")
                .components(material('iron') * 1, material('rare_earth') * 1)
                .cableProperties(8, 2, 1)
                .build()

        new Material.Builder(32003, "obsidian_steel")
                .ingot().fluid()
                .color(0x414751).iconSet("metallic")
                .flags("generate_plate", "generate_rod", "disable_decomposition")
                .components(material('steel') * 1, material('obsidian') * 1)
                .build()

        new Material.Builder(32004, "silicon_steel")
                .ingot().fluid()
                .color(0xB2C0C1).iconSet("shiny")
                .flags("generate_plate", "generate_rod", "generate_gear", "decomposition_by_centrifuging")
                .components(material('steel') * 1, material('silicon') * 1)
                .build()

        new Material.Builder(32005, "rare_gold")
                .ingot().fluid()
                .color(0x755C40)
                .flags("generate_plate", "disable_decomposition")
                .components(material('gold') * 1, material('rare_earth') * 1)
                .build()
    }
    ```

## Modifying existing Materials

See the **Retrieving Existing Materials** section for information on retrieving existing materials.

The material registry can do more than just get materials.

_`MaterialRegistry.get(String materialName)`_

* `materialName` - get a `Material` by its unlocalized name.

_`MaterialRegistry.getAllMaterials()`_ get

* get a list of every material registered

Materials also have more methods and fields.

**Getters:**

_`getChemicalFormula()`_

* returns a string representation of the internal chemical formula (i.e. "H2O")

_`materialRGB`_ get default materialRGB.

* returns the in color of the material

_`radioactive`_

* returns whether the material is radioactive

_`protons`_

* returns the number of protons in the material

_`neutrons`_

* returns the number of neutrons in the material

_`mass`_

* returns the total amount of mass in the material

_`averageProtons`_

* returns the amount of protons divided by total amount of components in the material

_`averageNeutrons`_

* returns the amount of neutrons divided by total amount of components in the material

_`averageMass`_

* returns the amount of mass divided by total amount of components in the material

_`blastTemperature`_

* returns the material's blast furnace temperature

_`camelCaseName`_ get default camelCaseName.

* returns the string camelCase form of the material's unlocalized name. I.e. a name of "my_material" returns "
  myMaterial"

_`unlocalizedName`_

* returns the string of the material's unlocalized name

_`localizedName`_

* returns the string of the material's localized (translated) name

_`name`_

* returns toString() used on the material internally

**Setters:**

_`setFormula(String formula, @Optional boolean withFormatting)`_

Sets the internal formula and thus tooltip of this Material.

* `formula` - the string to set the formula to
* `@Optional withFormatting` - whether to apply number formatting (subscripts, etc) to the formula and tooltip

_`addFlags(String... names)`_

Adds additional flags to this Material.

* `names` - a string array of flags to add

_`setMaterialRGB(int materialRGB)`_

Sets the color of this Material.

* `materialRGB` - the int color to set. Accepts the raw int value or values in the `0x` format.

!!! example

    ```groovy
    import gregtech.api.GregTechAPI.PostMaterialEvent

    event_manager.listen { PostMaterialEvent event ->
        def gold = material('gold')
        def name = gold.toString() // "gold"
        def color = gold.getMaterialRGB() // 0xFFE650
        gold.setFormula("(Au)2Au", true) // set formula
        def formula = gold.getChemicalFormula() // "(Au)2Au"
        gold.addFlags("generate_long_rod", "generate_gear") // add gold long rod, add gold gear
    }
    ```
