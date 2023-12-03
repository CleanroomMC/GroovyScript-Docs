# 构建器

构建器是一个包含构建对象方法的类。这些方法可以链接在一起，并且通常以 `.build()` 调用结束。
每个方法（`build()` 方法除外）应该返回相同的构建器实例。
GroovyScript中的配方构建器以 `.register()` 调用结束，因为配方是注册而不仅仅是构建，而 `.buildAndRegister()` 太长了。

!!! 例子 "构建器类示例"
    让我们看看一个简单的构建器类可能是什么样子：

    ```groovy
    class RecipeBuilder {
        private final List<IIngredient> inputs = new ArrayList()
        private final List<ItemStack> outputs = new ArrayList() // (1)

        RecipeBuilder input(IIngredient ingredient) {
            this.inputs.add(ingredient)
            return this     // 该方法返回此构建器 (2)
        }

        RecipeBuilder output(ItemStack itemStack) {
            this.outputs.add(itemStack)
            return this     // 该方法返回此构建器 (3)
        }

        Recipe build() {    // 通常，build方法返回将要构建的对象
            return new Recipe(inputs, outputs)
        }
    }
    ```

    1. 我们需要在某处存储输入和输出
    2. 通常在Groovy中不需要使用 `return` 关键字，但在这种情况下，它有助于理解概念。
    3. 通常在Groovy中不需要使用 `return` 关键字，但在这种情况下，它有助于理解概念。

!!! 例子 "用法示例"
    现在让我们使用构建器创建一个新的配方

    ```groovy
    def recipe = new RecipeBuilder()            // 首先创建一个配方构建器实例
            .input('<minecraft:iron_ingot>')    // 添加一个输入
            .input('<minecraft:clay_ball>' * 3) // 添加另一个输入
            .output('<minecraft:nether_star>')  // 添加一个输出
            .build()                            // 构建并返回一个配方实例
    ```

    注意每个方法调用是如何链接在一起的。这是因为 `input()` 和 `output()` 返回相同的构建器实例。<br>
    由于 `build()` 方法返回一个 `Recipe` 实例，因此 `recipe` 变量也将是 `Recipe` 类型。<br>
    与上面的代码相同的代码也可以放在一行中：

    ```groovy
    def recipe = new RecipeBuilder().input('<minecraft:iron_ingot>').input('<minecraft:clay_ball>' * 3).output('<minecraft:nether_star>').build()
    ```

    这做的事情完全相同，但如您所见，它更难看且难以阅读。换行符纯粹是为了美观，但强烈推荐使用。

    现在让我们看看没有构建器的情况下配方可能是什么样子：

    ```groovy
    def recipe = new Recipe(['<minecraft:iron_ingot>', '<minecraft:clay_ball>' * 3], ['<minecraft:nether_star>'])
    ```

    看起来还不错，对吧？现在想象一下，如果配方需要5个输入。或者10个。或者20个。而且你需要指定能量要求、持续时间，可能还有液体。<br>
    这就是构建器发挥作用的地方。

## 结论

构建器有助于在创建复杂对象时产生清晰的代码。
理解这个概念将有助于你在GroovyScript中，因为它们通常用于配方的创建。