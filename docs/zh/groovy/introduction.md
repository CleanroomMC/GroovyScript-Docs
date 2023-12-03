# Groovy
Groovy是一种基于Java的强大脚本语言。

在此选项卡中，您可以找到有关脚本语言本身的一些信息。
有关GroovyScript特定的内容，请参阅GroovyScript选项卡。

语法与Java非常相似，但具有其他脚本语言的一些便利之处。
最显着的是，您不需要在行尾使用 `;`。

## 注释
可以在脚本内添加将被编译器忽略的注释，如下所示：
```groovy
// 单行注释

/*
多行注释
 */
```

## 变量
变量可以保存具有特定类型的数据。可以使用关键字 `def` 或直接使用所需的类型创建它们。
然后是变量名。通常以小写字母开头。
最后是值。如果使用了 `def`，则值将定义类型。
```groovy
def num = 10   // 动态类型
int num2 = 100 // 强类型
```

## 数据类型
有不同类型的数据：基本类型和复杂类型。

### 基本类型
基本类型永远不能为null。它们总是有一个值。默认情况下，整数是 `int`<br>
例如 `1.5` 这样的小数默认为 `BigDecimal` 类型。这可能不是您想要的类型。
我强烈建议为 `double` 或 `float` 使用 `d` 或 `f` 后缀。<br>
`int`：范围从 -2^31 到 2^31 - 1 的任意整数<br>
`long`：范围从 -2^63 到 2^63 - 1 的任意整数<br>
`byte`：范围从 -2^7 到 2^7 - 1 的任意整数（-256 - 255）<br>
`short`：范围从 -2^15 到 2^15 - 1 的任意整数（-32768 - 32767）<br>
`float` 32位存储的十进制数<br>
`double` 64位存储的十进制数<br>
`boolean` true 或 false（没有其他值）
```groovy
def num1 = 10 // int
def num2 = 10l // long
def num3 = 10 as byte // byte
def num4 = 10 as short // byte
def num5 = 1.0f // float
def num6 = 1.0d // double
def bool = true // boolean
```

### 复杂类型
复杂类型是所有不是基本类型的类型。每个对象都属于此类别。
基本类型也有封箱的复杂类型。
如前所述，`def num = 1.5` 将创建一个 `BigDecimal`，它是复杂类型。<br>
`def num = 10G` 将创建一个 `BigInteger`，它几乎没有值限制，但可能占用大量内存，因此请尽量不要经常使用。

## 函数
函数是一组可以通过一行调用的指令。

### 定义函数
```groovy
// 接受单个参数并返回无结果的函数
def f(x) {
    println(x)
}

// 接受两个参数并返回它们的和的函数
def sum(x, y) {
    return x + y
}

// 指定类型是可选的
// 如果使用，如果传递了无效类型，将引发错误
def sum2(int x, int y) {
    return x + y
}
```

### 调用函数
我们将使用上面的函数。
```groovy
f(10) // 使用参数 10 调用函数
f(sum(4, 16)) // 使用 sum 的结果调用 f
```

## 导入
如果要使用任何类的短名称，您需要导入完整的类名。
大多数Java类默认已导入。
```groovy
import my.package.MyClass // 导入单个类
import my.other.package.* // 导入包中的所有类

import static my.package.MyClass.FIELD // 静态字段导入
import static my.package.MyClass.function // 静态函数导入
import static my.other.package.MyOtherClass.* // 导入类中的所有静态函数

import my.package.MyClass as MC // 导入别名
import static my.package.MyClass.function as f // 静态导入别名
```

## 进一步阅读

如果您想学习更高级的内容，请查看[官方Groovy文档](https://groovy-lang.org/documentation.html)。

一些有用的Groovy文档页面：

* [语法](https://groovy-lang.org/syntax.html)
* [运算符](https://groovy-lang.org/operators.html)
* [闭包](https://groovy-lang.org/closures.html)
* [语义](https://groovy-lang.org/semantics.html)