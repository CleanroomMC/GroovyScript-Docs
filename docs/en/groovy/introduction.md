# Groovy
Groovy is a powerful scripting language based on java.

In this tab you can find some information about the scripting language itself.
For GroovyScript specific stuff refer to the GroovyScript tab.

The syntax is very similar to java, but with some conveniences from other scripting languages.
The most noticeable is that you don't need `;` at the end of a line.

## Comments
Comments can be made inside scripts that will be ignored by the compiler like this:
```groovy
// single line comment

/*
Multi line comment
 */
```

## Variables
Variables can hold data with a specific type. They can be created with the keyword `def` or by using the desired type directly.
After that comes the name. It usually starts with a lower case letter.
At the end is the value. If you used `def` then the value will define the type.
```groovy
def num = 10   // dynamically typed
int num2 = 100 // strongly typed
```

## Datatypes
There are differnt kinds of datatypes: primitive and complex.

### Primitive types
Primitive types can never be null. They always have a value. A whole number is by default a `int`<br>
Decimals like `1.5` have by default the type `BigDecimal`. Which is most likely not what you want.
I highly recommend to use the `d` or `f` suffix for `double` or `float`.<br>
`int`: any whole number from -2^31 to 2^31 - 1<br>
`long`: any whole number from -2^63 to 2^63 - 1 <br>
`byte`: any whole number from -2^7 to 2^7 - 1 (-256 - 255)<br>
`short`: any whole number from -2^15 to 2^15 - 1 (-32768 - 32767)<br>
`float` a decimal number stored in 32 bits<br>
`double` a decimal number stored in 64 bits<br>
`boolean` true or false (nothing else)
```groovy
def num1 = 10 // int
def num2 = 10l // long
def num3 = 10 as byte // byte
def num4 = 10 as short // byte
def num5 = 1.0f // float
def num6 = 1.0d // double
def bool = true // boolean
```

### Complex types
Complex types are all types that are not primitive. Every object falls under this category.
Primitive types also have boxed complex types.
As said before `def num = 1.5` will create a `BigDecimal` which is complex.<br>
`def num = 10G` will create a `BigInteger` which has almost no value limit, but it can take a lot of memory, so try to not use to often.

## Functions
A function is a set of instructions that can be called with a single line.

### Defining Functions
```groovy
// function which takes a single parameter and returns nothing
def f(x) {
    println(x)
}

// function which takes two parameters and returns their sum
def sum(x, y) {
    return x + y
}

// specifying types is optional
// if used, it will error if passed invalid types
def sum2(int x, int y) {
    return x + y
}
```

### Calling functions
We'll take the functions from above.
```groovy
f(10) // calls the function with the parameter 10
f(sum(4, 16)) // calls f with the result of sum
```

## Imports
If you want to use any classes short name you need to import the full class name.
Most of javas classes are imported by default.
```groovy
import my.package.MyClass // import a single class
import my.other.package.* // import all classes from a package

import static my.package.MyClass.FIELD // static field import
import static my.package.MyClass.function // static function import
import static my.other.package.MyOtherClass.* // import all static functions from the class

import my.package.MyClass as MC // import aliasing
import static my.package.MyClass.function as f // static import aliasing
```

## Further Reading

If there's something more advanced you'd like to learn, take a look at the [Official Groovy Documentation](https://groovy-lang.org/documentation.html).

Some useful Groovy Documentation pages:

* [Syntax](https://groovy-lang.org/syntax.html)
* [Operators](https://groovy-lang.org/operators.html)
* [Closures](https://groovy-lang.org/closures.html)
* [Semantics](https://groovy-lang.org/semantics.html)
