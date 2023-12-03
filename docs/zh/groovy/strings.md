# 字符串
字符串是字符的序列。
有多种定义字符串的方法，每种方法都有不同的作用。
最简单的方法是使用 `''`。在 Java 中，它们用于表示字符。在这里，它们创建字符串并没有什么特殊之处。
更高级的方法是使用 `""`。它们允许您在文本字面值中使用变量。
最后一种方法是使用 `\\`。这对于正则表达式非常完美，因为您不需要转义任何 `\`。
```groovy
def s = 'hello' // 字符串
def s2 = "hello" // 可以使用 '' 或 ""
assert s == s2 // 两个字符串相等

def num = 7
def numberOfDays = 'There are ' + num + ' days in a week' // 使用连接在字符串中使用变量
def numberOfDays2 = "There are $num days in a week" // 使用 $ 在字符串中使用变量
```