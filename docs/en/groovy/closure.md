# Closures

Closures are like lambdas in java, but slightly different.

# For beginners

You may know what a method is. A method is a set order of instructions you can call. For example:

````groovy
def print_numbers(int n) {
    for (def i : 0..n) {
        log.info(i)
    }
}
````

This method prints numbers from 0 to a given number to the log.

````groovy
print_numbers(5)
````

This will now output

````
0
1
2
3
4
````

You can call that method as often as you want with any number input.

Now closures are methods, but you can carry them around. Example:

````groovy
def print_numbers = { int n -> /*(1)*/
    for (def i : 0..n) {
        log.info(i)
    }
}
````

1. Most of the time the type is optional, so here it would become `{ n -> ...`

This closure does the same thing as the method above, but it's a variable instead of a method. Just like any other
variable you can pass it to other methods. (See [Events](../groovyscript/minecraft/events/aa_events.md)).
You can invoke this closure the same way you do with a method:
````groovy
print_numbers(3)
````