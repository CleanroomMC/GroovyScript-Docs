# Groovy
Groovy is a scripting language based on java.

## Basics
Here's the basics of Groovy to get you started.

### Variables and Datatypes
```groovy
// Numbers
def i = 10 // int of 10
def f = 3.5 // float of 3.5

// Booleans
def b = true // boolean true

// Strings
def s = 'hello' // String
def s2 = "hello" // can use either '' or ""

// Lists
def list = [1, 2, 3, 4, 5]

// Maps
def map = ['a': 1, 'b': 2, 'c': 3]

// Types
// Specifying exact types is optional, but allowed
// Specific types will error if assigned to something incompatible
int x = 10
String y = 20
List<Integer> nums = [1, 2, 3] 
```

### Conditionals and Loops
```groovy
// a standard if statement
if (a > b) {
    println('a is bigger than b')
} else if (a < b) {
    println('a is smaller than b')
} else {
    println('a is equal to b')
}

// standard java for loop
for (int i = 0; i < 5; i++) {
    println(i)
}

// for in loop
for (i in ['a', 'b', 'c']) {
    println(i)
}

// while loop
while (x > 0) {
    println(x)
    x--
}
```

### Functions
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

### Imports
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
