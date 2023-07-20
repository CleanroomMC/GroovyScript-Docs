# Groovy
Groovy是一门基于JVM的脚本语言, 它十分强大 (它在兼容Java语法的同时, 借鉴了Ruby,Python等语言的特性).

在本选项卡中, 您可以找到有关脚本语言本身的一些信息. 而有关 GroovyScript 的具体信息，请参阅 GroovyScript 选项卡。

Groovy的语法与 java 非常相似, 但它更加简洁而灵活. 最明显的是, 行尾不需要`;`.

## 注释
我们可以在脚本中添加注释, 注释能使你的脚本更易读, 编译器会忽略这些注释, 例如: 
````groovy
// 我是一行单行注释

/*
其实我是区块注释哒!
 */
````

## 变量
变量可以保存特定类型的数据. 可以用def关键字来定义变量, 而不一定需要写明具体的类型（实际上def关键字也可以省略). 然后是名称,通常以小写字母开头. 最后是值.(译者注:Groovy可以通过形如${var}的方式来进行字符串格式化)
```groovy
def num = 10   // 动态类型
int num2 = 100 // 强类型
```

## 数据类型
数据类型有主要数据类型(Primitive)和复数数据类型(Complex).

### 主要数据类型
主要数据类型不会为空, 它总有一个值. 整数默认为 `int` 类型<br>
像 `1.5` 之类的小数默认为 `BigDecimal` 类型. 它很可能不是你想要的.
我建议你使用 `d` 或 `f` 后缀来表示 `double` 或 `float`.<br>
`int`: 可以是 -2^31 到 2^31 - 1 之间的任何整数<br>
`long`: 可以是 -2^63 到 2^63 - 1 之间的任何整数 <br>
`byte`: 可以是 -2^7 到 2^7 - 1 (-128 - 127) 之间的任何整数.<br>
`short`: 可以是 -2^15 到 2^15 - 1 (-32768 - 32767) 之间的任何整数<br>
`float` 32位单精度的小数类型<br>
`double` 64位双精度的小数类型<br>
`boolean` 仅有 "真(true)"或"假(false)".

````groovy
def num1 = 10 // int
def num2 = 10l // long
def num3 = 10 as byte // byte
def num4 = 10 as short // byte
def num5 = 1.0f // float
def num6 = 1.0d // double
def bool = true // boolean
````

### 复数数据类型
Complex types are all types that are not primitive. Every object falls under this category.
Primitive types also have boxed complex types.
As said before `def num = 1.5` will create a `BigDecimal` which is complex.<br>
`def num = 10G` will create a `BigInteger` which has almost no value limit, but it can take a lot of memory, so try to not use to often.

## 函数
函数是一组指令，只需一行即可调用.

### 定义函数
```groovy
// 这是一个只接受一个参数, 不返回任何内容的函数
def f(x) {
    println(x)
}

// 接收两个参数并返回其和的函数
def sum(x, y) {
    return x + y
}

// 指定类型是可选的, 你可以省略它
// 如果你指定了, 则在传递无效类型时会出错
def sum2(int x, int y) {
    return x + y
}
```

### 调用函数
我们将用到上面定义的函数.
````groovy
f(10) // 调用函数"f", 参数为10
f(sum(4, 16)) // 用求和的结果作为参数, 调用函数"f"
````

## 导入
如果想要使用任何类的简短名称, 则需要先导入完整的类名.
但需要注意的是大多数javas类都是默认导入的.
```groovy
import my.package.MyClass // 导入一个类
import my.other.package.* // 导入一个包内的所有类

import static my.package.MyClass.FIELD // 静态字段导入
import static my.package.MyClass.function // 静态函数导入
import static my.other.package.MyOtherClass.* // 导入该类的所有静态函数

import my.package.MyClass as MC // import aliasing
import static my.package.MyClass.function as f // static import aliasing
```

## 更进一步

如果你觉得这些满足不了你, 请参见 [Official Groovy Documentation](https://groovy-lang.org/documentation.html).

另一些可能对你有用的 Groovy 文档页面:

* [Syntax](https://groovy-lang.org/syntax.html)
* [Operators](https://groovy-lang.org/operators.html)
* [Closures](https://groovy-lang.org/closures.html)
* [Semantics](https://groovy-lang.org/semantics.html)
