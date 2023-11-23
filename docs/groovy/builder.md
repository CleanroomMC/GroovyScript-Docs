# Builder

A builder is a class that contains methods to build an object. Those methods can be chained together and often end in a `.build()` call.
Each method, except the `build()` method, should return the same builder instance.
The Recipe Builders in GroovyScript and with a `.register()` call, because the recipe is registered rather than just build and `.buildAndRegister()` is too long.

!!! example "Builder class example"
    Let's see what a simple Builder class can look like:

    ```groovy
    class RecipeBuilder {
        private final List<IIngredient> inputs = new ArrayList()
        private final List<ItemStack> outputs = new ArrayList() // (1)

        RecipeBuilder input(IIngredient ingredient) {
            this.inputs.add(ingredient)
            return this     // the method returns this builder (2)
        }

        RecipeBuilder output(ItemStack itemStack) {
            this.outputs.add(itemStack)
            return this     // the method returns this builder (3)
        }

        Recipe build() {    // the build method usually returns the object that will be build
            return new Recipe(inputs, outputs)
        }
    }
    ```

    1. We need to store our inputs and outputs somewhere
    2. Usually the return keyword is not needed in groovy, but in this case it helps to understand the concept.
    3. Usually the return keyword is not needed in groovy, but in this case it helps to understand the concept.

??? example "Usage example"
    Now let's create a new recipe using the builder

    ```groovy
    def recipe = new RecipeBuilder()            // first create a recipe builder instance
            .input('<minecraft:iron_ingot>')    // add a input
            .input('<minecraft:clay_ball>' * 3) // add another input
            .output('<minecraft:nether_star>')  // add a output
            .build()                            // build and return a recipe instance
    ```

    Notice how each method call is chained together. This is because `input()` and `output()` return the same builder instance.<br>
    Since the `build()` method returns a `Recipe` instance, the `recipe` variable will also be of type `Recipe`.<br>
    The same code as above can also be put in a single line:

    ```groovy
    def recipe = new RecipeBuilder().input('<minecraft:iron_ingot>').input('<minecraft:clay_ball>' * 3).output('<minecraft:nether_star>').build()
    ```

    This does exactly the same thing, but as you can see it is uglier and harder to read. The line breaks are purely aesthetically, but are highly recommended.

    Now lets see what the recipe could look like without a builder:

    ```groovy
    def recipe = new Recipe(['<minecraft:iron_ingot>', '<minecraft:clay_ball>' * 3], ['<minecraft:nether_star>'])
    ```

    That doesn't look too bad right? Now imagine the recipe requires 5 inputs. Or 10. Or 20. And you need to specify energy requirement, duration and maybe fluids.<br>
    This is where Builders shine.

## Conclusion

Builders help to produce clean code while creating complex objects.
Understanding the concept will help you in GroovyScript, since they are used commonly for recipes.
