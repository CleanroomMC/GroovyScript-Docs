# 创建流体

!!! 注意
    这需要至少 GroovyScript 的版本 0.7.0。

## 最简单的方式

```groovy
content.createFluid(String name).register()
```

简单吧？
我们来分解一下：

- `content` 是一个全局变量。
- `createFluid(String name)` 创建一个流体构建器对象并返回它。名称是注册名称，只能包含小写字母和 `_`。
- `register()` 注册这个流体。如果没有这个，流体将不会出现在游戏中。

这将创建一个桶物品和一个带有白色水纹理的流体块。

## 设置器

- `setStill(ResourceLocation)` 设置静态流体纹理
- `setFlowing(ResourceLocation)` 设置流动流体纹理
- `setOverlay(ResourceLocation)` 设置覆盖流体纹理（通常为空）
- `setTexture(ResourceLocation still, ResourceLocation flowing)` 设置静态和流动流体纹理
- `setTexture(ResourceLocation still, ResourceLocation flowing, ResourceLocation overlay)` 设置静态、流动和覆盖流体纹理
- `setDefaultTexture()` 将静态和流动流体纹理设置为默认纹理（白色水）
- `setMetalTexture()` 将静态和流动流体纹理设置为 Tinkers 熔融金属纹理
- `setColor(int)` 设置流体颜色。纹理通常是白色。颜色叠加在纹理之上
- `setSound(SoundEvent fillSound, SoundEvent emptySound)` 设置桶装满和倒空的声音（默认是来自流体材料的声音）
- `setLuminosity(int)` 设置发光度。流体的光亮度从 0 到 15（默认是 0）。
- `setDensity(int)` 设置密度。完全是任意的值。负值意味着流体比空气轻。默认值是 1000。
- `setTemperature(int)` 设置温度。完全是任意的值。默认是 300（开尔文中的室温）。
- `setViscosity(int)` 设置黏性。完全是任意的值，数值越高，流体流动越慢。默认值是 1000。
- `setGaseous(boolean)` 设置流体是否是气体。通常这与负密度流体相关。默认值是 false。
- `setRarity(EnumRarity)` 设置流体的稀有度。这只用于工具提示颜色（据我所知）。默认是 `EnumRarity.COMMON`。
- `setWaterMaterial()` 将流体材料设置为水。这使流体块的行为类似于水。这是默认值。
- `setLavaMaterial()` 将流体材料设置为岩浆。这使流体块的行为类似于岩浆。（目前没有自定义材料）
- `noBlock()` 禁用流体块的生成。桶将无法在世界中放置流体。

??? 示例
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

## 注册流体

上面的例子为您创建了一个简单的流体，但您也可以自己创建流体。
使用以下方法注册自定义流体。

```groovy
content.registerFluid(Fluis)
```

!!! 警告
    这不推荐使用，因为使用 `createFluid(name).register()` 为您做了很多工作。

## 纹理

我们建议使用默认纹理。但是您也可以自己添加其他的。
如果流体有一个块，块状态 json 将自动生成，

## 翻译流体名称

在您的 lang 文件中添加 `fluid.[pack id].[fluid name]=Fluid Name`

例如对于熔融铁：
```mclang
fluid.placeholdername.molten_iron=Molten Iron
```